# Домашнее задание к занятию «SQL. Часть 2» - Логинов Даниил

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию:

* фамилия и имя сотрудника из этого магазина;
* город нахождения магазина;
* количество пользователей, закреплённых в этом магазине.

### Ответ 1

[Ответ 1](https://github.com/Loginochka/sdb-hw/blob/main/SQL_P_2/media/job_1.png)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Ответ 2

[Ответ 2](https://github.com/Loginochka/sdb-hw/blob/main/SQL_P_2/media/job_2.png)

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### Ответ 3

[Ответ 3](https://github.com/Loginochka/sdb-hw/blob/main/SQL_P_2/media/job_3.png)

### Задание 4*

Посчитайте количество продаж, выполненных каждым продавцом.
Добавьте вычисляемую колонку «Премия».
Если количество продаж превышает 8000, то значение в колонке будет «Да», иначе должно быть значение «Нет».

### Ответ 4

[Ответ 4](https://github.com/Loginochka/sdb-hw/blob/main/SQL_P_2/media/job_4.png)

## P.S Все запросы

```SQL

SELECT 
    s.store_id AS store_id,
    CONCAT(s.first_name, ' ', s.last_name) AS employee_name,
    ci.city AS store_city,
    COUNT(c.customer_id) AS customer_count
FROM staff s
JOIN store st ON s.store_id = st.store_id
JOIN address a ON st.address_id = a.address_id
JOIN customer c ON st.store_id = c.store_id
JOIN city ci ON a.city_id = ci.city_id
GROUP BY s.store_id, s.first_name, s.last_name, ci.city
HAVING COUNT(c.customer_id) > 300;


SELECT COUNT(*) AS count_of_long_films
FROM film
WHERE length > (SELECT AVG(length) FROM film);

SELECT 
    MONTH(payment_date) AS payment_month,
    SUM(amount) AS total_payment_amount,
    COUNT(rental.rental_id) AS rental_count
FROM payment
JOIN rental ON payment.rental_id = rental.rental_id
GROUP BY payment_month
ORDER BY total_payment_amount DESC
LIMIT 1;

SELECT staff_id, COUNT(*) AS sales_count,
CASE
  WHEN COUNT(*) > 8000 THEN 'Да'
  ELSE 'Нет'
END AS Премия
FROM payment p  
GROUP BY staff_id;

```