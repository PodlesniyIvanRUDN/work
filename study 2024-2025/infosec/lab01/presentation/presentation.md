---
## Front matter
lang: ru-RU
title:  Основы информационной безопасности. Лабораторная работа №1
subtitle: Установка операционной системы на виртуальную машину"
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

## Цель Работы
Целью данной работы является приобретение практических навыков установки операционной системы на виртуальную машину, и базовая настройка системы

# Ход работы


## Установка ОС

![Имя и Операционная система VM](1.png){#fig:001 width=70%}

## Установка ОС

![Окно «Имя машины и тип ОС»](2.png){#fig:002 width=70%}

## Установка ОС

![Окно «Автоматическая установка гостевой ОС»](3.png){#fig:003 width=70%}

## Установка ОС

![Окно подключения или создания жёсткого диска на виртуальной машине](4.png){#fig:004 width=70%}

## Установка ОС

![Установка языка интерфейса ОС](5.png){#fig:005 width=70%}

## Установка ОС

![Окно настройки установки: выбор программ](6.png){#fig:006 width=70%}

## Установка ОС

![Окно настройки установки: сеть и имя узла](7.png){#fig:007 width=70%}

## Установка ОС

![Установка пароля для root](8.png){#fig:008 width=70%}

## Установка ОС
![Подключение образа диска дополнений](9.png){#fig:011 width=70%}

## Настройка ОС

В окне терминала проанализируем последовательность загрузки системы, выполнив команду dmesg (рис. @fig:010):

![Вывод информации о загрузке системы](10.png){#fig:010 width=70%}

# Домашнее задание

Получим следующую информацию при помощи команды grep(рис. @fig:011):

1. Версия ядра Linux (Linux version).
3. Модель процессора (CPU0).
4. Объем доступной оперативной памяти (Memory available).
5. Тип обнаруженного гипервизора (Hypervisor detected).

## Домашнее задание

![Вывод нужной информации о системе из файла диагностики](11.png){#fig:012 width=70%}

# Заключение

## Выводы

В результате выполнения работы были приобретены практические навыки установки операционной системы на виртуальную машину, настройки минимально необходимых для дальнейшей работы.

