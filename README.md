# Zomato-Project

We will analyse the sql zomato database
Q. what is the total amount each customer spent on zomato?
Q. How many days has each customer visited zomato.
Q. what was the first product purchased by each customer?
Q. what is the most purchased item in the menu and how many times was it purchased by each customer?


Find the solutions here


create database Y

use Y

CREATE TABLE goldusers_signup(userid integer,gold_signup_date date); 

INSERT INTO goldusers_signup(userid,gold_signup_date) 
 VALUES (1,'09-22-2017'),
(3,'04-21-2017');

CREATE TABLE userst(userid integer,signup_date date); 

INSERT INTO userst(userid,signup_date) 
 VALUES (1,'09-02-2014'),
(2,'01-15-2015'),
(3,'04-11-2014');

CREATE TABLE sales(userid integer,created_date date,product_id integer); 

INSERT INTO sales(userid,created_date,product_id) 
 VALUES (1,'04-19-2017',2),
(3,'12-18-2019',1),
(2,'07-20-2020',3),
(1,'10-23-2019',2),
(1,'03-19-2018',3),
(3,'12-20-2016',2),
(1,'11-09-2016',1),
(1,'05-20-2016',3),
(2,'09-24-2017',1),
(1,'03-11-2017',2),
(1,'03-11-2016',1),
(3,'11-10-2016',1),
(3,'12-07-2017',2),
(3,'12-15-2016',2),
(2,'11-08-2017',2),
(2,'09-10-2018',3);

CREATE TABLE product(product_id integer,product_name text,price integer); 

INSERT INTO product(product_id,product_name,price) 
 VALUES
(1,'p1',980),
(2,'p2',870),
(3,'p3',330);

select * from sales;
select * from product;
select * from goldusers_signup;
select * from userst;

Q. what is the total amount each customer spent on zomato?

select
A.userid,
sum(B.price)

from sales as A
left join
Product as B
on
A.product_ID=B.product_ID
group by A.userid
order by 1 desc


Q. How many days has each customer visited zomato.

select
userid,
count(created_date)
from sales
group by userid

Q.what was the first product purchased by each customer?

with happy as
(
select
A.userid, A.created_date, A.product_id,
B.product_name,
DENSE_RANK() over (partition by A.userid order by A.created_date asc) as JPJ
from sales as A
left join
product as B
on A.product_id=B.product_id)
select userid, created_date, product_id, product_name  from happy where JPJ = 1

select * from (select *, dense_rank() over (partition by userid order by created_date) as AAD from sales) a where AAD = 1

Q.what is the most purchased item in the menu and how many times was it purchased by each customer?


select
userid,
product_id,
count(*) as PP
from sales
group by userid,
product_id
order by pp desc

select top 1
product_id,
count(*) GG
from sales
group by product_id
order by GG desc

use [practice 4]

select * from information_schema.tables
