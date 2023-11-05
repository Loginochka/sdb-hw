# Домашнее задание к занятию «Индексы» - Логинов Даниил

### Задание 1

Напишите запрос к учебной базе данных, который вернёт процентное отношение общего размера всех индексов к общему размеру всех таблиц.

### Ответ 1 

[Ответ 1](https://github.com/Loginochka/sdb-hw/blob/main/index/media/job_1.png)

```SQL

 SELECT
    SUM(index_length) / (SUM(data_length) + SUM(index_length)) * 100 AS index_size_percentage
FROM information_schema.tables
WHERE table_schema = 'sakila';

```
----

### Задание 2

Выполните explain analyze следующего запроса:

```SQL

select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id, f.title)
from payment p, rental r, customer c, inventory i, film f
where date(p.payment_date) = '2005-07-30' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id;

```
* перечислите узкие места;
* оптимизируйте запрос: внесите корректировки по использованию операторов, при необходимости добавьте индексы.

### Ответ 2 

[Результат explain analyze](https://github.com/Loginochka/sdb-hw/blob/main/SQL_P_2/media/explain_analyze.png)

* Самое времязатратное действие - это временная таблица с удалением дубликатов (Temporary table with deduplication). 
* Сортировка данных по столбцам c.customer_id и f.title выполняется в процессе выполнения запроса, что может также нагрузить бащу.
* Выполнение слияний таблиц может быть затратным. Есть несколько вложенных слияний, которые добавляют временные затраты.

Для оптимизации добавлию Индексы

```SQL

CREATE INDEX idx_payment_date ON payment (payment_date);
CREATE INDEX idx_rental_date ON rental (rental_date);
CREATE INDEX idx_customer_id ON rental (customer_id);
CREATE INDEX idx_inventory_id ON inventory (inventory_id);
CREATE INDEX idx_film_id ON inventory (film_id);

```
Немного изменил запрос:

```SQL

SELECT DISTINCT CONCAT(c.last_name, ' ', c.first_name), SUM(p.amount) OVER (PARTITION BY c.customer_id, f.title)
FROM payment p
JOIN rental r ON p.payment_date = r.rental_date
JOIN customer c ON r.customer_id = c.customer_id
JOIN inventory i ON r.inventory_id = i.inventory_id
JOIN film f ON i.film_id = f.film_id
WHERE DATE(p.payment_date) = '2005-07-30';

```

[Результат explain analyze после оптимизации](https://github.com/Loginochka/sdb-hw/blob/main/SQL_P_2/media/explain_analyze_optim.png)