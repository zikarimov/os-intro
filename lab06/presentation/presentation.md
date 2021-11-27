---
## Front matter
lang: ru-RU
title: Мандатное разграничение прав в Linux
author: Каримов Зуфар НПИ-01-18

institute: RUDN University

date: Информационная безопасность, 26 ноября, 2021, Москва, Россия

## Formatting
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
toc: false
slide_level: 2
theme: metropolis
header-includes:
 - \metroset{progressbar=frametitle,sectionpage=progressbar,numbering=fraction}
 - '\makeatletter'
 - '\beamer@ignorenonframefalse'
 - '\makeatother'
aspectratio: 43
section-titles: true

---

# Цель лабораторной работы

Развить навыки администрирования ОС Linux. Получить первое практическое знакомство с технологией SELinux.

Проверить работу SELinx на практике совместно с веб-сервером
Apache.

# Процесс выполнения лабораторной работы

## Выполнение работы

1. Создание файла

2. Проверить работу SELinx на практике совместно с веб-сервером Apache.

3. Веб-сервер Apache на прослушивание ТСР-порта 81


## Создание файла

### Результат

![Файл test.html](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_8.png?raw=true){ #fig:001 width=70% }


## Проверить работу SELinx на практике совместно с веб-сервером Apache.

### Результат

![Обращение к файлу через браузер](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_10.png?raw=true){ #fig:002 width=50% }

##

![Контекст файла](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_9.png?raw=true){ #fig:003 width=50% }


## Веб-сервер Apache на прослушивание ТСР-порта 81

### Результат

![ТСР-порт 81](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_15.png?raw=true){ #fig:004 width=70% }

## Результат

![Обращение к файлу через браузер](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_21.png?raw=true){ #fig:005 width=50% }

##

![Удаление TCP-порта 81](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_23.png?raw=true){ #fig:006 width=50% }


# Выводы

Развил навыки администрирования ОС Linux. Получил первое практическое знакомство с технологией SELinux.

Проверил работу SELinx на практике совместно с веб-сервером
Apache.
