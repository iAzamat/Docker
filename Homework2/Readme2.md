# Домашняя работа №2

### Задание: 
1. запустить контейнер с Ubuntu, используя механизм LXC
2. ограничить контейнер 256 Мб ОЗУ и проверить, что ограничение работает 
3. "*"
4. добавить автозапуск контейнеру, перезагрузить ОС и убедиться, что контейнер  действительно запустился самостоятельно
5. при создании указать файл, куда записывать логи
6. после перезагрузки проанализировать логи

### Листинг команд:
0.	Заходим под рутом:
```bash
sudo -i
```

1.	Устанавливаем среду LXC и создаем контейнер **`test2`** с **Ubuntu**
```bash
apt install lxc lxctl lxc-templates lxc-utils -y
lxc-create -t ubuntu -n test2
```

2. Запускаем контейнер и проверяем RAM без ограничений
```bash
lxc-start -n test2
lxc-attach -n test2
free -m
exit
```

3. Останавливаем контейнер и правим конфиг для ограничения RAM до 256 MB
```bash
lxc-stop -n test2
nano /var/lib/lxc/test2/config
```
Добавляем в конец файла строку
```
lxc.cgroup2.memory.max = 256M
```

4. Запускаем контейнер и проверяем RAM с ограничением
```bash
lxc-start -n test2
lxc-attach -n test2
free -m
```

5. Удалить контейнер
```bash
lxc-destroy -n test2
```

6. Добавляем контейнер в автозапуск
```bash
nano /var/lib/lxc/test2/config

добавим в конец строку:
lxc.start.auto = 1

перезагружаем
reboot
```

7. Проверяем после перезагрузки запущенные контейнеры:
```bash
sudo -i
lxc-ls -f
```

8. Добавляем файл для логов
```bash
nano /var/lib/lxc/test2/config

добавим в конец строку:
lxc.console.logfile = /var/log/lxc/test2.log

reboot
```

8. Проверяем логи:
```bash
less /var/log/lxc/test2.log
```
