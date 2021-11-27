---
# Front matter
lang: ru-RU
title: "Отчет по лабораторной работе №6"
subtitle: "Мандатное разграничение прав в Linux"
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

Развить навыки администрирования ОС Linux. Получить первое практическое знакомство с технологией SELinux.

Проверить работу SELinx на практике совместно с веб-сервером
Apache.

# Последовательность выполнения работы

1. Войдите в систему с полученными учётными данными и убедитесь, что SELinux работает в режиме enforcing политики targeted с помощью команд getenforce и sestatus (рис. -@fig:001)

![SELinux](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_1.png?raw=true){ #fig:001 width=70% }

2. Обратитесь с помощью браузера к веб-серверу, запущенному на вашем
компьютере, и убедитесь, что последний работает:

service httpd status

или

/etc/rc.d/init.d/httpd status

Если не работает, запустите его так же, но с параметром start. (рис. -@fig:002)

![Apache HTTP Server](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_2.png?raw=true){ #fig:002 width=70% }

3. Найдите веб-сервер Apache в списке процессов, определите его контекст
безопасности и занесите эту информацию в отчёт. Например, можно использовать команду

ps auxZ | grep httpd

или

ps -eZ | grep httpd  (рис. -@fig:003)

![Apache в списке процессов](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_3.png?raw=true){ #fig:003 width=70% }

4. Посмотрите текущее состояние переключателей SELinux для Apache с помощью команды

sestatus -b | grep httpd

Обратите внимание, что многие из них находятся в положении «off». (рис. -@fig:004)

![Текущее состояние переключателей SELinux для Apache](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_4.png?raw=true){ #fig:004 width=70% }

5. Посмотрите статистику по политике с помощью команды seinfo, также определите множество пользователей, ролей, типов. (рис. -@fig:005)

![Статистику по политике](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_5.png?raw=true){ #fig:005 width=70% }

Множество типов: 4793.
Множество пользователей: 8.
Множество ролей: 14.

6. Определите тип файлов и поддиректорий, находящихся в директории /var/www, с помощью команды (рис. -@fig:006)

ls -lZ /var/www

![Определение типов файлов и поддиректорий](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_6.png?raw=true){ #fig:006 width=70% }


7. Определите тип файлов, находящихся в директории /var/www/html:

ls -lZ /var/www/html (рис. -@fig:007)

8. Определите круг пользователей, которым разрешено создание файлов в
директории /var/www/html.

![Определение типов файлов и поддиректорий](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_7.png?raw=true){ #fig:007 width=70% }

9. Создайте от имени суперпользователя (так как в дистрибутиве после установки только ему разрешена запись в директорию) html-файл /var/www/html/test.html следующего содержания: (рис. -@fig:008)

<html>
<body>test</body>
</html>

![Файл test.html](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_8.png?raw=true){ #fig:008 width=70% }

10. Проверьте контекст созданного вами файла. Занесите в отчёт контекст, присваиваемый по умолчанию вновь созданным файлам в директории

/var/www/html (рис. -@fig:009)

![Контекст файла](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_9.png?raw=true){ #fig:009 width=70% }

11. Обратитесь к файлу через веб-сервер, введя в браузере адрес http://127.0.0.1/test.html. Убедитесь, что файл был успешно отображён. (рис. -@fig:010)

![Обращение к файлу через браузер](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_10.png?raw=true){ #fig:010 width=70% }

12. Изучите справку man httpd_selinux и выясните, какие контексты файлов определены для httpd. Сопоставьте их с типом файла test.html. Проверить контекст файла можно командой ls -Z.

ls -Z /var/www/html/test.html

Рассмотрим полученный контекст детально. Обратите внимание, что так как по умолчанию пользователи CentOS являются свободными от типа (unconfined в переводе с англ. означает свободный), созданному нами файлу test.html был сопоставлен SELinux, пользователь unconfined_u. Это первая часть контекста.
Далее политика ролевого разделения доступа RBAC используется процессами, но не файлами, поэтому роли не имеют никакого значения для файлов. Роль object_r используется по умолчанию для файлов на «постоянных» носителях и на сетевых файловых системах. (В директории /ргос файлы, относящиеся к процессам, могут иметь роль system_r. Если активна политика MLS, то могут использоваться и другие роли, например, secadm_r. Данный случай мы рассматривать не будем, как и
предназначение :s0).

Тип httpd_sys_content_t позволяет процессу httpd получить доступ к файлу. Благодаря наличию последнего типа мы получили доступ к файлу при обращении к нему через браузер.

13. Измените контекст файла /var/www/html/test.html с httpd_sys_content_t на любой другой, к которому процесс httpd не должен иметь доступа, например, на samba_share_t: (рис. -@fig:011)

chcon -t samba_share_t /var/www/html/test.html

ls -Z /var/www/html/test.html

После этого проверьте, что контекст поменялся

![Изменение контекста файла](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_11.png?raw=true){ #fig:011 width=70% }

14. Попробуйте ещё раз получить доступ к файлу через веб-сервер, введя в браузере адрес http://127.0.0.1/test.html. Вы должны получить сообщение об ошибке: (рис. -@fig:012)

Forbidden

You don't have permission to access /test.html on this server.

![Обращение к файлу через браузер](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_12.png?raw=true){ #fig:012 width=70% }

15. Проанализируйте ситуацию. Почему файл не был отображён, если права доступа позволяют читать этот файл любому пользователю? (рис. -@fig:013) (рис. -@fig:014)

ls -l /var/www/html/test.html

Просмотрите log-файлы веб-сервера Apache. Также просмотрите системный лог-файл:

tail /var/log/messages

Если в системе окажутся запущенными процессы setroubleshootd и audtd, то вы также сможете увидеть ошибки, аналогичные указанным выше, в файле /var/log/audit/audit.log. Проверьте это утверждение самостоятельно.

![Права доступа](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_13.png?raw=true){ #fig:013 width=70% }

![log-файлы веб-сервера Apache](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_14.png?raw=true){ #fig:014 width=70% }

16. Попробуйте запустить веб-сервер Apache на прослушивание ТСР-порта 81 (а не 80, как рекомендует IANA и прописано в /etc/services). Для этого в файле /etc/httpd/httpd.conf найдите строчку Listen 80 и замените её на Listen 81. (рис. -@fig:015)

![ТСР-порт 81](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_15.png?raw=true){ #fig:015 width=70% }

17. Выполните перезапуск веб-сервера Apache. Произошёл сбой? Поясните
почему? (рис. -@fig:016)

![Перезапуск веб-сервера Apache](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_16.png?raw=true){ #fig:016 width=70% }

Никакого сбоя не произошло.

18. Проанализируйте лог-файлы: (рис. -@fig:017)

![log-файлы веб-сервера Apache](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_17.png?raw=true){ #fig:017 width=70% }

19. Выполните команду

semanage port -a -t http_port_t -р tcp 81

После этого проверьте список портов командой

semanage port -l | grep http_port_t

Убедитесь, что порт 81 появился в списке. (рис. -@fig:018)

![Проверка порта](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_18.png?raw=true){ #fig:018 width=70% }

20. Попробуйте запустить веб-сервер Apache ещё раз. Поняли ли вы, почему
он сейчас запустился, а в предыдущем случае не смог? (рис. -@fig:019)

![Презапуск веб-сервера Apache](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_19.png?raw=true){ #fig:019 width=70% }

21. Верните контекст httpd_sys_cоntent__t к файлу /var/www/html/ test.html: (рис. -@fig:020)

chcon -t httpd_sys_content_t /var/www/html/test.html

После этого попробуйте получить доступ к файлу через веб-сервер, введя в браузере адрес http://127.0.0.1:81/test.html.

Вы должны увидеть содержимое файла — слово «test». (рис. -@fig:021)

![Изменение контекста](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_20.png?raw=true){ #fig:020 width=70% }

![Обращение к файлу через браузер](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_21.png?raw=true){ #fig:021 width=70% }

22. Исправьте обратно конфигурационный файл apache, вернув Listen 80. (рис. -@fig:022)

![TCP-порт 80](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_22.png?raw=true){ #fig:022 width=70% }

23. Удалите привязку http_port_t к 81 порту:

semanage port -d -t http_port_t -p tcp 81

и проверьте, что порт 81 удалён. (рис. -@fig:023) (рис. -@fig:024)

![Удаление TCP-порта 81](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_23.png?raw=true){ #fig:023 width=70% }

![Удаление TCP-порта 81](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_24.png?raw=true){ #fig:024 width=70% }

24. Удалите файл /var/www/html/test.html:

rm /var/www/html/test.html (рис. -@fig:025)

![Удаление файла](https://github.com/zikarimov/os-intro/blob/master/lab06/image/Screenshot_25.png?raw=true){ #fig:025 width=70% }

# Выводы

Развил навыки администрирования ОС Linux. Получил первое практическое знакомство с технологией SELinux.

Проверил работу SELinx на практике совместно с веб-сервером
Apache.
