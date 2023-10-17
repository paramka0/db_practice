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











