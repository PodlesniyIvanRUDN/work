---
## Front matter
lang: ru-RU
title: "Основы информационной безопасности"
subtitle: "Индивидуальный проект. Этап № 2. Установка DVWA"
author: |
	Подлесный Иван Сергеевич.
institute: Российский Университет дружбы народов
date: 07.09.2024

## i18n babel
babel-lang: russian
babel-otherlangs: english

## Formatting pdf
toc: false
toc-title: Содержание
slide_level: 2
aspectratio: 169
section-titles: true
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
---

# Информация

## Докладчик

  * Подлесный Иван Сергеевич
  * студент группы НКНбд-01-21
  * Российский университет дружбы народов


# Вводная часть

# Цель работы

Целью данной работы является проведение brute-force атаки на приложение DVWA.


# Ход работы

## Установим низкий уровень защиты DVWA(рис. @fig:001)

![Уровень защиты DVWA](1.jpg){#fig:001 width=70%}

## Откроем страницу для проведения атаки brute force(рис. @fig:002).

![Форма для ввода пароля](2.jpg){#fig:002 width=70%}

## Просмотр файла с паролями

В Kali лежит файл с наиболее популярными паролями, распакуем его и увидим, что уже в начале есть пароль, который установлен по умолчанию для нашего аккаунта(рис. @fig:004, @fig:005).

![Вывод из файла rockyou.txt 10 наиболее популярных паролей](4.jpg){#fig:004 width=70%}

## Рассмотрим данные о запросе на вход(рис. @fig:005).

![Данные о запросе на вход](5.jpg){#fig:005 width=70%}



## Исходные данные:

- IP сервера 127.0.0.1(localhost);
- Для авторизации используется html форма, которая отправляет по адресу http://localhost/DVWA/vulnerabilities/brute методом GET запрос вида username=admin&password=test_password;
- В случае неудачной аутентификации пользователь наблюдает сообщение Username and/or password incorrect.

## Запрос к Hydra

Запрос к Hydra будет следующим образом(рис. @fig:006):

![Запрос к Hydra](6.jpg){#fig:006 width=70%}

## Итог

В результате получим нужный пароль(рис. @fig:007):

![Проверка полученного пароля](7.jpg){#fig:007 width=70%}


# Заключение

## Выводы

В результате выполнения была успешно проведена brute-force атака на приложение DVWA.
