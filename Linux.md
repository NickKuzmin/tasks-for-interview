`sudo apt-get update`

`sudo apt-get install xde`

-------------------
`cd /`
`cd ..`
`ls`
`ls ..`

`touch myfirstfile`
`mkdir myfirstdir`
`touch myseconddir/mysecondfile`

`ls - понять файл или директория`
`drwxr - директория`
`-rw - файл`

`tab - дополнить название файла`

`ps - процессы`

`сигналы:`
`sigkill -- 9`
`sigterm -- 15`
`kill -9 PID (завершение процесса)`

`ps -auxf`

`whoami - получение текущего пользователя`

`rwx (read/write/execute)`

`chmod (user access/group access/other access/all access) + (+/-/=) + (read/write/execute) + filename`
`chmod a+x myfirstfile`
`chmod g-rwx myfirstdir`
`chmod g=r,o=rwx myfirstdir`

`rm myfirstfile`
`rm myfirstdir/`
`rm -r myfirstdir/`

`/etc/passwd`

`useradd username -b /home/username -c "Username Usernamov" -g usergroup -p password`
`adduser username`

`usermod:`
`-l (поменять имя пользователя)`
`-d (поменять домашнюю директорию)`
`-m -d (поменять домашнюю директорию с созданием новой, если она ещё не существует)`
`-L (заблокировать или разблокировать пользователя)`

`/etc/shadow`

`passwd username (смена пароля)`
`whereis passwd`

`SUID: chmod u+s file`
`SGID: chmod g+s dir`
`Sticky-bit: chmod +t dir`

`/etc/group`

`groupadd groupname`

`usermod:`
`-g (задать основную группу для пользователя)`
`-G (задать дополнительную группу для пользователя)`
`-a (добавить группу для пользователя)`

`usermod -a -G devopsgroupname myusername`

`groupdel groupname`
`userdel username`

`sudo -u username ls /tmp`

------
`apt-get`
`apt`
`apt-cache`
`dpkg`

`dpkg -s telegram-desktop`

`apt-get update`
`apt-get install my-application-name`
`apt-get remove --purge my-application-name`
`apt-get changelog my-application-name`

`apt-cache pkgnames`
`apt-cache search telegram`
`apt-cache policy telegram-desktop`
`apt-get install telegram-desktop=0.2`

