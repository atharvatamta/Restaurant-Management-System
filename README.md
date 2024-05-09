# Restaurant-Management-System

As a part of our University Curriculum, we made this project for Database Management Systems (DBMS) - ITE1003.<br>
This project contains theoretical as well as implementation in SQL.<br>

## Pre-requisite

Oracle SQL Server (or) Oracle Community Edition

## Contents

- Mini world and Project Description
- Basic structure
  - Functional requirements
  - Entity Relation (ER) diagram and constraints
  - Relational database schema
- Implementation
  - Creating tables
  - Inserting data
- Queries
  - Basic queries
  - PL/SQL function
  - Trigger function

## 1. Introduction

## 2. Basic Structure

### 2.1 FRequirement Analysis

To develop a successful Restaurant Management System, we need to analyze
the requirements of the system. The following are the primary requirements for
the system:

1. Menu Management: The system must have the ability to display the
menu, including the items, their prices, and descriptions.
2. Customer Management: The system should allow the staff to create
customer profiles and store their information, including their name,
contact details,etc.
3. Order Management: The system should provide features to place orders
and add more items to order.
4. Bill and Tips Management: The system should be able to generate bills
and also allow customers to tip the waiter.

### 2.2 Entity Relation Diagram

![ER diagram](https://private-user-images.githubusercontent.com/110754495/329217198-6e36fecd-658b-45c6-ba6c-496b0159b62f.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNTE2NjAsIm5iZiI6MTcxNTI1MTM2MCwicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjE3MTk4LTZlMzZmZWNkLTY1OGItNDVjNi1iYTZjLTQ5NmIwMTU5YjYyZi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxMDQyNDBaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lYzUyMmViY2U0NDhmNTE2MzRkM2VhMGFlM2E5NDNkOTRiZmQ3ZTk4MmM1MTIyZTNiYzk4NzNkYjZhNjgyZmM1JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.-bCnfC-ibjX0hrnz8aRM2SpDf5uFaSKS2uJhH_4wz1Q)

### 2.3 ER To Table
```sql
ER to Table
Relation ‘Places’
Customer:- cust_id , cust_fname , cust_lname, contact_no
Ord:- ord_no , ord_date , cust_id (FK)
Relation ‘Takes’
Ord:- ord_no , ord_date , waiter_id (FK)
Waiter:- waiter_id , waiter_name , waiter_lname
Relation ‘Tips’
Customer:- cust_id , cust_fname , cust_lname , contact_no
Waiter:- waiter_id , waiter_fname , waiter_lname
Tips:- cust_id (FK) , waiter_id (FK) , tip
Relation ‘Prepares’
Food:- item_no , item_name , item_type , item_price , item_stock ,
chef_id (FK)
Chef:- chef_id , chef_fname , chef_lname , chef_type
Relation ‘Generates’
Ord:- ord_no , ord_date
Bill:- bill_no , tot_price , tax , discount , net_payable , ord_no (FK)
Relation ‘Contains’
Food:- item_no , item_name , item_type , item_price , item_stock
Contains:- item_no (FK) , ord_no (FK)
Ord:- ord_no , ord_date

```

## 3. Implementation

You can directly copy and paste all the commands from the text given here into the SQL console to create and insert values into your table.

### 3.1 Creating Tables

```sql
    create table waiter(
waiter_id integer primary key,
waiter_fname varchar(50) not null,
waiter_lname varchar(50)
);
create table customer(
cust_id integer primary key,
cust_fname varchar(50) not null,
cust_lname varchar(50),
contact_no integer
);
create table tips(
waiter_id integer references waiter(waiter_id),
cust_id integer references customer(cust_id),
tips integer not null
);
create table ord(
ord_no integer primary key,
ord_date date not null,
cust_id integer references customer(cust_id),
waiter_id integer references waiter(waiter_id)
);
create table chef(
chef_id integer primary key,
chef_fname varchar(50) not null,
chef_lname varchar(50),
chef_type varchar(50) not null
);
create table food(
item_no integer primary key,
item_name varchar(50) not null,
item_type varchar(50) not null,
item_price integer not null,
item_stock integer
);
create table contains(
ord_no integer references ord(ord_no),
item_no integer references food(item_no)
);
create table prepares(
item_type varchar(50) primary key,
chef_id integer references chef(chef_id)
);
create table bill(
bill_no integer primary key,
tot_price integer not null,
tax float default 5,
discount integer default 0,
net_payable float as
(tot_price+(tot_price*tax/100)-(tot_price*discount/100)),
ord_no integer references ord(ord_no)
);
```

### 3.2 After Inserting Dummy Values

### Customer:

![ER diagram](https://private-user-images.githubusercontent.com/110754495/329220322-11579329-de37-4ec0-88fd-93d2c8d22ce7.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNTI2OTEsIm5iZiI6MTcxNTI1MjM5MSwicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjIwMzIyLTExNTc5MzI5LWRlMzctNGVjMC04OGZkLTkzZDJjOGQyMmNlNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxMDU5NTFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT02YmU3NjYzZmU4ZWRlMDYwY2I2YTEyYzQwM2U3MTY1ODA1ZmEwNThjZWVkNjJlNzc1MmE4ZGM3Y2U1ZTU1NDE3JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.VggxPOIDlERBYrla_1zvoEnfrdf2ca89pjTsWF0jqGk)

### Waiter:
![ER diagram](https://private-user-images.githubusercontent.com/110754495/329220556-130add6b-c12c-4a2d-8c64-2d1b2553557a.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNTIyNDQsIm5iZiI6MTcxNTI1MTk0NCwicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjIwNTU2LTEzMGFkZDZiLWMxMmMtNGEyZC04YzY0LTJkMWIyNTUzNTU3YS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxMDUyMjRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT00NzRlN2M5MDY4ZGNiMDI0ZmIyOTIwNmY1NmM5YzkzMjE5YTg3OWQ3OTZjNDAwYjJlMjQ4MmUzMDUxZTAyOTMzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.aFtXXXRYQ-UzRDGDRS0nV3b7h-7MX1gcTaECeeoPIQA)
### Tips:
![ER diagram](https://private-user-images.githubusercontent.com/110754495/329221275-aaf91580-d35a-465a-bb95-bdae4da1ff02.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNTMyOTIsIm5iZiI6MTcxNTI1Mjk5MiwicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjIxMjc1LWFhZjkxNTgwLWQzNWEtNDY1YS1iYjk1LWJkYWU0ZGExZmYwMi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxMTA5NTJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wNWM0ZjllN2UyZWVkZDRhZTc2ZmJlY2E3YzhlOTBhZjI2OTUxOTllYjY4YTU4OGY0NjdlMTQxZTBjZDZhZmNhJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.gzp_ZGhY33o8aBkO0nKL-9avwdD_t_6bzVngMsU-YXU)
### Food:
![ER diagram](https://private-user-images.githubusercontent.com/110754495/329221515-21287cb6-e950-489f-871b-959ba36aefba.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNTMyNDMsIm5iZiI6MTcxNTI1Mjk0MywicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjIxNTE1LTIxMjg3Y2I2LWU5NTAtNDg5Zi04NzFiLTk1OWJhMzZhZWZiYS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxMTA5MDNaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lYTY2NmNkN2I2ZmQ2ZmExNWFhNjdlNDA4YzkzZjI3OTQ4MjViZmRkZmY0NWJmZDUzNTYwMmViMjg5YjY0NTliJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.RCkY_92xHLnj1WFOjlNESZieMQaULTB-vqJj22-ZXQU)
### Chef:
![ER diagram](https://private-user-images.githubusercontent.com/110754495/329221742-c853eaf1-8857-4f09-ada4-d9132b2c2f27.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNTMxOTIsIm5iZiI6MTcxNTI1Mjg5MiwicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjIxNzQyLWM4NTNlYWYxLTg4NTctNGYwOS1hZGE0LWQ5MTMyYjJjMmYyNy5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxMTA4MTJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1lOWM4OWYwZWQzOGVjZjRkMmEzNGJiMzA1YzFkMGZmYjMwMDU4MDk3Y2MyMGQwODI1YjRkNWJhMjVjMWY2MDcwJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.aKq11dR_IukB8JSkrze2lPeM28sbhUnmGkojmwlIalw)
### Prepares:
![ER diagram](https://private-user-images.githubusercontent.com/110754495/329222206-cdc1dbdb-99a9-49d0-92b8-334fa6930ebb.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNTMxNjIsIm5iZiI6MTcxNTI1Mjg2MiwicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjIyMjA2LWNkYzFkYmRiLTk5YTktNDlkMC05MmI4LTMzNGZhNjkzMGViYi5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxMTA3NDJaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT05MDdhZGVkNTIxMmYzZGUxYTliNDc0OWJiOWYxNDhiY2YxN2Y4YzVhNzY0OGI1ODBkNDdkN2ExMzZjZTdhYzAxJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.6mo2kSczCZTxFzegVt8Qftu_OYko1bCSay_qwPSaf4M)
### Order:
![ER diagram](https://private-user-images.githubusercontent.com/110754495/329222535-8333d341-0f12-4a33-a538-e794883232d8.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNTMxMTUsIm5iZiI6MTcxNTI1MjgxNSwicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjIyNTM1LTgzMzNkMzQxLTBmMTItNGEzMy1hNTM4LWU3OTQ4ODMyMzJkOC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxMTA2NTVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT04YTAzMjUyZTdmZmQ5NWM0MjUxNmQzMGQ4ZGQ1NWI5MTBkMWMyMmM3OTE3Zjc0NGRiMjcyOTUzNjViYWE5YWE3JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.Z0QBBDco3_2XuCRdozwJDs_Lw6Pm0z1gYvSBebs4Lxs)
### Contains:
![ER diagram](https://private-user-images.githubusercontent.com/110754495/329222585-37aefd69-c2bd-4df8-801d-f49eeaf92811.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNTMwNDQsIm5iZiI6MTcxNTI1Mjc0NCwicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjIyNTg1LTM3YWVmZDY5LWMyYmQtNGRmOC04MDFkLWY0OWVlYWY5MjgxMS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxMTA1NDRaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1iMzQwOGZkNGRhMWZhMGIzMDZhNTUwZWYzZGE0MDQ1NmZhMGMyZTk3Y2I4ODYwMzkwOTFhZmNlY2E3ZmZkZjg2JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.W9FAJt0AxpawkFKnq55UZ7ww68ZjYYY1-btYPFHIAEI)
## 4. Queries

### 4.1 Basic Queries

#### If the customer wants to see details of product present in the cart

```sql
    select * from product where product_id in(
        select product_id from Cart_item where (Cart_id in (
            select Cart_id from Customer where Customer_id='cid100'
        ))
    and purchased='NO');
```

#### If a customer wants to see order history

```sql
    select product_id,Quantity_wished from Cart_item where (purchased='Y' and Cart_id in (select Cart_id from customer where Customer_id='cid101'));
```

#### Customer wants to see filtered products on the basis of size,gender,type

```sql
    select product_id, color, cost, seller_id from product where (type='jeans' and p_size='32' and gender='F' and quantity>0)
```

#### If customer wants to modify the cart

```sql
    delete from cart_item where (product_id='pid1001' and Cart_id in (select cart_id from Customer where Customer_id='cid100'));
```

#### If a seller stops selling his product

```sql
    delete  from seller where seller_id = 'sid100';
    update product set quantity = 00 where seller_id is NULL;
```

#### If admin want to see what are the product purchased on the particular date

```sql
    select product_id from cart_item where (purchased='Y' and date_added='12-dec-2018');
```
#### How much product sold on the particular date

```sql
    select count(product_id) count_pid,date_added from Cart_item where purchased='Y'  group by(date_added);
```
#### If a customer want to know the total price present in the cart

```sql
    select sum(quantity_wished * cost) total_payable from product p join cart_item c on p.product_id=c.product_id where c.product_id in (select product_id from cart_item where cart_id in(select Cart_id from customer where customer_id='cid101') and purchased=’Y’);
```
#### Show the details of the customer who has not purchased any thing

```sql
    Select * from customer where customer_id not in (select customer_id from Payment);
```
#### Find total profit of the website from sales.

```sql
    select sum(quantity_wished * cost * commission/100) total_profit from product p join cart_item c on p.product_id=c.product_id where purchased=’Y’;
```

### 4.2 PL/SQL function
#### Procedure which returns the type of product with  the cost less than the given cost

```sql
    create or replace procedure cost_filter(c in number,t in varchar)
    is
    cs product.cost%type;
    ty product.type%type;
    id product.product_id%type;
    cursor cf is
    select product_id,cost,type from product where cost<c and type=t;
    begin
    open cf;
    loop
    fetch cf into id,cs,ty;
    exit when cf%notfound;
    dbms_output.put_line('Product' || id || 'has cost ' || cs || ' and the type is' || ty);
    end loop;
    close cf;
    exception
    when no_data_found then
    dbms_output.put_line('Sorry no such products exist');
    end;

```

#### Function which returns total number of products which a particular seller sells

```sql
    create or replace function totalProducts(sId in varchar)
    return number
    is
    total number(2):=0;
    begin
    select count(*) into total
    from product
    where seller_id=sId;
    return total;
    end;
    /
```
Function execution:
```sql
    declare
    c number(2);
    begin
    c:=totalProducts('sid102');
    dbms_output.put_line('Total products is : '|| c);
    end;
```

#### Procedure which returns the total quantity of product with the given ID
Procedure with exception handling
```sql
    create or replace procedure prod_details(p_id in varchar)
    is
    quan number(2);
    begin
    select quantity into quan from product where product_id=p_id;
    exception
    when no_data_found then
    dbms_output.put_line('Sorry no such product exist !!');
    end;
    /
```
### 4.3 Triggers
#### Trigger that will execute before inserting new customer to database and inserting a new cartId to the cart_items table
Function to count number of cart items
```sql
    create or replace function numCartId(cd in varchar)
    return number
    is
    total number(2):=0;
    begin
    select count(*) into total
    from cart_item
    where cart_id=cd;
    return total;
    end;
    Trigger
    Create or replace trigger before_customer
    before insert
    on
    customer
    for each row
    declare
    c varchar(10);
    n number(2);
    begin
    c:= :new.cart_id;
    n:=numCartId(c);
    if n>0 then
    dbms_output.put_line('Sorry');
    end if;
    insert into cart values(c);
    end;
```
#### Trigger to update the total amount of user everytime he adds something to payment table
```sql
    create or replace function total_cost(cId in varchar)
    return number
    is
    total number(2) :=0;
    begin
    select sum(cost) into total from product,cart_item where product.product_id=cart_item.product_id and cart_id=cId;
    return total;
    end;

    create or replace trigger before_pay_up
    before insert
    on
    payment
    for each row
    declare
    total number(3);
    begin
    total :=total_cost(:new.cart_id);
    insert into payment values(:new.payment_id,:new.payment_date,:new.payment_type,:new.customer_id,:new.cart_id,total);
    end;
```
## Contributors
Do check the contributors to follow some awesome projects

- [@bhumijgupta](https://www.github.com/bhumijgupta)
- [@YashMeh](https://www.github.com/YashMeh)
- [@roney_b](https://www.github.com)

> Feel free to fork the repository and contribute to this project.
You made it till the end. Brofist :punch:!!!
