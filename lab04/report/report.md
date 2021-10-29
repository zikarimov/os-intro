---
# Front matter
lang: ru-RU
title: "Отчет по лабораторной работе №4"
subtitle: "Дискреционное разграничение прав в Linux. Расширенные атрибуты"
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

Получение практических навыков работы в консоли с расширенными атрибутами файлов


# Последовательность выполнения работы


1. От имени пользователя guest определите расширенные атрибуты файла /home/guest/dir1/file1 командой

lsattr /home/guest/dir1/file1

2. Установите командой

chmod 600 file1

на файл file1 права, разрешающие чтение и запись для владельца файла.


3. Попробуйте установить на файл /home/guest/dir1/file1 расширенный атрибут a от имени пользователя guest:

chattr +a /home/guest/dir1/file1

В ответ вы должны получить отказ от выполнения операции. (рис. -@fig:001)

![Создаем второго нового пользователя](https://github.com/zikarimov/os-intro/blob/master/lab04/image/Screenshot_2.png?raw=true){ #fig:001 width=70% }

4. Зайдите на третью консоль с правами администратора либо повысьте свои права с помощью команды su. Попробуйте установить расширенный атрибут a на файл /home/guest/dir1/file1 от имени суперпользователя:

chattr +a /home/guest/dir1/file1 (рис. -@fig:002)

![Создаем второго нового пользователя](https://github.com/zikarimov/os-intro/blob/master/lab04/image/Screenshot_1.png?raw=true){ #fig:002 width=70% }

5. От пользователя guest проверьте правильность установления атрибута:

lsattr /home/guest/dir1/file1

6. Выполните дозапись в файл file1 слова «test» командой

echo "test" /home/guest/dir1/file1

После этого выполните чтение файла file1 командой

cat /home/guest/dir1/file1

Убедитесь, что слово test было успешно записано в file1.

7. Попробуйте удалить файл file1 либо стереть имеющуюся в нём информацию командой

echo "abcd" > /home/guest/dirl/file1

Попробуйте переименовать файл.

8. Попробуйте с помощью команды

chmod 000 file1

установить на файл file1 права, например, запрещающие чтение и запись для владельца файла. Удалось ли вам успешно выполнить указанные команды? (рис. -@fig:003)

![Определение id пользователя guest](https://github.com/zikarimov/os-intro/blob/master/lab04/image/Screenshot_2.png?raw=true){ #fig:003 width=70% }


9. Снимите расширенный атрибут a с файла /home/guest/dirl/file1 от
имени суперпользователя командой

chattr -a /home/guest/dir1/file1

Повторите операции, которые вам ранее не удавалось выполнить. Ваши
наблюдения занесите в отчёт. (рис. -@fig:004)

![Выполниение регистрации пользователя guest2](https://github.com/zikarimov/os-intro/blob/master/lab04/image/Screenshot_3.png?raw=true){ #fig:004 width=70% }

Теперь нам нужно повторить операции, которые ранее не удалось сделать.

Выполните дозапись в файл file1 слова «test» командой

echo "test" /home/guest/dir1/file1

После этого выполните чтение файла file1 командой

cat /home/guest/dir1/file1

Убедитесь, что слово test было успешно записано в file1.

Попробуйте удалить файл file1 либо стереть имеющуюся в нём информацию командой

echo "abcd" > /home/guest/dirl/file1

Попробуйте переименовать файл.

Попробуйте с помощью команды

chmod 000 file1

установить на файл file1 права, например, запрещающие чтение и запись для владельца файла. Удалось ли вам успешно выполнить указанные команды? (рис. -@fig:005)

![Выполниение регистрации пользователя guest2](https://github.com/zikarimov/os-intro/blob/master/lab04/image/Screenshot_4.png?raw=true){ #fig:005 width=70% }

10. Повторите ваши действия по шагам, заменив атрибут «a» атрибутом «i».
Удалось ли вам дозаписать информацию в файл? Ваши наблюдения занесите в отчёт

10.1 Установите командой

chmod 600 file1

на файл file1 права, разрешающие чтение и запись для владельца файла.

10.2 Попробуйте установить расширенный атрибут a на файл /home/guest/dir1/file от имени суперпользователя:

chattr +i /home/guest/dir1/file (рис. -@fig:006)

![Выполниение регистрации пользователя guest2](https://github.com/zikarimov/os-intro/blob/master/lab04/image/Screenshot_5.png?raw=true){ #fig:006 width=70% }

10.3 От пользователя guest проверьте правильность установления атрибута:

lsattr /home/guest/dir1/file

10.4 Выполните дозапись в файл file слова «test» командой

echo "test2" /home/guest/dir1/file

После этого выполните чтение файла file командой

cat /home/guest/dir1/file

10.5 Попробуйте удалить файл file1 либо стереть имеющуюся в нём информацию командой

echo "abcdefg" > /home/guest/dirl/file

Попробуйте переименовать файл.

10.6 Попробуйте с помощью команды

chmod 000 file1

установить на файл file1 права, например, запрещающие чтение и запись для владельца файла. (рис. -@fig:007)

![Выполниение регистрации пользователя guest2](https://github.com/zikarimov/os-intro/blob/master/lab04/image/Screenshot_7.png?raw=true){ #fig:007 width=70% }

10.7 Снимите расширенный атрибут i с файла /home/guest/dirl/file1 от
имени суперпользователя командой

chattr -i /home/guest/dir1/file1 (рис. -@fig:008)

![Выполниение регистрации пользователя guest2](https://github.com/zikarimov/os-intro/blob/master/lab04/image/Screenshot_6.png?raw=true){ #fig:008 width=70% }

# Выводы

Получили практические навыкы работы в консоли с расширенными
атрибутами файлов.
