---
# Front matter
lang: ru-RU
title: "Отчет по лабораторной работе №5"
subtitle: "Дискреционное разграничение прав в Linux. Исследование влияния дополнительных атрибутов"
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

Изучение механизмов изменения идентификаторов, применения SetUID- и Sticky-битов. Получение практических навыков работы в консоли с дополнительными атрибутами. Рассмотрение работы механизма смены идентификатора процессов пользователей, а также влияние бита Sticky на запись и удаление файлов.

# Последовательность выполнения работы

##  Создание программы

Для начала нам следовало установить компилятор gcc. (рис. -@fig:001)

![Компилятор gcc](https://github.com/zikarimov/os-intro/blob/master/lab05/image/1.jpg?raw=true){ #fig:001 width=70% }

Чтобы защита SELinux не мешала выполнению заданий работы, мы отключили ее. (рис. -@fig:002)

![Отключение защиты](https://github.com/zikarimov/os-intro/blob/master/lab05/image/2.jpg?raw=true){ #fig:002 width=70% }


1. Войдите в систему от имени пользователя guest.

2. Создайте программу simpleid.c: (рис. -@fig:003) (рис. -@fig:004)

![Программа simpleid.c](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_2.png?raw=true){ #fig:003 width=70% }

![Программа simpleid.c](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_1.png?raw=true){ #fig:004 width=70% }

3. Скомплилируйте программу и убедитесь, что файл программы создан:

gcc simpleid.c -o simpleid

4. Выполните программу simpleid:

./simpleid

5. Выполните системную программу id:

id

и сравните полученный вами результат с данными предыдущего пункта задания. (рис. -@fig:005)

![Компиляция и выполнения программы](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_3.png?raw=true){ #fig:005 width=70% }

6. Усложните программу, добавив вывод действительных идентификаторов: (рис. -@fig:006) (рис. -@fig:007)

![Программа simpleid2.c](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_5.png?raw=true){ #fig:006 width=70% }

![Программа simpleid2.c](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_4.png?raw=true){ #fig:007 width=70% }

7. Скомпилируйте и запустите simpleid2.c:

gcc simpleid2.c -o simpleid2

./simpleid2 (рис. -@fig:008)

![Компиляция и выполнения программы](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_6.png?raw=true){ #fig:008 width=70% }

8. От имени суперпользователя выполните команды:

chown root:guest /home/guest/simpleid2

chmod u+s /home/guest/simpleid2 (рис. -@fig:009)

![Смена пользователя и установка SetU’D-бита](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_7.png?raw=true){ #fig:009 width=70% }

9. Используйте sudo или повысьте временно свои права с помощью su. Поясните, что делают эти команды.

Команда sudo позволяет пользователям выполнять указанные программы с административными привилегиями без ввода пароля суперпользователя root.

10. Выполните проверку правильности установки новых атрибутов и смены владельца файла simpleid2:

ls -l simpleid2

11. Запустите simpleid2 и id:

./simpleid2

id

Сравните результаты. (рис. -@fig:010)

![Проверка правильности установки новых атрибутов](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_8.png?raw=true){ #fig:010 width=70% }

12. Проделайте тоже самое относительно SetGID-бита. (рис. -@fig:011) (рис. -@fig:012)

![Проверка правильности установки новых атрибутов](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_9.png?raw=true){ #fig:011 width=70% }

![Проверка правильности установки новых атрибутов](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_10.png?raw=true){ #fig:012 width=70% }

13. . Создайте программу readfile.c: (рис. -@fig:013)

![Программа readfile.c](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_11.png?raw=true){ #fig:013 width=70% }

14. Откомпилируйте её.

gcc readfile.c -o readfile (рис. -@fig:014)

![Программа readfile](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_12.png?raw=true){ #fig:014 width=70% }

15. Смените владельца у файла readfile.c (или любого другого текстового файла в системе) и измените права так, чтобы только суперпользователь (root) мог прочитать его, a guest не мог (рис. -@fig:015)

![Смена владельца и изменения прав](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_13.png?raw=true){ #fig:015 width=70% }

16. Проверьте, что пользователь guest не может прочитать файл readfile.c. (рис. -@fig:016)

![Проверка на правильность](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_14.png?raw=true){ #fig:016 width=70% }

17. Смените у программы readfile владельца и установите SetU’D-бит. (рис. -@fig:017)

![Смена пользователя и установка SetU’D-бита](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_15.png?raw=true){ #fig:017 width=70% }

18. Проверьте, может ли программа readfile прочитать файл readfile.c? (рис. -@fig:018) (рис. -@fig:019)

![Проверка на правильность](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_16.png?raw=true){ #fig:018 width=70% }

![Чтения файла](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_17.png?raw=true){ #fig:019 width=70% }

19. Проверьте, может ли программа readfile прочитать файл /etc/shadow?

Отразите полученный результат и ваши объяснения в отчёте.  (рис. -@fig:020)

![Чтения файла](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_18.png?raw=true){ #fig:020 width=70% }

## Исследование Sticky-бита

1. Выясните, установлен ли атрибут Sticky на директории /tmp, для чего выполните команду

ls -l / | grep tmp

2. От имени пользователя guest создайте файл file01.txt в директории /tmp со словом test:

echo "test" > /tmp/file01.txt

3. Просмотрите атрибуты у только что созданного файла и разрешите чтение и
запись для категории пользователей «все остальные»:

ls -l /tmp/file01.txt

chmod o+rw /tmp/file01.txt

ls -l /tmp/file01.txt (рис. -@fig:021)

![Просмотр атрибутов и разрешения прав](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_19.png?raw=true){ #fig:021 width=70% }

4. От пользователя guest2 (не являющегося владельцем) попробуйте прочитать файл /tmp/file01.txt:

cat /tmp/file01.txt

5. От пользователя guest2 попробуйте дозаписать в файл /tmp/file01.txt слово test2 командой

echo "test2" > /tmp/file01.txt

Удалось ли вам выполнить операцию? Да, удалось.

6. Проверьте содержимое файла командой

cat /tmp/file01.txt

7. От пользователя guest2 попробуйте записать в файл /tmp/file01.txt слово test3, стерев при этом всю имеющуюся в файле информацию командой

echo "test3" > /tmp/file01.txt

Удалось ли вам выполнить операцию? Да, удалось выполнить операцию.

8. Проверьте содержимое файла командой

cat /tmp/file01.txt

9. От пользователя guest2 попробуйте удалить файл /tmp/file01.txt командой

rm /tmp/fileOl.txt

Удалось ли вам удалить файл? Нет, не удалось удалить файл. (рис. -@fig:022)

![Просмотр атрибутов и разрешения прав](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_20.png?raw=true){ #fig:022 width=70% }

10. Повысьте свои права до суперпользователя следующей командой

su -

и выполните после этого команду, снимающую атрибут t (Sticky-бит) с директории /tmp:

chmod -t /tmp (рис. -@fig:023)

![Просмотр атрибутов и разрешения прав](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_21.png?raw=true){ #fig:023 width=70% }

11. Покиньте режим суперпользователя командой

exit

12. От пользователя guest2 проверьте, что атрибута t у директории /tmp нет:

ls -l / | grep tmp (рис. -@fig:024)

![Просмотр атрибутов и разрешения прав](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_22.png?raw=true){ #fig:024 width=70% }

13. Повторите предыдущие шаги. Какие наблюдаются изменения?

14. Удалось ли вам удалить файл от имени пользователя, не являющегося его владельцем? Ваши наблюдения занесите в отчёт. (рис. -@fig:025)

![Просмотр атрибутов и разрешения прав](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_23.png?raw=true){ #fig:025 width=70% }

Да, удалось удалить файл от имени пользователя, не являющегося его владельцем.

15. Повысьте свои права до суперпользователя и верните атрибут t на директорию /tmp:

su -

chmod +t /tmp

exit (рис. -@fig:026)

![Просмотр атрибутов и разрешения прав](https://github.com/zikarimov/os-intro/blob/master/lab05/image/Screenshot_24.png?raw=true){ #fig:026 width=70% }

# Выводы

Изучил механизмы изменения идентификаторов, примененив SetUID- и Sticky-биты. Получил практические навыкы работы в консоли с дополнительными атрибутами. Рассмотрел работы механизмов смены идентификаторов процесса пользователей, а также влияние бита Sticky на запись и удаление файлов.
