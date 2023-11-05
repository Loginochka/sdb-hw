# Домашнее задание к занятию «SQL. Часть 1» - Логинов Даниил

### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

### Ответ 1

[Ответ 1](https://github.com/Loginochka/sdb-hw/blob/main/SQL_P_1/media/job_1.png)

### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года включительно и стоимость которых превышает 10.00.

### Ответ 2

[Ответ 2](https://github.com/Loginochka/sdb-hw/blob/main/SQL_P_1/media/job_2.png)

### Задание 3

Получите последние пять аренд фильмов.

### Ответ 3

[Ответ 3](https://github.com/Loginochka/sdb-hw/blob/main/SQL_P_1/media/job_3.png)

### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie.

Сформируйте вывод в результат таким образом:
* все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
* замените буквы 'll' в именах на 'pp'.

### Ответ 4

[Ответ 4](https://github.com/Loginochka/sdb-hw/blob/main/SQL_P_1/media/job_4.png)

P.S Все запросы 

```SQL

SELECT DISTINCT district
FROM address
WHERE district LIKE 'K%a' AND district NOT LIKE '% %';

SELECT *
FROM rental
ORDER BY rental_date DESC
LIMIT 5;

SELECT *
FROM payment
WHERE payment_date >= '2005-06-15' AND payment_date <= '2005-06-18'
AND amount > 10.00;

SELECT
LOWER(REPLACE(CONCAT(lower(first_name), ' ', lower(last_name)), 'll', 'pp')) AS transformed_name
FROM customer
WHERE active = 1
AND (first_name = 'Kelly' OR first_name = 'Willie');

```