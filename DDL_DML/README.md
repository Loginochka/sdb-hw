# Домашнее задание к занятию «Работа с данными (DDL/DML)» - Логинов Даниил

### Задание 1

1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.
2. Создайте учётную запись sys_temp.
3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)
4. Дайте все права для пользователя sys_temp.
5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)
6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос:
```SQL

ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';

```
По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.
7. Восстановите дамп в базу данных.
8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.

### Ответ 1 

[Список пользователей](https://github.com/Loginochka/sdb-hw/blob/main/DDL_DML/media/select_usert.png)

[Список прав для пользователя sys_temp](https://github.com/Loginochka/sdb-hw/blob/main/DDL_DML/media/select_priv.png)

[Все таблицы базы данных sakila](https://github.com/Loginochka/sdb-hw/blob/main/DDL_DML/media/db_dump.png)


```SQL

CREATE USER 'sys_temp'@'localhost' IDENTIFIED WITH mysql_native_password BY '123';
GRANT ALL PRIVILEGES ON *.* TO 'sys_temp'@'localhost' WITH GRANT OPTION;

select user from mysql.user

show grants for 'sys_temp'@'localhost';

```

### Задание 2 

Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца:
в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц.

### Ответ 2 

[Таблица первичных ключей базы](https://github.com/Loginochka/sdb-hw/blob/main/DDL_DML/media/pri_key.png)