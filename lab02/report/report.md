---
# Front matter
lang: ru-RU
title: "Отчет по лабораторной работе №2"
subtitle: "Дискреционное разграничение прав в Linux. Основные атрибуты"
author: "Каримов Зуфар НПИ-01-18"

# Formatting
toc-title: "Содержание"
toc: true # Table of contents
fontsize: 12pt
linestretch: 1.5
papersize: a4paper
documentclass: scrreprt
polyglossia-lang: russian
polyglossia-otherlangs: english
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase
indent: true
pdf-engine: lualatex
header-includes:
  - \linepenalty=10 # the penalty added to the badness of each line within a paragraph (no associated penalty node) Increasing the value makes tex try to have fewer lines in the paragraph.
  - \interlinepenalty=0 # value of the penalty (node) added after each line of a paragraph.
  - \hyphenpenalty=50 # the penalty for line breaking at an automatically inserted hyphen
  - \exhyphenpenalty=50 # the penalty for line breaking at an explicit hyphen
  - \binoppenalty=700 # the penalty for breaking a line at a binary operator
  - \relpenalty=500 # the penalty for breaking a line at a relation
  - \clubpenalty=150 # extra penalty for breaking after first line of a paragraph
  - \widowpenalty=150 # extra penalty for breaking before last line of a paragraph
  - \displaywidowpenalty=50 # extra penalty for breaking before last line before a display math
  - \brokenpenalty=100 # extra penalty for page breaking after a hyphenated line
  - \predisplaypenalty=10000 # penalty for breaking before a display
  - \postdisplaypenalty=0 # penalty for breaking after a display
  - \floatingpenalty = 20000 # penalty for splitting an insertion (can only be split footnote in standard LaTeX)
  - \raggedbottom # or \flushbottom
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

# Цель работы

Получение практических навыков работы в консоли с атрибутами файлов, закрепление теоретических основ дискреционного разграничения доступа в современных системах с открытым кодом на базе ОС Linux

# Последовательность выполнения работы

Постарайтесь последовательно выполнить все пункты, занося ваши ответы на поставленные вопросы и замечания в отчёт.

1. В установленной при выполнении предыдущей лабораторной работы операционной системе создайте учётную запись пользователя guest (использую учётную запись администратора):

useradd guest

2. Задайте пароль для пользователя guest (использую учётную запись администратора):

passwd guest (рис. -@fig:001)

![Создали нового пользователя](https://github.com/zikarimov/os-intro/blob/master/lab02/image/Screenshot_1.png?raw=true){ #fig:001 width=70% }

3. Войдите в систему от имени пользователя guest. (рис. -@fig:002)

![Выбираем пользователя](https://github.com/zikarimov/os-intro/blob/master/lab02/image/Screenshot_2.png?raw=true){ #fig:002 width=70% }

Задаем пароль, чтобы войти в систему (рис. -@fig:003)

![Вход в систему](https://github.com/zikarimov/os-intro/blob/master/lab02/image/Screenshot_3.png?raw=true){ #fig:003 width=70% }

4. Определите директорию, в которой вы находитесь, командой pwd. Сравните её с приглашением командной строки. Определите, является ли она вашей домашней директорией? Если нет, зайдите в домашнюю директорию.

5. Уточните имя вашего пользователя командой whoami.

6. Уточните имя вашего пользователя, его группу, а также группы, куда входит пользователь, командой id. Выведенные значения uid, gid и др. запомните. Сравните вывод id с выводом команды groups. (рис. -@fig:004)

![Уточняем id пользователя](https://github.com/zikarimov/os-intro/blob/master/lab02/image/Screenshot_4.png?raw=true){ #fig:004 width=70% }

7. Сравните полученную информацию об имени пользователя с данными, выводимыми в приглашении командной строки.

8. Просмотрите файл /etc/passwd командой

cat /etc/passwd (рис. -@fig:005)

![Определение id пользователя ](https://github.com/zikarimov/os-intro/blob/master/lab02/image/Screenshot_5.png?raw=true){ #fig:005 width=70% }

9. Определите существующие в системе директории командой

ls -l /home/

Удалось ли вам получить список поддиректорий директории /home? Какие права установлены на директориях?

10. Проверьте, какие расширенные атрибуты установлены на поддиректориях, находящихся в директории /home, командой:

lsattr /home

Удалось ли вам увидеть расширенные атрибуты директории? Удалось ли вам увидеть расширенные атрибуты директорий других пользователей?

11. Создайте в домашней директории поддиректорию dir1 командой

mkdir dir1

Определите командами ls -l и lsattr, какие права доступа и расширенные атрибуты были выставлены на директорию dir1. (рис. -@fig:006)


![Окно «Размер основной памяти»](https://github.com/zikarimov/os-intro/blob/master/lab02/image/Screenshot_6.png?raw=true){ #fig:006 width=70% }

Нет, не удалось получить список поддиректорий директории /home. На директориях установлены следующие права: r - права на чтение, w - права на запись, x - права на исполнение. И все эти права только для владельца.(user)

Нет, не удалось увидеть расширенные атрибуты директории и атрибуты директорий других пользователей.

На директорию dirl установлены следующие права: r - права на чтение, w - права на запись, x - права на исполнение для владельца и для основной группы пользователей, а для остальных только чтение и исполнение без права записи.

12. Снимите с директории dir1 все атрибуты командой

chmod 000 dir1

и проверьте с её помощью правильность выполнения команды

ls -l

13. Попытайтесь создать в директории dir1 файл file1 командой

echo "test" > /home/guest/dir1/file1

Объясните, почему вы получили отказ в выполнении операции по созданию файла? Оцените, как сообщение об ошибке отразилось на создании файла? Проверьте командой

ls -l /home/guest/dirl

действительно ли файл file1 не находится внутри директории dir1. (рис. -@fig:007)

![Снятие атрибутов](https://github.com/zikarimov/os-intro/blob/master/lab02/image/Screenshot_7.png?raw=true){ #fig:007 width=70% }

Получили отказ, потому что команда

chmod 000

отключила все права доступа на директорию. Создать файл тоже не удалось так как нету прав на запись.

14. Заполните таблицу «Установленные права и разрешённые действия», выполняя действия от имени владельца директории (файлов), определив опытным путём, какие операции разрешены, а какие нет. Если операция разрешена, занесите в таблицу знак «+», если не разрешена, знак «-». (рис. -@fig:008)

![Установленные права и разрешённые действия](https://github.com/zikarimov/os-intro/blob/master/lab02/image/Screenshot_9.png?raw=true){ #fig:008 width=70% }

15. На основании заполненной таблицы определите те или иные минимально необходимые права для выполнения операций внутри директории dir1, заполните табл. 2.2.

![Минимально необходимые права](https://github.com/zikarimov/os-intro/blob/master/lab02/image/Screenshot_10.png?raw=true){ #fig:009 width=70% }


# Выводы

Получил практические навыкы работы в консоли с атрибутами файлов, закрепил теоретические основы дискреционного разграничения доступа в современных системах с открытым кодом на базе ОС Linux.
