# Домашнее задание к занятию "Репликация и масштабирование" - Логинов Даниил

### Задание 1

На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.
Ответить в свободной форме.

### Ответ 1 

В master-slave может быть один мастер и одна или несколько реплик. В master-master может быть 2+ мастера, каждый мастер может быть доступен как для чтения, так и для записи.
В master-slave запись вполняется на master. Slave достпен только для чтения.
1. Master-Slave :
    * может быть один мастер и 1+ реплик;
    * запись вполняется на master, slave достпен только для чтения;
    * реплики могут быть использованы как балансировщики нагрузки на чтение;
    * мастер обеспечивает централизованное управление данными.
2. Master-Master (Мастер-Мастер):
    * 2+ мастера, каждый доступен как для чтения так и для записи;
    * обечпечивает распределение нагрузки между двумя мастерами, также повышает доступность БД;
    * более сложная конфигурация с точки зрения управления конфликтами и согласования данных;
    * важным критерием является согласование данных между мастерами во избежании конфликтов.
 
 ----

### Задание 2

Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.
Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.

### Ответ 2

[Ссылка на docker-copmose](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/mysql-master.yml)

[Ссылка на конфиг slave](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/slave/my.cnf)

[Ссылка на конфиг master](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/master/my.cnf)

[Ссылка на состояние master после деплоя](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/master_status_after_deploy.png)

[Созданные пользователь для репликации](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/user_for_replication.png)

[Ссылка на состояние slave после настройки](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/slave_status.png)

[Результат репликации](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/peplication_example.png)


CHANGE MASTER TO
MASTER_HOST = 'master_2',
MASTER_USER = 'replica',
MASTER_PASSWORD = '114563',
MASTER_LOG_FILE= 'mysql-bin.000003',
MASTER_LOG_POS = 157;

CHANGE MASTER TO
MASTER_HOST = 'master_1',
MASTER_USER = 'replica',
MASTER_PASSWORD = '114563',
MASTER_LOG_FILE= 'mysql-bin.000003',
MASTER_LOG_POS = 157;


create user 'replica'@'%' identified with mysql_native_password by '114563';
grant replication slave on *.* to 'replica'@'%';
show grants for 'replica'@'%';