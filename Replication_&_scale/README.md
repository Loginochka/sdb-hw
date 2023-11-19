# Домашнее задание к занятию "Репликация и масштабирование. Часть 1" - Логинов Даниил

### Задание 1

На лекции рассматривались режимы репликации master-slave, master-master, опишите их различия.
Ответить в свободной форме.

### Ответ 1 

1. Master-Slave:
    * может быть один мастер и 1+ реплик;
    * запись вполняется на master, slave достпен только для чтения;
    * реплики могут быть использованы как балансировщики нагрузки на чтение;
    * мастер обеспечивает централизованное управление данными.
2. Master-Master:
    * 2+ мастера, каждый доступен как для чтения так и для записи;
    * обечпечивает распределение нагрузки между двумя мастерами, также повышает доступность БД;
    * более сложная конфигурация с точки зрения управления конфликтами и согласования данных;
    * важным критерием является согласование данных между мастерами во избежании конфликтов.
 
 ----

### Задание 2

Выполните конфигурацию master-slave репликации, примером можно пользоваться из лекции.
Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.

### Ответ 2

[Ссылка на docker-copmose](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/master-slave/mysql-master.yml)

[Ссылка на конфиг slave](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/master-slave/slave/my.cnf)

[Ссылка на конфиг master](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/master-slave/master/my.cnf)

[Ссылка на состояние master'а после деплоя](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/master_status_after_deploy.png)

[Созданный пользователь для репликации](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/user_for_replication.png)

[Ссылка на состояние slave'a после настройки](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/slave_status.png)

[Результат репликации](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/peplication_example.png)

----

### Задание 3*

Выполните конфигурацию master-master репликации. Произведите проверку.

Приложите скриншоты конфигурации, выполнения работы: состояния и режимы работы серверов.

### Ответ 3

[Ссылка на docker-copmose](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/master-master/mysql-m-m.yml)

[Ссылка на конфиг master_1](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/master-master/master_1/my.cnf)

[Ссылка на конфиг master_2](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/master-master/master_2/my.cnf)

[Ссылка на состояние master'ов после деплоя](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/masters_status_after_deploy.png)

[Созданный пользователь для репликации](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/masters_user_for_replication.png)

[Ссылка на состояние master'ов после настройки](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/m-m_status.png)

[Результат репликации](https://github.com/Loginochka/sdb-hw/blob/main/Replication_%26_scale/media/m-m_peplication_example.png)
