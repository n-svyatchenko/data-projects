# Вопросы

## 1. Какой оператор SQL используется для возвращения только разных значений?
SELECT DISTINCT

## 2. Есть ли ошибка в запросе? 

```
SELECT id, date, brand FROM orders WHERE brand = Nike
```


Необходимо добавить одинарные ковычки.

```
SELECT id, date, brand FROM orders WHERE brand = 'Nike'
```

## 3. Дана таблица users со столбцами name, age, city. С помощью какого запроса можно получить список имен пользователей без повторений?  SELECT DISTINCT name FROM TABLE ili SELECT name FROM table GROUP BY name

## 4. Напишите запрос, возвращающий имена, фамилии и даты рождения сотрудников. Условие: в фамилии содержится сочетание «se».

```
SELECT FirstName, LastName, BirthDate from Employees WHERE LastName like “%se%” 
```

## 5. Дана таблица БД "Товары". Для бытовой техники необходимо выяснить среднюю цену (назвать «Средняя_цена») и какое количество её на складе (Назвать «На_складе»). 

```
SELECT 
avg("Цена") as "Средняя_цена",
sum("Колличество")  as "На_складе"
from "Товары"
where "Тип" = 'Бытовая Техника'
```

## 6.  Дана таблица customers со столбцами name, email. Необходимо вывести дубли столбца email.

```
SELECT
name,
count(email)
from customers
group by name
having count(email) > 1
```

## 7. Дана таблица users со столбцами id, name, email и таблица customers со столбцами id, name, email. Необходимо с помощью соединения таблиц вывести уникальные email, которые встречаются в этих таблицах

```
SELECT DISTINCT email FROM (
SELECT id, name, email FROM users
UNION ALL 
SELECT id, name, email FROM users)
```

## 8. Дана таблица products со столбцами ProductId, ProductName, CategoryId, Price. Необходимо с помощью оконной функции для каждой CategoryId найти сумму, среднее, минимальное и максимальное значение (Добавить значения к строкам таблицы)

```
SELECT
SUM(Price) OVER (PARTITION BY CategoryId) as category_sum,
AVG(Price) OVER (PARTITION BY CategoryId) as category_avg,
MIN(Price) OVER (PARTITION BY CategoryId) as category_min,
MAX(Price) OVER (PARTITION BY CategoryId) as category_max,
FROM Products
```

## 9. Дана таблица products со столбцами ProductId, ProductName, CategoryId, Price. Необходимо с помощью подзапроса вывести ProductName, стоимость которых в среднем меньше, че стоимость монитора.


```
SELECT 
ProductName,
AVG(Price) FROM Products
GROUP BY ProductName
HAVING  AVG(Price) > (SELECT price FROM Products where ProductName = 'Монитор')
```

## 10. Дана таблица users со столбцами id, name, email и таблица customers со столбцами id, name, email. Необходимо объединить эти таблицы. Вывести все доступные строки и столбцы.

```
SELECT * FROM user FULL JOIN customers
```

