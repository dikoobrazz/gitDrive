## Video programming
 **[Сергей Туленцев NoSQL (Not only SQL)](http://www.url.com)**    
 **[Про криптографию Владимир Иванов](https://www.youtube.com/watch?v=yrOKSZ6CxtU)**    
 **[Сетвеые технологии Владимир Иванов](https://www.youtube.com/watch?v=x9z2uoyPd6g)**    
 **[Олег Бунин высоконагруженные системы](https://www.youtube.com/watch?v=KmIE5K6adus﻿)**

## Ruby
  **Frameworks**
  - Sinatra (kind express, flask)
  - Padrino (kind django) no progress
  - Hanami (new, 2-3 year)
  - RoR
  - Grape (from API)
  - Jets (lambda servlets)

## Django
### Расширение в шаблонах

   ```html
   {% block title %}  {{ block.super }} - Контакты  {% endblock title %}
   ``` 

### Подсветка текущего пункта меню в шаблоне HTML  
   
   ```html
    {% url 'home' as home %}
    {% url 'about' as about %}
    <li {% if request.path == home %} class="active" {% endif %} ></li>
    <li {% if request.path == about %} class="active" {% endif %} ></li>
   ```

### БД заполнение через shell (json)  
   **Файл posts.json**

  ```json
    [
      {
        "title": "My Updated Post",
        "content": "My first updated post!\r\n\r\nThis is exciiting!",
        "user_id": 1
      },
      ...
    ]
  ```

  **python shell:**

  ```bash
  import json
  from blog.models import Post
  with open('posts.json') as f:
    posts_json = json.load(f)    

  for post in posts_json:
    post = Post(title=post['title'], content=post['content'], author_id=['user_id'])  
    post.save()   

  exit()    
  ```

### Выборка уникальных значений из объекта БД    
  **views.py**  
  выборка уникальных записей по полю **title** из **products**  

  ```py
  unique = list({item.title: item for item in products}.values())
  ```

## Python  
### Запуск ботов на удаленном сервере    
  Создайте новый экран и прикрепите к нему:
   
  ```bash
   $ screen -S mybot
  ```
   
  **Запустите бот (замените python на python3, если вы используете Python 3):**
   
  ```bash
   $ python bot.py
  ```
   
   Отсоедините от экрана, удерживая CTRL и нажав A, затем D.  
   Теперь вы можете отключиться от сервера, набрав exit, если хотите.  

   **Чтобы снова подключиться к экрану после входа в систему:**  

  ```bash
   $ screen -r mybot  
  ```
   
   **[Использование - link](https://ruhighload.com/%25D0%2597%25D0%25B0%25D0%25BF%25D1%2583%25D1%2581%25D0%25BA+%25D0%25BF%25D1%2580%25D0%25BE%25D1%2586%25D0%25B5%25D1%2581%25D1%2581%25D0%25BE%25D0%25B2+%25D0%25B2+supervisor)**    
   
   **Минимальный конф:**

   > [program:worker]  
   > command=python /root/test.py  
   > stdout_logfile=/var/log/worker.log  
   > autostart=true  
   > autorestart=true  
   > user=root  
   > stopsignal=KILL  
   > numprocs=1   


   Если используются относительные пути в системе, то обязательно используйте параметр **directory**.  
   По умолчанию скрипт запускается из **/**.  

#### Telegram BOT pyTelegramBotAPI  
  **Зацикливание бота и обработка отключения сервера**

  ```python
  while True:  
      try:  
          bot.polling(none_stop=True)  
      except Exception as e:  
          logger.error(e)   
          time.sleep(15)  
  ```
    
## JavaScript     
### vue cli install    
   
  ```bash
   npm install -g @vue/cli    
  ```

### Изучаем JavaScript 2019     
  **[Портал Ильи Кантора Learn JavaScript](http://learn.javascript.ru/)**  
  **[Задачи по программированию - Codewars](https://www.codewars.com/)**  
  **[Серия книг по JavaScript на русском языке](https://github.com/azat-io/you-dont-know-js-ru)**  
  **[Книга «Exploring ES6» на английском](https://exploringjs.com/es6/)**  
  **[Большой справочник по JavaScript от MDN](https://developer.mozilla.org/ru/)**  
  **[Книга «Грокаем алгоритмы» на русском языке](https://github.com/mduisenov/GrokkingAlgorithms)**  
  **[Гарвардский курс «CS50» видео Youtube на русском](https://www.youtube.com/watch?v=Sy_wba7l1UU&list=PLawfWYMUziZqyUL5QDLVbe3j5BKWj42E5)**  

## Linux
### import key

   **Импортируем ключ для приложения**

   ```bash
   gpg --recv-keys DBD2CE893E2D1C87
   ```

### ipv6 disable
   
   **Убираем ipv6**

   ~/usr/lib/sysctl.d/50-default.conf~
   ~/etc/sysctl.conf~
   
   ```script
   в конец файла добавляем:  
   net.ipv6.conf.all.disable_ipv6 = 1  
   net.ipv6.conf.default.disable_ipv6 = 1  
   net.ipv6.conf.lo.disable_ipv6 = 1  
   net.ipv6.conf.tun0.disable_ipv6 = 1
   ```

   ```bash
   $ sudo sysctl -p
   ```

   **или**

   ```bash
   $ sudo gedit /etc/default/grub
   ```

   >GRUB_CMDLINE_LINUX="ipv6.disable=1"

   ```bash
   $ sudo update-grub2
   ```

### DOKER start

   ```bash
   $ sudo systemctl start docker.service
   ```

### Baloo
   
   **Отключение Baloo (KDE)**  
   _индексация файлов_

   ~/.kde4/share/config/baloofilerc

   ```bash
   [Basic Settings]
   Indexing-Enabled=false
   ```

### iso to Flash

   **Запись образа на флеш накопитель**

   Проверяем имя флешки в системе

   ```bash
   $ sudo fdisk -l
   ```

   Запись на флеш накопитель через терминал

   ```bash
   $ sudo dd bs=4M if=/path/to/image.iso of=/dev/sdX status=progress && sync
   ```

### Locale settings

   **Установка локали**

   ```bash
   $ sudo nano /etc/locale.gen
   ```
   
  > расскоментировать -> ru_RU.UTF-8
  > -> en_US.UTF-8

   ```bash
   $ sudo nano /etc/locale.conf
   ```

   ```script
   добавить:
   LANG=ru_RU.UTF-8
   LANG=en_US.UTF-8
   ```

   **по желанию**

   ```bash
   $ sudo mkinitcpio -p linux (для Arch Linux)
   ```

   **Если в оболочке KDE язык системы не изменился удалить файлы:**

   ~/.config/plasma-localerc
   ~/.config/plasma-locale-settings.sh

### NOT start X

   **Не стратуют иксы**

   В загрузочном меню grub выбираем нужный пункт и нажимаем "e"
   
   в строку с ~quiet~ пишем:

   > * nomodeset
   > * nouveau.modeset=0
   > * i915.modeset=1
   > * radeon.modeset=0
   > * nvidia.modeset=0
   > * modprobe.blacklist=nouveau

   acpi_osi=! acpi_osi="Windows 2009" **для ноутбуков MSI**  
   acpi_osi=! acpi_osi="Windows 2015" **для др ноутбуков**

   **Если добавляем запись непосредственно в grub.cfg**

   acpi_osi=! acpi_osi=\"Windows 2009\"  **экранируем кавычки**
   
   **Reload GRUB2**

   ```bash
   $ sudo grub mkconfig -o /boot/grub/grub.cfg
   ```

### Teamviewer start

   **Запуск Teamviewer**
   Перед запуском приложения
   
   ```bash
   $ sudo teamviewer --daemon enable
   ```

### Addiction remove
   
   **Удаление приложения с его зависимостями**

   ```bash
   $ sudo pacman -Rscn packagename
   ```

   **Вывод зависимостей для пакета (т.е. какие пакеты зависят от данного пакета)**

   ```bash
   $ sudo pacman -Qi packagename
   ```

### Steam

   **Запуск игр в Steam через primusrun**

   В меню "параметры запуска" пишем несколько вариантов:

   > 1. primusrun %command% (60 fps)
   > 2. vblank_mode=0 primusrun %command% (80 fps)  
   > 3. vblank_mode=0 optirun -b primus %command% (80 fps)
   
   **На страх и риск можно повысить fps настройками в файле:**

   _/usr/bin/primusrun_

   ```bash
   в строку:
   # export PRIMUS_SYNC=" from ${PRIMUS_SYNC:-0}
   расскоментировать и поменять на:
   export PRIMUS_SYNC=" from ${PRIMUS_SYNC:-1}
   ```

### DNS Crypt
   
   **Запуск dnscrypt**

   ```bash
   $ systemctl enable dnscrypt-proxy.service
   $ systemctl start dnscrypt-proxy.service
   ```
 
### Grub update

   **Обновление конфигурации загрузчика GRUB2**

   ```bash
   $ sudo grub-mkconfig -o /boot/grub/grub.cfg
   ```

### QEMU 

   **Перед запуском virt-manager (Arch Linux)**

   ```bash
   $ systemctl start libvirtd
   $ systemctl enable libvirtd
   ```

### Keyboard layout

   **Установка расскладки клавиатуры**

   ```bash
   $ sudo -i
   $ localectl set-x11-keymap us,ru pc104 "" grp:alt_shift_toggle
   ```
 
### Screen settings

   **Установка разрешения экрана при загрузке системы**

   _/etc/default/grub_
   > GRUB_GFXPAYLOAD_LINUX="1920x1080x32"

   **Перезагрузка GRUB**

   ```bash
   $ sudo grub-mkconfig -o /boot/grub/grub.cfg
   ```
### Wget settings

   **Настройка wget**
   
   команда в консоли:

   ```bash
   $ wget -r -k -l 10 -p -E -nc http://site.com/
   ```
   
   настройка конфигурационного файла:

   ```bash
   $ sudo nano /etc/wgetrc
   ```

   **Скачать файл через прокси http:**
   _в файле:_
   > http_proxy="http://33.22.44.44:8080"
   _в консоли:_

   ```bash
   $ wget http://www.google.com/favicon.ico
   ```

   **Скачать файл через прокси https:**
   _в файле:_
   > https_proxy="http://33.22.44.44:8080"
   _в консоли:_
   
   ```bash
   $ wget https://www.google.com/favicon.ico
   ```

   **Использовать proxy с авторизацией**

   _в файле:_
   > http_proxy="http://33.22.44.44:8080"
   _в консоли:_

   ```bash
   $ wget -proxy-user=user -proxy-password=password http://www.google.com/favicon.ico
   ```

### System errors

   **Просмотр ошибок после загрузки системы**

   ```bash
   $ sudo systemctl --failed
   $ sudo systemctl status systemd-modules-load
   ```

### Run files in console

   **Запуск программ из консоли без привязки к ней**

   ```bash
   $ nohup programname > /dev/null &
   ```

### WI-FI marine

   **[Сайт с информацией по установке:](http://ubuntovod.ru/instructions/fix-wi-fi-ubuntu-12-10.html)**
   
   **Обновить систему**

   ```bash
   $ sudo apt update && sudo apt upgrate
   ```

   **Перезагрузка, далее:**

   ```bash
   $ sudo apt install linux linux-headers-generic kernel-package
   $ sudo apt install --reinstall bcmwl* firmware-b43-lpphy-installer b43-fwcutter
   ```

   **Перезагрузка**

   Если после перезагрузки Wi-Fi так и не ожил - попробуйте эти команды:

   ```bash
   $ sudo apt remove bcmwl-kernel-sourcesudo
   $ sudo apt install firmware-b43-installer b43-fwcutter
   ```

   **И вновь перезагрузите компьютер. Должно помочь.**

### Postgres DB

   **Установка, настройка, запуск базы**
   
   ```bash
   $ su
   enter pass..
   $ su postgres
   $ initdb --locale en_GB.UTF-8 -E UTF8 -D '/var/lib/postgres/data'
   $ exit
   $ exit
   ```

   **Запускаем Postgres**

   ```bash
   $ sudo systemctl start postgresql
   ```

   **Проверяем запуск базы**

   ```bash
   $ systemctl status postgresql
   ```

   **Добавляем в автозагрузку**

   ```bash
   $ systemctl enable postgresql
   ```

   **Вход в DB**

   ```bash
   $ sudo -u postgres psql
   ```

   **Создание новой DB**

   ```bash
   $ create database testdb;
   ```

   **Просмотр списка баз**

   ```bash
   $ \l
   ```

   **Коннект к созданной DB**

   ```bash
   $ \c testdb
   ```

   **Создаем схему**

   ```bash
   $ create schema testdbschema
   ```

   **Создаем таблицу**

   ```bash
   $ create table testdbschema.table1 (id integer, password CHAR(10))
   ```

### Deepin DE color restart

   **Если не меняется тема рабочего стола**

   ```bash
   $ gsettings set com.deepin.wrap.gnome.metacity compositing-manager true
   ```

   [github issues link](https://github.com/linuxdeepin/developer-center/issues/316%0A)

### Git, Github

   **Инициализация**

   ```bash
   $ git init
   ```

   **Добавление файлов в репозиторий**

   ```bash
   $ git add main.py
   ```

   **Массовое добавление файлов в репозиторий**

   ```bash
   $ git add .
   ```

   **Добавление коммита**

   ```bash
   $ git commit -m "Initial commit"
   ```

   **Добавление облачного репозитория GitHub**

   ```bash
   $ git remote add origin https://github.com/dikoobrazz/test_project.git
   ```

   **Заливаем в облако GitHub**

   ```bash
   $ git push -u origin master
   ```

   **Отслеживаем изменения**

   ```bash
   $ git status   
   $ git diff
   ```

   **Комманды после сделанных изменений**

   ```bash
   $ git add .  
   $ git commit -m "second commit"  
   $ git push -u origin master  
   $ git status
   ```

   **РЕАЛИЗАЦИЯ ВЕТОК**

   **Проверка веток**

   ```bash
   $ git branch
   ```

   **Создание и переключение на новую ветку**
   
   ```bash
   $ git checkout -b feature1
   ```

   **Создаем нужные нам файлы добавляем в репозиторий и коммитим**

   ```bash
   $ touch 3 main2.py && git add . && git commit -m "Feature1 Commit1"
   ```

   **Просмотр веток и коммитов**

   ```bash
   $ git log --graph
   ```

   **Переключение на другую (master) ветку**

   ```bash
   $ git checkout master
   ```

   **Первый способ** слияние веток.  Автоматически создается merge коммит

   ```bash
   $ (master) git merge featurel  
   $ git log --graph
   ```

   **Второй способ** слияние веток. Исория коммитов линейная

   ```bash
   $ (featurel) git rebase master  
   $ git checkout master  
   $ git log --graph  
   $ git merge featurel
   ```

   **Третий способ.** rebase + merge commit

   ```bash
   $ (featurel) git rebase master  
   $ git checkout master  
   $ git merge --no-ff featurel  
   $ git log --graph
   ```

   **Вытягивание всего что появилось в удаленном репозитории, и нет на локалке**

   ```bash
   $ git pull origin
   ```
   
   **или**

   ```bash
   $ git pull --rebase origin
   ```

### Bash commands

   **Bash commands**

   **touchi** - создать файл

   **mkdir** - создать папку

   **mkdir dir/subdir** - создаст все папки в цепочке
   
   **mv subdir dir** - перемещение папки subdir со всем содержимым в папку dir

   **mv subdir/ dir** - перемещение всего из папки subdir в папку dir

   **rm file** - удаление файла

   **rm -rf dir** - удаление папки со всем содеримым (ОПАСНО! Быть аккуратнее)

   **cati** - вывод в вконсоль содержимого всего файла

   **head** - вывод 10-ти первых строк содержимого файла

   **tail** - вывод 10-ти последних строк содержимого файла

   **tail -f system.log** - постоянный вывод последних 10 сообщений в файле

   **grep 'Apr 27’ system.log** - выведет все строки с заданным содержимым из файла system.log

   **grep Mac system.log** - выведет все строки с “Mac” из файла system.log

   **Пэйджеры** - программы которые открывают и выводят в консоль содержимое файлов частями, то что помещается на экран
   
   • more

   • less - боее продвинутый, попадаем в режим vim’а
     
   > * q - выход
   > * h - справка
   > * ctrl + f - перемещение постранично вперед
   > * ctrl + b - перемещение постранично назад
   > * G - переместтиться в начало файла
   > * /char - поиск слова char в файле. n , shift + n - премещение по найденным вперед назад;

   **man** - справка
   
   **man man** - справка по справке
   
   **man mkdir** - справка по команде mkdir
   
   **man -f mkdir** - вывод всех категорий где встречается mkdir

   **which ls** - which показывает где лежит программа

   **env** - Просмотр списка переменных окружения

   **PATH=/var/tmp:$PATH** - добавляем папку в переменную PATH. Теперь если в папке tmp/ лежит скрипт, его можно запустить из любого места в консоли. Теперь оболочка будет заглядывать и по адресу /var/tmp. Работает только в рамках текущей сессии;

   **ls > outputLs** - перенаправления потока вывода не на экран, а в файл

   **sort < unsorted** - отсортированный (sort) вывод на экран(<) из файла(unsorted)
   
   **sort < unsorted > sorted** - вывести отсоритрованный(sort) файл(unsorted) и записать во новь созданный файл(sorted)

   /Использование конвеера/ ( | )

   **cat unsorted | sort** - ввыведет отсорированный файл unsorted на экран

   **cat unsorted | sort | uniq** - ~//~ + если есть повторения в фйле, выведет в одном экземплре(uniq)
   
   **ls | grep test** - выведет на экран все файлы и папки с названием test

   **history** - вывод истории терминала .bash_history

   **!524** - повтор (вызов) команды из списка истории, 524 - номер команды в истории
   
   **!cat** - первая встретившаяся сконца списка команда, содержащая cat
   
   **ctrl +r + "history"** - инкрементальный поиск команд в истории. Если найденная команда не та, нажимаем ctrl + r

   **Alias** (псевдонимы для команд)
   
   **alias** - вывод списка алиасов утановленных в системе
   
   **alias ll='ls -la'** - назначаем алиас ll, ll исполняет ls -la
   
   **unalias ll** - удаление алиаса
   
   **type ll** - просмотр описания алиаса

### Virtualbox settings #arch linux
  
   **Настройка сети на виртуальной машине**
    
   **На virtualbox**

   _Сеть -> Адаптер -> добавить новый (редактируем)_
    
   > * vboxnet ->
   > * IPv4 адрес - 192.168.100.1
   > * IPv4 маска подсети 255.255.255.0     

   **НАСТРОЙКИ виртуальной машины**

   /Сеть/
    
   > * Адапртер1
   > * Виртуальный адаптер хоста → ☑vboxnet0
   > * Дополнительно → ☑Intel PRO/1000 MT Desktop(82540EM)
   > * Кабель подключен → ☑      

   > * Адаптер2
   > * NAT
   > * Дополнительно → ☑Intel PRO/1000 MT Desktop(82540EM)
   > * Кабель подключен → ☑     

   **Файл interfaces (в загруженной виртуальной машине)**

   ```bash
   $ sudo nano /etc/network/interfaces
   ``` 

   > * iface eth0 inet static
   > * address 192.168.100.16
   > * netmask 255.255.255.0
   > * auto eth0 
      
   > * iface eth1 inet dhcp
   > * auto eth1    

   **На хост машине добавляемся в группу**

   ```bash
   $ sudo$  gpasswd -a $USER vboxusers
   ``` 

   **Прописываем в файл**

   ```bash
    $ sudo nano /etc/modules-load.d/virtualbox.conf
   ```

   > * vboxdrv
   > * vboxnetadp
   > * vboxnetflt   

   **Расшаривание общей папки**

   ```bash
   $ sudo pacman -S virtualbox-guest-utils
   ```

   **Добавляемся в группу**

   ```bash
    $ sudo gpasswd -a $USER vboxsf
   ``` 

   **В самой виртуальной машине когда загрузится создаем папку vboxshare и в терминале**

   ```bash
    $ sudo mount -t vboxsf -o rw,uid=1000,gid=1000 vboxshare vboxshare
   ```

   **На хост-машине тоже должна быть папка vboxshare**

### Nvidia + Bumblebee #arch linux

   **Установка и настройка Nvidia + Bumblebee**

   ```bash
    $ sudo pacman -Rc xf86-video-nouveau    
    $ yaourt -Syyua    
   ```

   **Далее устанавливаем один из трех вариантов**

   ```bash
    $ sudo pacman -S bumblebee mesa xf86-video-intel nvidia lib32-nvidia-utils lib32-virtualgl nvidia-settings bbswitch
   ``` 

   **или**

   ```bash
    $ sudo pacman -S bumblebee mesa xf86-video-intel nvidia-340xx nvidia-340xx-utils lib32-nvidia-340xx-utils lib32-virtualgl bbswitch
   ```

   **или**

   ```bash
    $ sudo pacman -S bumblebee mesa xf86-video-intel nvidia-304xx nvidia-304xx-utils lib32-nvidia-304xx-utils lib32-virtualgl bbswitch
   ``` 

   **Добавляем пользователя в группы:**

   ```bash
    $ sudo gpasswd -a $USER bumblebee    
    $ sudo gpasswd -a $USER video    
   ```

   **Включаем Bumblebee**

   ```bash
    $ sudo systemctl enable bumblebeed.service
   ``` 

   **Перезагрузка**
   
   ```bash
    $ sudo shutdown -r now
   ``` 

   **Проверка. Если оба off - все нормально**

   ```bash
    $ optirun --status
   ```

  _Bumblebee status: Ready (3.2.1). X inactive. Discrete video card is off._

   ```bash
    $ optirun pwd
   ```

   _/home/just/_

   ```bash
    $ optirun$  --status
   ```

   _Bumblebee status: Ready (3.2.1). X inactive. Discrete video card is off._

   **ЗАПУСК NVIDIA Settings**

   ```bash
    $ optirun -b none nvidia-settings -c :8
   ```

   **Устанавливаем**

   > * primus
   > * lib32-primus     

   **Запуск программ с видеокартой**

   ```bash
    $ primusrun steam
   ```

   **После обновления драйвера Nvidia**

   ```bash
    $ sudo mkinitcpio -P
   ```

### Mmount files with server #arch linux

  **Монтируем файлы с удаленного сервера на локальную машину**
    
  **Устанавливаем**

  ```bash
  $ sudo pacman -S sshfs fuse
  ```

  **Создаем папку для примонтированных файлов**

  ```bash
  $ mkdir /home/username/www
  ```

  **Монтируем файлы**

  ```bash
  $ sudo sshfs username@192.168.100.16:/var/www/html/ /home/username/www/    
  $ username password.....    
  ```

  **Размонтирование файлов с сервера**

  ```bash
  $ sudo umount /home/username/www
  ```

  **или**

  ```bash
  $ fusermount -u /home/username/www
  ```   

### Snapper #OpenSuse

  **Включение выключение автоматичческих снимков**

  **Отключение / включение снимков временной шкалы**

  > * Включение. snapper -c root set-config "TIMELINE_CREATE=yes"
  > * Отключение. snapper -c root set-config "TIMELINE_CREATE=no"
  > * Временные снимки временной шкалы включены по умолчанию, за исключением корневого раздела.     

  **Отключение / включение снимков установки**

  > * Включение: установите пакет snapper-zypp-plugin
  > * Отключение: удаление пакета snapper-zypp-plugin
  > * Установочные снимки включены по умолчанию.    

  **Отключение / включение снимков министрирования**

  > * Включение: установите USE_SNAPPER в yes в /etc/sysconfig/yast2 .
  > * Отключение: установите USE_SNAPPER на no в /etc/sysconfig/yast2 .
  > * По умолчанию моментальные снимки управления включены.    

### Youtube music download   

  **Скачиваем музыку отдельно от видео с youtube**

  ```bash
  $ youtube-dl --extract-audio --audio-format mp3 https://www.youtube.com/watch\?v\=2daUg5ZcFi0
  ```

  **или**

  ```bash
  $ youtube-dl -F http://www.youtube.com/watch?v=HRIF4_WzU1w
  ```

  > * 171         webm      audio only  DASH webm audio , audio@ 48k (worst)     
  > * 140         m4a       audio only  DASH audio , audio@128k    
  > * 160         mp4       192p        DASH video     

  ```bash
  $ youtube-dl -f 140 http://www.youtube.com/watch?v=HRIF4_WzU1w
  ```

  В этом случае формат будет m4a.
  /Можно переименовать в mp3/
    
### Nvidia + Bumblebee #opensuse leap 15

  **Установка и настройка Nvidia + Bumblebee в OpenSuse Leap 15**
   
  ```bash
  sudo zypper ar -f http://download.opensuse.org/repositories/X11:/Bumblebee/openSUSE_Leap_15.0 Bumblebee
  sudo zypper in bumblebee
  sudo usermod -G video,bumblebee insert_your_username_here
  sudo systemctl enable bumblebeed
  sudo systemctl start bumblebeed
  sudo echo "blacklist nouveau" >> /etc/modprobe.d/99-local.conf
  sudo mkinitrd
  sudo reboot
  ``` 
   
  **Далее, после перезагрузки:**

  ```bash
  sudo zypper in patterns-devel-base-devel_kernel
  sudo zypper in nvidia-bumblebee nvidia-bumblebee-32bit
  sudo echo "blacklist nvidia" >> /etc/modprobe.d/99-local.conf
  sudo systemctl enable dkms
  sudo systemctl start dkms
  sudo mkinitrd
  sudo reboot
  ```
    
  **После перезагрузки:**

  Редактируем файл _/etc/bumblebee/bumblebee.conf_
  Вставляем в начало файла, ничего не удаляем и не исправляем

  ```bash
  [bumblebee]
  TurnCardOffAtExit=true
  Driver=nvidia
  ``` 

  **Перезапускаем bumblebee**
    
  ```bash
  sudo systemctl restart bumblebeed
  ```

   **Проверяем запуск:**

  ```bash
   optirun --status
   optirun glxspheres
  ```
   
   **При каждом обновлении ядра пересобираем:**

  ```bash
   sudo mkinitrd
  ```
   
   **Если nvidia-bumblebee не заводится делаем следующее:**

  ```bash
   sudo systemctl stop dkms
   sudo systemctl disable dkms
   sudo zypper remove nvidia-bumblebee nvidia-bumblebee-32bit
   sudo mkinitrd
   sudo reboot
  ```

   **После перезагрузки заного устанавливаем**

  ```bash
   sudo zypper in nvidia-bumblebee nvidia-bumblebee-32bit
   sudo systemctl enable dkms
   sudo systemctl start dkms
   sudo mkinitrd
   sudo reboot
  ```

   **После перезагрузки**

  ```bash
   sudo systemctl restart bumblebeed
   optirun --status
   optirun glxspheres
  ```

### Snapper undochange, create snap #opensuse

  **Отмена изменений в снимке**
    
  ```bash
    sudo snapper undochange 1315..1316
  ```

  **Создание снимка, терминал**
    
  ```bash
    sudo snapper create --type pre --print-number --description "Before somechange 22.06.2019"
    ...1315
  ```
 
  **После внесенных изменений в систему:**

  ```bash
    sudo snapper create --type post --pre-number 1315 --description "After somechange 22.06.2019"
  ```

### OpenSuse update Error

  **Ошибка чтения репозиториев обновления в OpenSuse**

  **В терминале**
    
  ```bash
    sudo rpm --rebuilddb
    sudo zypper clean && sudo zypper ref
  ```
