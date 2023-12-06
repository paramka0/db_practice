![image](https://github.com/paramka0/db_practice/assets/74873667/12d8003e-db2b-4392-92b3-c1575d79a5d2)![image](https://github.com/paramka0/db_practice/assets/74873667/5db4b215-a23d-4d77-a8d2-abb9c1b36c36)
![image](https://github.com/paramka0/db_practice/assets/74873667/216685ff-4239-4bb6-baef-ab53f076a557)
![image](https://github.com/paramka0/db_practice/assets/74873667/bb6dce3a-5b00-490a-9710-4762f7389099)
![image](https://github.com/paramka0/db_practice/assets/74873667/72028e0b-2ef9-4a65-aac6-2433bd4241bb)
![image](https://github.com/paramka0/db_practice/assets/74873667/9cde950f-cda6-4d27-84e9-132cc64b70f9)
![image](https://github.com/paramka0/db_practice/assets/74873667/66484159-6326-4451-b760-e7ed5c19b0d9)
![image](https://github.com/paramka0/db_practice/assets/74873667/18361358-217e-4804-9c39-32d05b8a0e89)
![image](https://github.com/paramka0/db_practice/assets/74873667/6e520222-f8d0-4d1c-b04b-18252d4eac4a)
![image](https://github.com/paramka0/db_practice/assets/74873667/9789a1cf-3f36-4e46-a7ec-95adebd9d848)
![image](https://github.com/paramka0/db_practice/assets/74873667/1120c0b1-89cb-4ade-82ff-b6ba89115c60)


## 19.09.2023
`--1--
```sql
SELECT person.id, person.name, "age", "gender", "address", pizzeria.id, pizzeria.name,
"rating" FROM "person", "pizzeria"
ORDER BY pizzeria.id ASC;
```
```sql
SELECT person.id, person.name, "age", "gender", "address", pizzeria.id, pizzeria.name,
"rating" FROM "person", "pizzeria"
ORDER BY person.id ASC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/163cd372-6c9c-439e-a6f1-cb405275ee49)

![image](https://github.com/paramka0/db_practice/assets/74873667/50963c45-b905-405d-996b-9edc9746dfd2)


--2--
```sql
SELECT "order_date" AS action_date, "name" FROM "person_order", "person"
WHERE "order_date" IN (SELECT "visit_date" FROM "person_visits") AND person_order.person_id = person.id
ORDER BY "name" DESC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/4aa0bea9-d367-4fbe-bce6-11f32ad2ea22)

--3--
```sql
SELECT "order_date", ("name" || '(age:' || "age" || ')') AS person_information FROM "person_order" JOIN "person" ON "person_id" = person.id
ORDER BY "order_date" ASC, "person_information" ASC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/900f88d6-9fac-4694-b2a3-d538e4a0c3b4)

--4--
```sql
SELECT "order_date", ("name" || '(age:' || "age" || ')') AS person_information FROM "person_order" NATURAL JOIN "person"
ORDER BY "order_date" ASC, "person_information" ASC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/97b181a4-8559-4f39-9d81-0916dd236c5e)

--5--
-- in --
```sql
SELECT "name" FROM "pizzeria"
WHERE "id" NOT IN
(SELECT "pizzeria_id" FROM "person_visits");
```
![image](https://github.com/paramka0/db_practice/assets/74873667/7f875e5e-b426-45c5-aecf-d98b6d7619ee)
-- Exist --
```sql
SELECT "name" FROM "pizzeria"
WHERE NOT EXISTS
(SELECT * FROM "person_visits" WHERE pizzeria.id = "pizzeria_id");
```
![image](https://github.com/paramka0/db_practice/assets/74873667/61900b04-529b-4087-9365-7b6b8f211fdb)

--6--
```sql
SELECT person.name AS person_name, menu.pizza_name, pizzeria.name AS pizzeria_name FROM "person_order"
JOIN "person" ON person.id = person_order.person_id
LEFT JOIN "menu" ON menu.id = person_order.menu_id
LEFT JOIN "pizzeria" ON pizzeria.id = menu.pizzeria_id
ORDER BY "person_name", "pizza_name", "pizzeria_name";
```
![image](https://github.com/paramka0/db_practice/assets/74873667/f6cda925-8a8e-43c6-92d9-9721e5c47813)

## 26.09.23
--1--
```sql
SELECT firstname, lastname
FROM students
WHERE age > 21;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/9e9a1f45-ce88-4e5b-a4e8-2300ac43eea4)

--2--
```sql
SELECT coursename FROM courses;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/90730cd9-529c-4c1c-91c5-d8dadce1f3e8)

--3--
```sql
SELECT firstname, lastname FROM students
JOIN studentcourses ON studentcourses.studentid = students.studentid
WHERE courseid = (SELECT courseid FROM courses WHERE coursename = 'Математика');
```
![image](https://github.com/paramka0/db_practice/assets/74873667/97db56ed-ab6a-46af-929d-98e850767e16)

--4--
```sql
SELECT firstname, lastname FROM students
JOIN studentcourses ON studentcourses.studentid = students.studentid
WHERE courseid = (SELECT courseid FROM courses WHERE coursename = 'История') AND age = 20;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/73f6b9e6-261d-4b0a-bba1-18f4b0e97242)

--5--
```sql
SELECT coursename, (SELECT COUNT(studentid) FRom studentcourses WHERE c.courseid = studentcourses.courseid) 
FROM courses c;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/c8aefdce-e2fa-4edd-81b8-6e5718797940)

--6--
```sql
SELECT AVG(age) AS avg_age FROM students;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/a8c1b4e0-6ef8-4b1e-812f-b1292b6a32d7)

--7--
```sql
SELECT firstname, lastname, studentid FROM students
WHERE studentid NOT IN (SELECT studentid FROM studentcourses);
```
![image](https://github.com/paramka0/db_practice/assets/74873667/ff1fc232-cb31-4357-a290-26e98c516854)

--8--
```sql
SELECT coursename, (SELECT COUNT(studentid) FROM studentcourses WHERE c.courseid = studentcourses.courseid) 
FROM courses c;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/f4298a70-82bb-4094-9082-4b16ebd6c8ff)

--9--
```sql
SELECT firstname, lastname FROM students
JOIN studentcourses ON studentcourses.studentid = students.studentid
WHERE courseid = (SELECT courseid FROM courses WHERE coursename = 'Биология') AND age >= 22;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/b98a1be6-3346-4799-b75f-4fa6b50928c1)

## 04.10.23

--1--
```sql
SELECT id FROM menu 
EXCEPT
SELECT menu_id FROM person_order
ORDER BY id ASC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/a7f3f195-59de-435c-98a7-ef04e2a6d951)

--2--
```sql
SELECT pizza_name, price, name FROM menu m
LEFT JOIN pizzeria ON m.pizzeria_id = pizzeria.id
WHERE m.id IN (SELECT id FROM menu 
EXCEPT
SELECT menu_id FROM person_order)
ORDER BY price ASC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/87bdc218-e4cd-4b5c-ae29-77035472bace)

## 12.09.23

--1--

```sql
insert into person values (10, 'Zhenia', 18, 'male', 'Saint-Petersburg');
insert into person values (11, 'Olga', 35, 'female', 'Kemerovo');
insert into person values (12, 'Lisa', 19, 'female', 'Kazan');
insert into person values (13, 'Oleg', 29, 'male', 'Kemerovo');
insert into person values (14, 'Pavel', 38, 'male', 'Saint-Petersburg');
insert into person values (15, 'Viktor', 56, 'male', 'Kazan');
insert into person values (16, 'John', 23, 'male', 'Novosinirsk');
insert into person values (17, 'James', 47, 'male', 'Samara');
insert into person values (18, 'Frank', 39, 'male', 'Saint-Petersburg');
insert into person values (19, 'Diane', 15, 'female', 'Kemerovo');
insert into person values (20, 'Carol', 22, 'female', 'Samara');
```
![image](https://github.com/paramka0/db_practice/assets/74873667/9a8efd60-7574-49e5-8ffb-df53e0e4726d)

```sql
insert into pizzeria values (7,'Pizzeria Stokey', 3.9);
insert into pizzeria values (8,'Voodoo Rays', 4.4);
insert into pizzeria values (9,'Zia Lucia', 5.0);
insert into pizzeria values (10,'Hai Cenato', 2.3);
insert into pizzeria values (11,'Princi', 4.0);
insert into pizzeria values (12,'Four Hundred Rabbits', 4.9);
insert into pizzeria values (13,'50 Kalo di Ciro Salvo', 3.7);
insert into pizzeria values (14,'Pizza Castle', 1.9);
insert into pizzeria values (15,'Quattro Pizza', 1.2);
insert into pizzeria values (16,'Ragazza', 3.2);
insert into pizzeria values (17,'Pizza Planet', 4.7);
```
![image](https://github.com/paramka0/db_practice/assets/74873667/7214b464-6fd4-4eb8-8a66-4ed52130d7cd)

```sql
insert into person_visits values (20, 17, 10, '2022-01-11');
insert into person_visits values (21, 17, 9, '2022-01-11');
insert into person_visits values (22, 12, 11, '2022-01-13');
insert into person_visits values (23, 11, 11, '2022-01-12');
insert into person_visits values (24, 17, 7, '2022-01-20');
insert into person_visits values (25, 15, 12, '2022-02-01');
insert into person_visits values (26, 12, 12, '2022-02-01');
insert into person_visits values (27, 17, 15, '2022-01-21');
insert into person_visits values (28, 9, 13, '2022-01-30');
insert into person_visits values (29, 8, 15, '2022-01-29');
insert into person_visits values (30, 7, 16, '2022-01-25');
```
![image](https://github.com/paramka0/db_practice/assets/74873667/16e61bb4-2ef9-4098-9d94-cae8f5d881b3)

```sql
insert into menu values (19,6,'cheese pizza', 700);
insert into menu values (20,6,'pepperoni pizza', 800);
insert into menu values (21,7,'cheese pizza', 700);
insert into menu values (23,7,'pepperoni pizza', 800);
insert into menu values (24,7,'sausage pizza', 950);
insert into menu values (25,8,'cheese pizza', 700);
insert into menu values (26,8,'mushroom pizza', 950);
insert into menu values (27,8,'sausage pizza', 950);
insert into menu values (28,9,'cheese pizza', 700);
insert into menu values (29,9,'supreme pizza', 1200);
```
![image](https://github.com/paramka0/db_practice/assets/74873667/3a4dcf29-9454-4ee1-b762-7c64e51bf9c6)

```sql
insert into person_order values (21,10, 2, '2022-01-11');
insert into person_order values (22,11, 19, '2022-01-16');
insert into person_order values (23,11, 2, '2022-01-12');
insert into person_order values (24,11, 7, '2022-01-18');
insert into person_order values (25,12, 10, '2022-01-21');
insert into person_order values (26,12, 17, '2022-01-09');
insert into person_order values (27,13, 10, '2022-01-24');
insert into person_order values (28,14, 7, '2022-01-12');
insert into person_order values (29,14, 5, '2022-01-20');
insert into person_order values (30,14, 1, '2022-01-02');
insert into person_order values (31,15, 9, '2022-01-23');
```
![image](https://github.com/paramka0/db_practice/assets/74873667/26e2473b-21ae-4604-8973-1d736763dd60)

--2--
```sql
SELECT name, age, address
FROM person
WHERE address = 'Kemerovo';
```
![image](https://github.com/paramka0/db_practice/assets/74873667/978e94bb-ec38-4930-a953-6c3aa9f25051)

--3--
```sql
SELECT  name, age, address, gender
FROM person
WHERE address = 'Kazan' AND gender = 'female'
ORDER BY name ASC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/90cc6fdd-04dd-4ce6-b431-3407aa3ba929)

--4--
```sql
SELECT name, rating
FROM pizzeria
WHERE rating >= 3.5 AND rating <= 5.0
ORDER BY rating DESC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/36a4874b-2f6c-45f3-9f59-48bf41b4ef84)
```sql
SELECT name, rating
FROM pizzeria
WHERE rating BETWEEN 3.5 AND 5.0
ORDER BY rating DESC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/d9d0bf1a-f89b-4583-8a20-829891610f82)

--5--
```sql
SELECT DISTINCT ON (person_id) person_id, visit_date
FROM person_visits
WHERE visit_date >= '2022.01.11' AND visit_date <= '2022.01.31' OR person_id = 2
ORDER BY person_id DESC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/bd8b675e-e555-4aae-9380-815d60534329)

## 13.09.23
--1--
```sql
SELECT menu.id AS object_id, pizza_name AS object_name FROM menu
UNION
SELECT person.id, name FROM person
ORDER BY object_id ASC, object_name ASC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/0ba0e582-3a82-484d-be9b-9140eced3bea)

--2--
```sql
SELECT menu.id AS object_id, pizza_name AS object_name FROM menu
UNION All
SELECT person.id, name FROM person
ORDER BY object_name DESC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/036414bc-c972-44fc-a0bf-98f58b6ec5fa)

--3--
```sql
SELECT person_id, visit_date AS action_date FROM person_visits
INTERSECT
SELECT person_id, order_date FROM person_order ORDER BY action_date ASC, person_id DESC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/df235834-7a12-4ff5-8518-fdd2e5cab141)

## 20.09.23

--1--
```sql
SELECT name, rating
FROM  pizzeria
LEFT  JOIN person_visits ON  pizzeria.id = person_visits.pizzeria_id
WHERE person_visits.pizzeria_id IS NULL
ORDER BY rating DESC;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/e85753a1-d96f-4f5e-b822-b5ca49951852)

--2--
```sql
SELECT missing_days::date FROM generate_series('2022-01-01', '2022-01-10', interval '1 day') as missing_days
FULL JOIN
(SELECT * FROM person_visits
WHERE person_id = 1 OR  person_id = 2) AS tab ON missing_days = tab.visit_date
WHERE person_id IS NULL;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/0f87e9d7-f517-437a-8550-3574a195e3e5)

## 11.10.23

--1--

```sql
CREATE INDEX idx_menu_pizzeria_id ON menu(pizzeria_id);
CREATE INDEX idx_person_visits_person_id ON person_visits(person_id);
CREATE INDEX idx_person_visits_pizzeria_id ON person_visits(pizzeria_id);
CREATE INDEX idx_person_order_person_id ON person_order(person_id);
CREATE INDEX idx_person_order_menu_id ON person_order(menu_id);
```
![image](https://github.com/paramka0/db_practice/assets/74873667/cd1edfbb-27d4-4916-bc4e-11a9d37dbd1a)

  
--2--
```sql
SET enable_seqscan = OFF;
EXPLAIN ANALYZE SELECT pizza_name, pizzeria.name AS pizzeria_name FROM menu, pizzeria
WHERE menu.pizzeria_id = pizzeria.id
```
![image](https://github.com/paramka0/db_practice/assets/74873667/279265d3-65f6-46a6-9947-a8796c028956)

  
--3--
```sql
CREATE INDEX idx_person_name ON person(name);
EXPLAIN ANALYZE 
SELECT UPPER(name) FROM person;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/b871aaa6-2671-4bcd-a4f3-1fd5d62fa0b5)
 
  
--4--
```sql
CREATE INDEX idx_person_order_multi ON person_order(person_id, menu_id);
EXPLAIN ANALYZE
SELECT person_id, menu_id,order_date
FROM person_order
WHERE person_id = 8 AND menu_id = 19;
```
![image](https://github.com/paramka0/db_practice/assets/74873667/3e0f155f-1c1d-4d46-a275-2696e8abd617)

  
--5--
```sql
CREATE UNIQUE INDEX idx_menu_unique ON menu(pizzeria_id, pizza_name);
EXPLAIN ANALYZE
SELECT pizzeria_id, pizza_name FROM menu
```
![image](https://github.com/paramka0/db_practice/assets/74873667/b45f2b0f-f4be-4e65-a300-f08e2520c558)

  
--6--
```sql
CREATE UNIQUE INDEX idx_person_order_order_date ON person_order(person_id, menu_id) WHERE order_date = '2022-01-01';
EXPLAIN ANALYZE
SELECT person_id, menu_id FROM person_order
WHERE order_date = '2022-01-01'
```
![image](https://github.com/IAmIngibitor/DB-practice-in-college/assets/109351663/1f0e15db-f5c7-4920-a7dd-4e4b318ccc4a)  
  
--7--
```sql
CREATE INDEX idx_1 ON pizzeria(id, rating);
EXPLAIN ANALYZE
SELECT
    m.pizza_name AS pizza_name,
    max(rating) OVER (PARTITION BY rating ORDER BY rating ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING) AS k
FROM  menu m
INNER JOIN pizzeria pz ON m.pizzeria_id = pz.id
ORDER BY 1,2;
```

![image](https://github.com/paramka0/db_practice/assets/74873667/ca269e55-3ce4-48ec-8186-5f617efa1a17)

## 18.10.2023

--1--
```sql
SELECT cus.first_name, cus.last_name FROM customers cus
JOIN orders ord ON cus.customer_id = ord.customer_id
GROUP BY cus.first_name, cus.last_name, ord.order_date
HAVING COUNT(*) >= 2 AND ord.order_date BETWEEN '2023-07-17' AND '2023-10-17'
ORDER BY 1, 2
```
![image](https://github.com/paramka0/db_practice/assets/74873667/06b16b65-3699-4786-be01-aafb5a642e92)

--2--
```sql
SELECT AVG(ord.quantity) AS average, prd.category FROM orders ord
JOIN products prd ON prd.product_id = ord.product_id
WHERE price >= 50
GROUP BY prd.category
ORDER BY 2
```
![image](https://github.com/paramka0/db_practice/assets/74873667/0e293520-18b5-41dd-92a4-7fd76dc2b22b)

--3--
```sql
WITH sum_customers AS (
	SELECT ord.customer_id, SUM(prd.price) AS summa FROM orders ord
	JOIN products prd ON prd.product_id = ord.product_id
	GROUP BY ord.customer_id
), avg_sum AS (
	SELECT ord.order_id, ord.customer_id, ord.quantity, SUM(prd.price) AS summa FROM orders ord
	JOIN products prd ON prd.product_id = ord.product_id
	GROUP BY ord.order_id
)

SELECT cus.first_name, cus.last_name, cus.email FROM customers cus
JOIN sum_customers scus ON scus.customer_id = cus.customer_id
JOIN avg_sum asum ON asum.customer_id = cus.customer_id
GROUP BY cus.first_name, cus.last_name, cus.email, scus.summa
HAVING scus.summa > AVG(asum.summa)
```
![image](https://github.com/paramka0/db_practice/assets/74873667/b776ae03-f9a2-4a1c-b7e5-481d97b1abbe)

--4--
```sql
WITH sum_price AS (
	SELECT ord.order_id, ord.customer_id, ord.product_id, ord.quantity, SUM(prd.price) AS summa FROM orders ord
	JOIN products prd ON prd.product_id = ord.product_id
	GROUP BY ord.order_id
	HAVING SUM(prd.price) >= 1000
)

SELECT cus.first_name, cus.last_name FROM customers cus
JOIN sum_price spr ON spr.customer_id = cus.customer_id
JOIN products prd ON prd.product_id = spr.product_id
WHERE category != 'Electronics'
```
![image](https://github.com/paramka0/db_practice/assets/74873667/28270a27-2eac-48fa-b33b-08b022b054cf)

--5--
--6--
```sql
WITH customer_orders AS (
	SELECT * FROM (SELECT ord.customer_id, ord.order_date, row_number() over(partition by ord.customer_id order by ord.order_date DESC) as rn FROM orders ord) cus_ord
	WHERE rn < 3
	
), max_range_order AS (
	SELECT csod.customer_id, (MAX(csod.order_date) - MIN(csod.order_date)) AS order_range FROM customer_orders csod
	GROUP BY 1
)

SELECT cus.first_name, cus.last_name, MAX(mro.order_range) FROM max_range_order mro
JOIN customers cus ON cus.customer_id = mro.customer_id
GROUP BY 1, 2
HAVING MAX(mro.order_range) = (SELECT MAX(mro.order_range) FROM max_range_order mro)
```
![image](https://github.com/paramka0/db_practice/assets/74873667/309f6aa7-090e-4f85-96a3-831630f73463)

--7--
```sql
SELECT cus.first_name, cus.last_name FROM customers cus
LEFT JOIN orders ord ON ord.customer_id = cus.customer_id
WHERE ord.order_date BETWEEN '2023-08-23' AND '2023-10-23'
```
![image](https://github.com/paramka0/db_practice/assets/74873667/8018f072-ded5-45f1-82d4-167a1f358e8d)

--8--
```sql
UPDATE products
SET price = price - (price * 10 / 100)
WHERE category = 'Clothing';

SELECT * FROM products
WHERE category = 'Clothing'
```
![image](https://github.com/paramka0/db_practice/assets/74873667/4d4d1cc1-a26c-4f00-8458-440b54a567e6)

## 01.11.23
![image](https://github.com/paramka0/db_practice/assets/74873667/27e6cfcf-e1a1-40fb-9f53-3dca7c9ea320)

```sql
CREATE TABLE equipment (
id INT PRIMARY KEY,
name VARCHAR(255),
serial_number VARCHAR(255),
description VARCHAR(255),
manufacturer VARCHAR(255)
);

CREATE TABLE client (
client_id INT PRIMARY KEY,
family VARCHAR(50),
address VARCHAR(100),
telephone VARCHAR(20)
);

CREATE TABLE order (
order_id INT PRIMARY KEY,
equipment_id INT,
client_id INT,
tab_number_master INT,
order_status_id INT,
execution_code INT
);

CREATE TABLE staff (
tab_number INT PRIMARY KEY,
family VARCHAR(50),
post_cod INT,
passport_series VARCHAR(10),
passport_number VARCHAR(20),
address VARCHAR(100),
telephone VARCHAR(20),
date_accepted DATE
);

CREATE TABLE post (
post_cod INT PRIMARY KEY,
post VARCHAR(50)
);

CREATE TABLE order_status (
order_cod INT PRIMARY KEY,
name VARCHAR(50)
);

CREATE TABLE execution (
execution_code INT PRIMARY KEY,
type_repair VARCHAR(50),
total_cost FLOAT,
date_execution DATE
);

CREATE TABLE execution_components_details (
uniquelid INT PRIMARY KEY,
component_id INT,
component_cost FLOAT,
work_cost FLOAT,
execution_id INT,
discount FLOAT
);
```
# заполнеие таблиц

```sql
INSERT INTO client (client_id, family, address, telephone) 
VALUES ('1', 'Гасанов', 'Ивановская область, город Дмитров, ул. Домодедовская, 66', '+7 (969) 158-15-92'),
('2', 'Функ', 'Калужская область, город Орехово-Зуево, спуск Косиора, 26', '+7 (977) 198-75-39'),
('3', 'Фролова', 'Астраханская область, город Можайск, ул. 1905 года, 56', '+7 (906) 997-96-45'),
('4', 'Панфилов', 'Омская область, город Серпухов, ул. Ломоносова, 01', '+7 (975) 111-33-57'),
('5', 'Артемов', 'Самарская область, город Можайск, проезд Космонавтов, 67', '+7 (907) 542-12-56'),
('6', 'Комаров', 'Брянская область, город Егорьевск, бульвар Ломоносова, 46', '+7 (927) 259-61-53'),
('7', 'Федотова', 'Новосибирская область, город Чехов, пл. Чехова, 55', '+7 (984) 663-22-16'),
('8', 'Семина', 'Ульяновская область, город Луховицы, пер. Космонавтов, 52', '+7 (919) 117-48-33'),
('9', 'Шульгин', 'Волгоградская область, город Дорохово, бульвар Ладыгина, 52', '+7 (941) 802-90-96'),
('10', 'Воронов', 'Нижегородская область, город Пушкино, въезд Ладыгина, 51', '+7 (989) 758-94-41');
```
```sql
INSERT INTO equipment (id, name, serial_number, description, manufacturer) 
VALUES ('1', 'Тележка "Скейт"', '542321', 'Тележка RUSKLAD "Скейт" (400х600) d125мм Скейт 125 выполнена из цельного листового металла. Изделие оснащено четырьмя колесами, оно служит для перевозки пластиковых контейнеров и ящиков.', 'RUSKLAD'),
('2', 'Гидравлическая тележка', '763433', 'Гидравлическая тележка Gigant JHPT2000 подойдет для работы на складах со средней пропускной способностью. Наличие гидравлического узла позволяет перевозить палетированные грузы массой до 2 тонн. Минимальная высота подъема составляет 85 мм, максимальная - 195 мм. Длина вил - 115 см.', 'Gigant'),
('3', 'Тележка грузовая КГМ 200 с литыми колёсами', '756655', 'Тележка RUSKLAD грузовая КГМ 200 с литыми колёсами КГМ 200 литые позволяет быстро и удобно перевозить грузы весом до 150 кг. Изделие обладает платформой, благодаря которой вы с лёгкостью и максимальным комфортом сможете перевозить различные грузы. Оснащена литыми колёсами D 200 мм.', 'RUSKLAD'),
('4', 'Платформенная тележка с сетчатыми бортами', '112433', 'Платформенная тележка с сетчатыми бортами RUSKLAD ТС 2, 600x900 мм, d125 мм ТС 2 125 служит для бережной транспортировки различных грузов и товаров суммарной массой до 300 кг. Полимерное порошковое покрытие устойчиво к влиянию коррозии, что позволяет использовать приспособление на открытом воздухе даже при неблагоприятных погодных условиях.', 'RUSKLAD'),
('5', 'Тележка "Кега 3"', '867343', 'Тележка RUSKLAD "Кега 3" (440x281x1160) грузовая, с пневматическими колёсами d250мм Кега 3 пневмо 250 разработана для перевозки пивных кег или бочонков с квасом. Модель оснащена универсальной осью, на которую также можно установить литые колеса диаметром 250 мм. Предполагает перевозку грузов до 130 кг.', 'RUSKLAD'),
('6', 'Транспортно-роликовая платформа', '987445', 'Транспортно-роликовая платформа EURO-LIFT CRA6 г/п 6 т 00012451 обладает небольшими размерами и предназначена для перемещения грузов. Удобство транспортировки заключается в небольших полиуретановых колесах: они обеспечивают комфортное перемещение с минимальным трением даже при значительной нагрузке. Толщина деталей, надежная сварка, наличие ребер жесткости под платформой делают конструкцию более прочной и качественной.', 'EURO-LIFT'),
('7', 'Самоходный подъемник ножничного типа с питанием от аккумуляторов', '872325', 'Устройства самоходных моделей GROST TOWER представляют собой самоходные сопровождаемые гидравлические подъемники ножничного типа, оснащенные платформой для подъема и опускания грузов и людей с инструментом, сообразно с максимальной высотой подъема и грузоподъемностью. Горизонтальное транспортирование подъемника требует твердых, ровных и гладких полов с уклоном не более 10-15%.', 'Tower Drive'),
('8', 'Тележка Тара', '135436', 'Тележка Тара.ру п/э 600х400 чёрные резиновые колёса, зелёный 08167 выполнена из пластика. Модель используется для внутрицехового и внутрискладского перемещения загруженных или пустых пластиковых ящиков.', 'RUSKLAD'),
('9', 'Тележка для двух баллонов', '765444', 'Тележка RUSKLAD КП 2 представляет собой специализированное оборудование для перевозки баллонов или аналогичных по форме предметов. Ширина тележки обеспечивает возможность перевозки двух баллонов одновременно. Продукт обладает системой ремневой фиксации баллонов.', 'RUSKLAD'),
('10', 'Набор для перемещения мебели', '125636', 'Набор для перемещения мебели PARK в наборе: 4 тележки + домкрат 103935 поможет с легкостью передвинуть мебель в пределах любого помещения, защитить мебель, пол и стены от повреждений.', 'PARK');
SELECT * FROM equipment;
```
```sql
INSERT INTO execution (execution_code, type_repair, total_cost, date_execution) 
VALUES ('1', 'Косметический ремонт', '15000', '20012-02-05'),
('2', 'Капитальный ремонт', '15000', '20021-07-22'),
('3', 'Декорирование', '10000', '2023-10-14'),
('4', 'Ремонт без проблем', '20000', '2018-11-25'),
('5', 'Евроремонт', '75000', '20020-08-13');
SELECT * FROM execution;
```
```sql
INSERT INTO execution_components_details (uniquelid, component_id, component_cost, work_cost, execution_id, discount) 
VALUES ('1', '1', '13500', '15000', '1', '15'),
('2', '2', '11000', '15000', '2', '10'),
('3', '3', '9000', '10000', '3', '25'),
('4', '4', '22000', '25000', '4', '17'),
('5', '5', '65000', '75000', '5', '21');
SELECT * FROM execution_components_details;
```
```sql
INSERT INTO order_ (order_id, equipment_id, client_id, tab_number_master, order_status_id, execution_code) 
VALUES ('546', '1', '542353', '1', '1', '15'),
('653', '2', '655343', '2', '2', '25'),
('234', '3', '135446', '3', '3', '31'),
('122', '4', '766543', '4', '4', '34'),
('654', '5', '325655', '5', '5', '46');
SELECT * FROM order_;
```
```sql
INSERT INTO order_status (order_cod, name) 
VALUES ('1', 'принят'),
('2', 'проектирование'),
('3', 'в работе'),
('4', 'проверка'),
('5', 'готов');
SELECT * FROM order_status;
```
```sql
INSERT INTO post (post_cod, post) 
VALUES ('1', 'архитектор'),
('2', 'инженер-строитель'),
('3', 'технологов'),
('4', 'мастер монтажных и строительных работ'),
('5', 'электросварщик'),
('6', 'заведующий склада'),
('7', 'бригадир'),
('8', 'кладовщик'),
('9', 'комплектовщик'),
('10', 'грузчик');
SELECT * FROM post;
```
```sql
INSERT INTO staff (tab_number, family, post_cod, passport_series, passport_number, address, telephone, date_accepted) 
VALUES ('1', 'Крюков', '2', '4352', '430324', 'Омская область, город Балашиха, пер. Гагарина, 00', '+7 (929) 104-33-26', '2023-09-23'),
('2', 'Артемьев', '5', '6544', '534563', 'Пензенская область, город Кашира, шоссе Будапештсткая, 50', '+7 (929) 207-99-44', '2020-11-12'),
('3', 'Кузнецов', '3', '3254', '32543', 'Астраханская область, город Зарайск, пр. Космонавтов, 79', '+7 (932) 110-35-31', '2023-12-03'),
('4', 'Родионов', '4', '1453', '132433', 'Томская область, город Пушкино, ул. Косиора, 32', '+7 (907) 556-43-97', '2023-07-13'),
('5', 'Евдокимов', '6', '7645', '564321', 'Кировская область, город Павловский Посад, ул. Домодедовская, 46', '+7 (994) 420-75-66', '2023-01-04'),
('6', 'Семёнов', '10', '6453', '453221', 'Смоленская область, город Волоколамск, пл. Ладыгина, 55', '+7 (994) 437-52-69', '2023-04-08'),
('7', 'Лаврентьев', '10', '3253', '654321', 'Амурская область, город Талдом, ул. 1905 года, 73', '+7 (914) 529-81-62', '2022-10-22'),
('8', 'Стрелков', '9', '1214', '654322', 'Пензенская область, город Серебряные Пруды, спуск Славы, 94', '+7 (922) 312-22-75', '2022-07-10'),
('9', 'Самсонов', '8', '6543', '12453', 'Новосибирская область, город Шаховская, пр. Сталина, 54', '+7 (916) 783-26-32', '2023-12-21'),
('10', 'Агафонов', '7', '3254', '764343', 'Волгоградская область, город Серебряные Пруды, бульвар Косиора, 03', '+7 (947) 617-51-35', '2023-07-27');
SELECT * FROM staff;
```
# триггеры

-- первый тригер --
```sql
CREATE FUNCTION validate_telephone() RETURNS TRIGGER AS $$
BEGIN
IF NEW.telephone SIMILAR TO '^\+7 (\d{3}) \d{3}-\d{2}-\d{2}$' THEN
RETURN NEW;
ELSE
RAISE EXCEPTION 'Invalid telephone number format';
END IF;
END;
$$
LANGUAGE 'plpgsql';

CREATE TRIGGER check_telephone BEFORE INSERT OR UPDATE ON client FOR EACH ROW EXECUTE FUNCTION validate_telephone();
```
![image](https://github.com/paramka0/db_practice/assets/74873667/20e63a38-2235-40cd-aafb-33b2b94e2b79)











