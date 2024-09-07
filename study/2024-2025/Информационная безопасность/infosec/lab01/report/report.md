---
## Front matter
title: "Основы информационной безопасности"
subtitle: "Лабораторная работа № 1. Настройка виртуальной машины и установка операционной системы "
author: "Подлесный Иван Сергеевич"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

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
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Постановка задачи

Целью данной работы является приобретение практических навыков установки операционной системы на виртуальную машину, и базовая настройка системы

# Выполнение лабораторной работы

Проверим в свойствах VirtualBox месторасположение каталога для виртуальных машин. Для этого в VirtualBox выберите Файл -> Настройки, вкладка Общие. 


![Имя и Операционная система VM](1.png){#fig:001 width=70%}

Образ Rocky Linux был скачен заранее. Создадим виртуальную машину. Добавим новый привод оптических дисков и выберите образ операционной системы, укажем имя виртуальной машины, тип операционной системы -- Linux, RedHat (64-bit), рамзер основной памяти  -- 4096 МБ,  конфигурацию жёсткого диска — загрузочный, VDI (BirtualBox Disk Image), динамический виртуальный диск,  размер диска — 40 ГБ.

![Окно «Имя машины и тип ОС»](2.png){#fig:002 width=70%}

![Окно «Автоматическая установка гостевой ОС»](3.png){#fig:003 width=70%}

![Окно подключения или создания жёсткого диска на виртуальной машине](4.png){#fig:004 width=70%}

Запустим виртуальную машину, выберем English в качестве языка интерфейса, дополнительно добавим русский язык и установим комбинацию клавиш для смены раскладки(рис. @fig:005).

![Установка языка интерфейса ОС](5.png){#fig:005 width=70%}

В разделе выбора программ укажем в качестве базового окружения Server with GUI, а в качестве дополнения -- Development Tools (рис. @fig:006):

![Окно настройки установки: выбор программ](6.png){#fig:006 width=70%}

Включим сетевое соединение и в качестве имени узла укажем eademidova.localdomain (рис. @fig:008):

![Окно настройки установки: сеть и имя узла](7.png){#fig:007 width=70%}

Установим пароль для root и пользователя с правами администратора(рис. @fig:009, @fig:010):

![Установка пароля для root](8.png){#fig:008 width=70%}


После завершения установки операционной системы корректно перезапустим виртуальную машину и при запросе примем условия лицензии. 

Войдем в ОС под заданной при установке учётной записью. В меню Устройства виртуальной машины подключим образ диска дополнений гостевой ОС, введем пароль пользователя root(рис. @fig:009):

![Подключение образа диска дополнений](9.png){#fig:009 width=70%}

# Домашнее задание

В окне терминала проанализируем последовательность загрузки системы, выполнив команду dmesg (рис. @fig:010):

![Вывод информации о загрузке системы](10.png){#fig:010 width=70%}

Получим следующую информацию при помощи команды grep(рис. @fig:011):

1. Версия ядра Linux (Linux version).
3. Модель процессора (CPU0).
4. Объем доступной оперативной памяти (Memory available).
5. Тип обнаруженного гипервизора (Hypervisor detected).

![Вывод нужной информации о системе из файла диагностики](11.png){#fig:011 width=70%}

# Выводы

В результате выполнения работы были приобретены практические навыки установки операционной системы на виртуальную машину, настройки минимально необходимых для дальнейшей работы.

