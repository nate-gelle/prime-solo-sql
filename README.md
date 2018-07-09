# prime-solo-sql

In this challenge, we’re going to practice performing SQL queries. This should help better solidify some concepts that were covered during lecture.

Assumptions
You are using Postico
You installed Postgres with homebrew
Postgres is currently running on your computer
Setup
Follow the instructions below before continuing with this challenge.

Create your database, table, and data
We are creating a bank database with a single table (accounts) and 8 records. Please follow the instructions below to create a new database with this table and data.

Open Postico, if needed.
Connect to localhost.
Click on the localhost tab/bar in the upper-left corner.
Create a bank database
Double-click the bank database to use it.
Double-click the 'SQL Query' icon to bring up the query window.
Paste the following query into the query box to create the accounts table and populate it with data. Remember to click the Execute query button.
CREATE TABLE accounts (
    user_id serial PRIMARY KEY,
    username character varying(12),
    city character varying(128),
    transactions_completed integer,
    transactions_attempted integer,
    account_balance numeric(12,2)
);

INSERT INTO accounts (username, city, transactions_completed, transactions_attempted, account_balance) VALUES ('shawn', 'chicago', 5, 10, 355.80),
('cherise', 'minneapolis', 9, 9, 4000.00),
('larry', 'minneapolis', 3, 4, 77.01),
('dallas', 'new york', 6, 12, 0.99),
('anthony', 'chicago', 0, 0, 0.00),
('travis', 'miami', 1, 100, 500000.34),
('davey', 'chicago', 9, 99, 98.04),
('ora', 'phoenix', 88, 90, 3.33),
('grace', 'miami', 7, 9100, 34.78),
('hope', 'phoenix', 4, 10, 50.17);
GitHub repo
Create a GitHub repo named “prime-solo-sql”.
Create a file called “database.sql”. You will store your responses to the exercise questions here. NOTE: This is merely a text file with a .sql extension.
Exercise
For each of the following questions

Write a comment that specifies which question you are answering. (SQL comments are two dashes, followed by text.)
Write the SQL query that answers the question, below that comment.
Example question and answer
-- 0. Get all the users
SELECT * FROM accounts;
Tasks
Get all users from Chicago.
Get all users with usernames that contain the letter a.
The bank is giving a new customer bonus! Update all records with an account balance of 0.00 and a transactions_attempted of 0. Give them a new account balance of 10.00.
Select all users that have attempted 9 or more transactions.
Get the username and account balance of the 3 users with the highest balances, sort highest to lowest balance. NOTE: Research LIMIT
Get the username and account balance of the 3 users with the lowest balances, sort lowest to highest balance.
Get all users with account balances that are more than $100.
Add a new record.
The bank is losing money in Miami and Phoenix and needs to unload low transaction customers: Delete users that reside in miami OR phoenix and have completed fewer than 5 transactions.

/////////////////////////////////////////////////////////////////
Next assignment
/////////////////////////////////////////////////////////////////

In this challenge, we’re going to practice performing SQL queries with multiple tables. This should help better solidify some concepts that were covered during lecture.

Assumptions
You are using Postico
Postgres is currently running on your computer
Setup
Follow the instructions below before continuing with this challenge.

Create your database, table, and data
We are creating a database with a multiple tables and records. Please follow the instructions below to create a new database with this table and data.

Open Postico, if needed
Connect to your server, if needed
Create a warehouse database
In the SQL query window, run the following queries.
Click on the OK tab/button to save your database
Open the SQL editor and run the following queries
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    first_name character varying(60),
    last_name character varying(80)
);

CREATE TABLE addresses (
    id SERIAL PRIMARY KEY,
    street character varying(255),
    city character varying(60),
    state character varying(2),
    zip character varying(12),
    address_type character varying(8),
    customer_id integer REFERENCES customers
);

CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    order_date date,
    total numeric(4,2),
    address_id integer REFERENCES addresses
);

CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    description character varying(255),
    unit_price numeric(3,2)
);

CREATE TABLE line_items (
    id SERIAL PRIMARY KEY,
    unit_price numeric(3,2),
    quantity integer,
    order_id integer REFERENCES orders,
    product_id integer REFERENCES products
);

CREATE TABLE warehouse (
    id SERIAL PRIMARY KEY,
    warehouse character varying(55),
    fulfillment_days integer
);

CREATE TABLE warehouse_product (
    product_id integer NOT NULL REFERENCES products,
    warehouse_id integer NOT NULL REFERENCES warehouse,
    on_hand integer,
    PRIMARY KEY (product_id, warehouse_id)
);

INSERT INTO customers 
VALUES (1, 'Lisa', 'Bonet'),
(2, 'Charles', 'Darwin'),
(3, 'George', 'Foreman'),
(4, 'Lucy', 'Liu');

INSERT INTO addresses 
VALUES (1, '1 Main St', 'Detroit', 'MI', '31111', 'home', 1), 
(2, '555 Some Pl', 'Chicago', 'IL', '60611', 'business', 1),
(3, '8900 Linova Ave', 'Minneapolis', 'MN', '55444', 'home', 2),
(4, 'PO Box 999', 'Minneapolis', 'MN', '55334', 'business', 3),
(5, '3 Charles Dr', 'Los Angeles', 'CA', '00000', 'home', 4),
(6, '934 Superstar Ave', 'Portland', 'OR', '99999', 'business', 4);

INSERT INTO orders 
VALUES (1, '2010-03-05', 88.00, 1),
(2, '2012-02-08', 23.50, 2),
(3, '2016-02-07', 4.09, 2),
(4, '2011-03-04', 4.00, 3),
(5, '2012-09-22', 12.99, 5),
(6, '2012-09-23', 23.00, 6),
(7, '2013-05-25', 39.12, 5);

INSERT INTO products 
VALUES (1, 'toothbrush', 3.00),
(2, 'nail polish - blue', 4.25),
(3, 'generic beer can', 2.50),
(4, 'lysol', 6.00),
(5, 'cheetos', 0.99),
(6, 'diet pepsi', 1.20),
(7, 'wet ones baby wipes', 8.99);

INSERT INTO line_items 
VALUES (1, 5.00, 16, 1, 1),
(2, 3.12, 4, 1, 2),
(3, 4.00, 2, 2, 3),
(4, 7.25, 3, 4, 4),
(5, 6.00, 1, 5, 7),
(6, 2.34, 6, 6, 5),
(7, 1.05, 9, 7, 5);

INSERT INTO warehouse VALUES (1, 'alpha', 2),
(2, 'beta', 3),
(3, 'delta', 4),
(4, 'gamma', 4),
(5, 'epsilon', 5);

INSERT INTO warehouse_product 
VALUES (1, 3, 0),
(1, 1, 5),
(2, 4, 20),
(3, 5, 3),
(4, 2, 9),
(4, 3, 12),
(5, 3, 7),
(6, 1, 1),
(7, 2, 4),
(6, 3, 88),
(6, 4, 3);
Entity Relationship Diagram (ERD)
See a diagram of the available entities and their relationships. https://docs.google.com/drawings/d/1eA7JJtCVDL0K45aVzbxIUrgWXHoKY5vv1jAhssC2c1A/edit

NOTE: Remember that a many-to-many relationship requires a join table, so the entities in the diagram may be missing some actual tables. Explore the tables in your database.

GitHub repo
Create a GitHub repo named “prime-group-joins”.
Create a file called “joins-solution.sql”. You will store your responses to the exercise questions here. NOTE: This is merely a text file with a .sql extension.
Exercise
For each of the following questions

Write a comment that specifies which question you are answering. (SQL comments are two dashes, followed by text.)
Write the SQL query that answers the question, below that comment.
Once one person writes half of the queries, switch off.
Example question and answer
-- 0. Get all the users
SELECT * FROM customers;
Tasks
Get all customers and their addresses.
Get all orders and their line items.
Which warehouses have cheetos?
Which warehouses have diet pepsi?
Get the number of orders for each customer. NOTE: It is OK if those without orders are not included in results.
How many customers do we have?
How many products do we carry?
What is the total available on-hand quantity of diet pepsi?

