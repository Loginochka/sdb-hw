# Домашнее задание к занятию «Защита хоста» - Логинов Даниил 

### Задание 1

Установите eCryptfs.
Добавьте пользователя cryptouser.
Зашифруйте домашний каталог пользователя с помощью eCryptfs.

В качестве ответа пришлите снимки экрана домашнего каталога пользователя с исходными и зашифрованными данными.

### Ответ 1 

[Home пользователя cryptouser](https://github.com/Loginochka/sdb-hw/blob/main/host_sec/media/job-1.png)

----

### Задание 2

Установите поддержку LUKS.
Создайте небольшой раздел, например, 100 Мб.
Зашифруйте созданный раздел с помощью LUKS.

В качестве ответа пришлите снимки экрана с поэтапным выполнением задания.

### Ответ 2

[Новый диска для шифрования](https://github.com/Loginochka/sdb-hw/blob/main/host_sec/media/new_disk.png)

[Подготовка диска](https://github.com/Loginochka/sdb-hw/blob/main/host_sec/media/prepare_dislk.png)

[Маппинг и форматирование раздела](https://github.com/Loginochka/sdb-hw/blob/main/host_sec/media/mount_and_format_disk.png)

[Монтирование "открытого" раздела](https://github.com/Loginochka/sdb-hw/blob/main/host_sec/media/mount_secret_part.png)

[Проверка смонтированного раздела](https://github.com/Loginochka/sdb-hw/blob/main/host_sec/media/check_disk_and_unmount.png)

[Результат шифрования](https://github.com/Loginochka/sdb-hw/blob/main/host_sec/media/result.png)