# Домашняя работа №1

### Задание: 
Необходимо продемонстрировать изоляцию одного и того же приложения 
(как решено на семинаре - командного интерпретатора) в одной, различных пространствах имен.
### Формат сдачи ДЗ: 
предоставить доказательства выполнения задания посредством ссылки на google-документ с правами на комментирование/редактирование.
### Результатом работы будет: 
текст объяснения, логи выполнения, история команд и скриншоты 
(важно придерживаться такой последовательности).
Пояснения - cамое простое , это как в первом примере лекции.

### Листинг команд:
1.	Заходим под рутом:
```bash
user@user-VB:~$ sudo -i
```

2.	Создаем папки для изоляции
```bash
root@user-VB:~# mkdir hw1
root@user-VB:~# cd hw1
root@user-VB:~/hw1# mkdir bin lib64 lib
```

3. Копируем bash
```bash
root@user-VB:~/hw1# cp /bin/bash ./bin/
```
4. Проверяем зависимости
```bash
root@user-VB:~/hw1# ldd /bin/bash
```
5. Копируем недостающие библиотеки
```bash
root@user-VB:~/hw1# cp /lib/x86_64-linux-gnu/libtinfo.so.6 ./lib
root@user-VB:~/hw1# cp /lib/x86_64-linux-gnu/libc.so.6 ./lib
root@user-VB:~/hw1# cp /lib64/ld-linux-x86-64.so.2 ./lib64/
```
6. Переходим в папку и проверяем содержимое
```bash
root@user-VB:~/hw1# cd ..
root@user-VB:~# ls
```
7. Меняем корневую директорию
```bash
root@user-VB:~# chroot hw1 /bin/bash
```
8. Скопируем файлы для работы команды ls
```bash
root@user-VB:~# cd hw1
root@user-VB:~/hw1# cp /bin/ls ./bin/
root@user-VB:~/hw1# ldd /bin/ls
root@user-VB:~/hw1# cp /lib/x86_64-linux-gnu/libselinux.so.1 ./lib
root@user-VB:~/hw1# cp /lib/x86_64-linux-gnu/libc.so.6 ./lib
root@user-VB:~/hw1# cp /lib/x86_64-linux-gnu/libpcre2-8.so.0 ./lib
root@user-VB:~/hw1# cp  /lib64/ld-linux-x86-64.so.2 ./lib64
root@user-VB:~/hw1# cd ..
```
9. Меняем корневую директорию
```bash
root@user-VB:~# chroot hw1 /bin/bash
root@user-VB:~# history >> log.txt
```