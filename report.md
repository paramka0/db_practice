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

