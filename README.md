# Restaurant-Management-System

As a part of our University Curriculum, we made this project for UCS310.This system offers an array of features, including menu browsing, personalized customer profiles, seamless order placement, convenient tipping options, and additional functionalities tailored to enhance the dining experience.
This project contains **theoretical** as well as **implementation** in SQL.<br>

## Contents

- Requirement Analysis
- Basic structure
  - Functional requirements
  - Entity Relation (ER) diagram and constraints
  - Relational database schema
- Implementation
  - Creating tables
  - Inserting data
- Queries
  - PL/SQL function
  - Trigger function

## 1. Introduction
Restaurant Management System is a crucial tool for the hospitality industry that
enables restaurants to manage their operations efficiently. It offers numerous
functionalities that help restaurants to streamline their operations and provide
better services to their customers. In this project, we aim to develop a
Restaurant Management System using SQL and PL/SQL. The system will provide
features such as showing the menu, creating customer profiles, placing orders,
giving tips, and more.

## 2. Basic Structure

### 2.1 Requirement Analysis

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


![ER diagram](https://user-images.githubusercontent.com/110754495/329228533-d771b9b4-9ed0-485d-9299-7b626cf5aeb4.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNjM4MDksIm5iZiI6MTcxNTI2MzUwOSwicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjI4NTMzLWQ3NzFiOWI0LTllZDAtNDg1ZC05Mjk5LTdiNjI2Y2Y1YWViNC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxNDA1MDlaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT1iZDllODlkNDJkZDM5NThkMDc3NGY1YmY2NDU0MTUxN2IwMGM0NTAwYjc2NjUxNDk0ZTMxMDhmZGQ3MzgwMDUyJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.UgwYDT4-cxkEZabgqCz5uzwrKelsiFWKJbXyIR9zrzE)


## ER to Table:
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

![Open folder DBMS PROJECT 7](https://github.com/atharvatamta/Restaurant-Management-System/assets/110754495/b8d85e6b-ff1d-4d7e-8523-7a0b3923ac96)

### Waiter:
![Open folder DBMS PROJECT 6](https://github.com/atharvatamta/Restaurant-Management-System/assets/110754495/5a0fe2af-93c5-4eea-aa39-a6eaf5ba423c)
### Tips:
![Open folder DBMS PROJECT 5](https://github.com/atharvatamta/Restaurant-Management-System/assets/110754495/6d72af56-6de6-414f-8d73-36a91a830437)
### Food:
![Open folder DBMS PROJECT 4](https://github.com/atharvatamta/Restaurant-Management-System/assets/110754495/10aed6c5-66da-40da-9f4c-05526b7f7fc7)
### Chef:
![Open folder DBMS PROJECT 3](https://github.com/atharvatamta/Restaurant-Management-System/assets/110754495/e12eea04-9368-4565-b860-e04adbe1c7bd)

### Prepares:
![Open folder DBMS PROJECT](https://github.com/atharvatamta/Restaurant-Management-System/assets/110754495/47dc42d7-553f-4eac-b317-e0db7ac945f3)
### Order:
![IMG_B9BA7EED3A72-1](https://github.com/atharvatamta/Restaurant-Management-System/assets/110754495/acb49112-a692-414d-a262-c0db9e3bc575)

### Contains:
![Open folder DBMS PROJECT 2](https://github.com/atharvatamta/Restaurant-Management-System/assets/110754495/d64cf051-f6d1-4108-8293-95fa1a1a1a9a)
## 4. Queries



### 4.1 PL/SQL function


###1. show_menu procedure
Displays the items and their prices using a cursor.
```sql

declare
cursor c1 is select item_name,item_price from food;
rec1 c1%rowtype;
procedure show_menu is
begin
open c1;
loop
fetch c1 into rec1;
exit when c1% not found;
dbms_output.put_line('Item :'||rec1.item_name||' Price : '||rec1.item_price);
end loop;
close c1;
end;
begin
show_menu;
end;

```
### 2. get_cust_id Function
If a customer already exists then returns the existing ID else creates a new customer and returns the new ID.

```sql
declare
id integer;
if exists integer:=0;
function get_cust_id(fname in varchar, Iname in varchar, contact in integer) return number is
begin
select count(*) into if_exists from customer where cust_fname=fname and cust_Iname=Iname and contact_no=contact; 
if_exists>0 then
select cust_id into id from customer where cust_fname=fname and cust_lname=lname and contact_no=contact;
return(id);
else
select count(*)+1 into id from customer;
insert into customer values (id, fname, lname, contact); 
return(id);
end if;
end;
begin
id:=get_cust_id('Blake', 'Ryan', 900000004); 
dbms_output.put_line('Customer Id is' || id);
end;

```
3. Placing Order
a. in_stock trigger:
Before Inserting the food items in the order it checks if the items are in stock if they are not in stock it will raise an error.

This function inserts the items in the form of an array of item_no in the order and returns the order_no to the customer.
d. add_order procedure:
This function adds the items in the form of an array of item_no in the order of the given order_no.

```sql
create or replace trigger in_stock
before insert on contains for each row
declare
stock integer;
begin
select item_stock into stock from food where food.item_no=:new.item_no;
if stock=0 then raise_application_error(-20000, 'Out of Stock'); 
end if;
end;

```
b. after_order trigger:
After Inserting the food items in the order it updates the stock of the items and decreases them accordingly.


```sql
create or replace trigger after_order
after insert on contains for each row
begin
update food set item_stock=item_stock-1 where item_no=:new.item_no;
end;

```
c. place_order function:
This function inserts the items in the form of an array of item_no in the order and returns the order_no to the customer..


```sql

declare
type num_array is varray(50) of integer;
items num_array;
order_no integer;
function place_order (id in integer, items in num_array,wait_id in number) return integer is 
begin
select count(*)+1 into order_no from ord;
insert into ord values (order_no, sysdate, id,wait_id);
for i in 1..items.count loop
insert into contains values (order_no,items(i));
end loop;
return (order_no);
end;
begin
items:=num_array(1,2);
order_no:=place_order (4, items,3);
dbms_output.put_line ('Your Order No is '||order_no);
end;


```
d. add_order procedure:
This function adds the items in the form of an array of item_no in the order of the given order_no.

```sql
declare
type num_array is varray(50) of integer;
items num_array;
order_no integer;
procedure add_order(order_no in integer, items in num_array) is 
begin
for i in 1..items.count loop
insert into contains values (order_no, items (i));
end loop;
end;
```
After processing all the statements we can see in the contains table the order_no 4 has three items and stock has decreased by 1.
```sql
begin
items:=num_array(3);
add_order(4,items);
end;
```

(![ER diagram](https://private-user-images.githubusercontent.com/110754495/329263858-9421d61c-e965-4c77-aaaf-b766c73efe90.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MTUyNjIyMjUsIm5iZiI6MTcxNTI2MTkyNSwicGF0aCI6Ii8xMTA3NTQ0OTUvMzI5MjYzODU4LTk0MjFkNjFjLWU5NjUtNGM3Ny1hYWFmLWI3NjZjNzNlZmU5MC5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQwNTA5JTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MDUwOVQxMzM4NDVaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0yYjdjMGMwZjcwODU2YTVkYWJlOTFiNjlhOGQ1ZWRiZjI3NWI1OTIyMWExZTA0NTdmY2U2MWU3MzdhNDZhNjkzJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZhY3Rvcl9pZD0wJmtleV9pZD0wJnJlcG9faWQ9MCJ9.eM7vuqlcNwsdQVli293idCBa3uKrwuUd5Kz-yO0YCHM)
#### Generating Bill
a. display_bill trigger:
It displays the bill along with the bill_no,ord_no,items, price, total price, discount, tax and the net_payable amount to the customer.


```sql
create or replace trigger display_bill after insert on bill for each row
begin
dbms_output.put_line('Total Price: Rs.'||: new.tot_price);
dbms_output.put_line ('Tax: '||: new.tax||' %');
dbms_output. put_line('Discount: '||:new.discount|| '%'); 
dbms_output.put_line ('Net Payable Amount: Rs. '||: new.net_payable);
end;

```
b. generate_bill procedure:
```sql
declare
cursor c2 (n integer) is select f.item_no, f.item_name, f.item_price,c.ord_no from food f, contains c where f.item_no=c.item_no and c.ord_no=n;
rec2 c2 %rowtype;
total integer:=0;
b_no integer;
procedure generate_bill(order_no in integer, disc in float) is
begin
open c2(order_no);
select count(*)+1 into b_no from bill;
dbms_output.put_line ('Bill No: 'Ilb_noll' order_no: 'I lorder_no);
loop
fetch c2 into rec2;
exit when c2%notfound;
dbms_output.put_line ('Item: 'Il rec2.item_name||' Price: Rs.'|| rec2.item_price);
total:=total+rec2.item_price;
end loop;
if (total>1000) then
insert into bill (bill_no, tot_price, tax, discount, ord_no) values (b_no, total, 10, disc, order_no);
else
insert into bill (bill_no, tot_price, discount, ord_no) values (b_no, total, disc, order_no);
end if;
close c2;
end;



It takes in the values order_no and any discount value and inserts the given values into the bill table.
begin
generate_bill (4,0);
end;
```

#### Tips:
a. give_tip procedure:
It takes in the value of the tip given by the customer to the denoted waiter.


```sql
   declare
procedure give_tip(id in integer, wait_id in integer, t in integer) is
Begin
insert into tips values (wait_id,id,t);
dbms_output.put_line ('Waiter 3 Recieved Rs. '||t||' tip');
end;
begin
give tip(4,3,10);
end;
```

b. display_waiter_tip procedure:
It displays the total tips collected by a specific waiter.
```sql
declare
tot integer;
procedure display_waiter_tip (wait_id in integer) is
begin
select sum(tip) into tot from tips where waiter_id=wait_id;
dbms_output.put_line('Total tip for waiter id' ||wait_id || ' is Rs. '||tot);
end;
begin
display_waiter_tip(3);
end;
```
## Conclusion:
In conclusion, the Restaurant Management System is an essential tool for the
hospitality industry, and it provides numerous features to streamline
operations and provide better services to customers. Developing a
Restaurant Management System using SQL and PL/SQL is an excellent way
to build a reliable, robust, and scalable system that meets the requirements
of the restaurant industry.
However, while developing such a system, it is essential to consider the
system requirements, external requirements, and hardware requirements to
ensure that the system performs optimally and securely. By taking these
requirements into account, the Restaurant Management System will be able
to handle a large number of transactions and users, integrate with other
third-party systems, be accessible from multiple devices and platforms, and
comply with the relevant regulations and standards.
Moreover, the system will provide a seamless and intuitive user experience,
making it easy for the restaurant staff to navigate and perform their tasks.
The system will have a user-friendly interface with clear instructions and
prompts, ensuring that the staff can use it with minimal training.
In summary, developing a Restaurant Management System using SQL and
PL/SQL is an excellent investment for restaurants, as it will help them
manage their operations more efficiently, reduce errors, and provide better
services to their customers.


