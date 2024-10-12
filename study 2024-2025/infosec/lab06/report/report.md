---
## Front matter
title: "Основы информационной безопасности"
subtitle: "Лабораторная работа № 6. Мандатное разграничение прав в Linux"
author: "Подлесный Иван Сергеевич"
## Generic otions
lang: ru-RU
toc-title: "Содержание"
## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: false # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage[T1]{fontenc}
  - \usepackage{lmodern}
  - \usepackage[utf8]{inputenx}
  - \input{ix-utf8enc.dfu}
  - \usepackage[T2A]{fontenc}
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---
# Цель работы

Целью данной работы является приобретение практических навыков администрирования ОС Linux. Получить первое практическое знакомство с технологией SELinux. Проверить работу SELinx на практике совместно с веб-сервером Apache.


# Выполнение лабораторной работы

В конфигурационном файле /etc/httpd/httpd.conf зададим параметр ServerName.
 Отключим фильтр командами(рис. @fig:001)

![Подготовка лабораторного стенда](1.1.jpg){#fig:001 width=70%}


Войдем в систему с полученными учётными данными и убедимся, что SELinux работает в режиме enforcing политики targeted с помощью команд getenforce и sestatus(рис. @fig:002).

![Проверка статуса SELinux](1.jpg){#fig:002 width=70%}

Проверим, что веб-сервер работает (рис. @fig:003).

![Проверка статуса веб-сервера](3.jpg){#fig:003 width=70%}

Найдем веб-сервер Apache в списке процессов, определим его контекст безопасности(рис. @fig:004)

![Просмотр контекста безопасности веб-сервера](4.jpg){#fig:004 width=70%}


Посмотрим текущее состояние переключателей SELinux для Apache(рис. @fig:005)

![Состояние переключателей SELinux для Apache](5.jpg){#fig:005 width=70%}

Посмотрим статистику по политике с помощью команды seinfo(рис. @fig:006):

![Статистика по политике](6.jpg){#fig:006 width=70%}

Определив тип файлов и поддиректорий, находящихся в директории /var/www, с помощью команды ls -lZ /var/www, увидим, что есть директория, содержащая cgi-скрипты, и директория /var/www/html, содержащая все скрипты httpd(в данный момент пустая)(рис. @fig:008):

![Просмотр типов директорий в /var/www](8.jpg){#fig:008 width=70%}

Можно увидеть, что создание файлов в директории /var/www/html разрешено только владельцу -- root.

Создадим от имени суперпользователя  html-файл /var/www/html/test.html следующего содержания(рис. @fig:009):

![Содержимое html-файла /var/www/html/test.html](9.jpg){#fig:009 width=70%}

Посмотрим контекст безопасности, заданный по умолчанию для html документа(@fig:010):

![Установка пароля для пользователя с правами администратора](10.jpg){#fig:010 width=70%}

Увидим, что файлам по умолчанию сопоставляется свободный пользователь SELinux unconfined_u, указана роль  object_r используется по умолчанию для файлов на «постоянных» носителях и на сетевых файловых системах и тип httpd_sys_content_t, который позволяет процессу httpd получить доступ к файлу

Обратимся к файлу через веб-сервер, введя в браузере адрес http://127.0.0.1/test.html, убедимся, что файл был успешно отображён.(рис. @fig:011):

![Открытие html-страницы через браузер](11.jpg){#fig:011 width=70%}

Изучим справку man httpd_selinux (через интернет, ибо команда не работает), выясним, какие контексты файлов определены для httpd.
Сопоставив их с типом файла test.html увидим, что его контекст httpd_sys_content_t для содержимого, которое должно быть доступно для всех скриптов httpd и для самого демона. 
Изменим контекст файла /var/www/html/test.html с httpd_sys_content_t на тот, к которому процесс httpd не должен иметь доступа -- samba_share_t(рис. @fig:012):

![Изменение контекста файла /var/www/html/test.html](12.jpg){#fig:012 width=70%}

Теперь снова попробуем получить доступ к файлу через браузер и получим отказ(рис. @fig:013):

![Отказ в доступе к html-странице через браузер](13.jpg){#fig:013 width=70%}

Посмотрим log-файлы веб-сервера Apache и системный лог-файл и увидим, что отказ происходит, так как доступ запрещен SELinux именно к веб-серверу(на просто просмтр текстовых файлов это не влияет)(рис. @fig:014):

![Просмотр лог-файлов](14.jpg){#fig:014 width=70%}

Запустим веб-сервер Apache на прослушивание ТСР-порта 81. Для этого в файле /etc/httpd/httpd.conf найдем строчку Listen 80 и заменим её на Listen 81(рис. @fig:015):

![Замена прослушиваемого порта](15.jpg){#fig:015 width=70%}

Выполним перезапуск веб-сервера Apache и  не увидим изменений по не понятным мне причинам, несмотря на то, что 81 порт не является официальным портом для доступа по TCP(рис. @fig:016):

![Открытие html-страницы через браузер при прослушивании 81 порта](13.jpg){#fig:016 width=70%}

Просмотрев лог-файлы увидим, что порт для прослушивания был сменен(рис. @fig:017):

![Просмотр лог-файлов](17.jpg){#fig:017 width=70%}

Также этот порт мог быть отключен, тогда мы бы совсем не видели страницу, добавлять порты и просматривать актуальные можно с помощью команды seamanage(рис. @fig:018):

![Просмотр портов с помощью seamnage](18.jpg){#fig:018 width=70%}


# Выводы

В результате выполнения работы были получены базовые навыки работы с технологией SELinux. Проверена работа SELinx на практике совместно с веб-сервером Apache.



