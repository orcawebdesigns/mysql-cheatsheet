# 1.Login into mysql from terminal
- You need to get into your root directory and run the mysql command.

```
/var/www/html$ sudo mysql -u root -p
```

# 2. Show MySQL Users
 - Now you would be logged into the mysql database and there you can run the these commands.

 ```
 SELECT user FROM mysql.user;
 ```
# 3.CREATE USERS

```
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
```

# 4.GRANT PRIVILEGES, Show granted privileges and remove.
#### GRANT PRIVILEGES

```
GRANT ALL PRIVILEGES ON * . * TO 'user_name'@'localhost';
FLUSH PRIVILEGES;
```
#### Show Grants

```
    mysql> GRANT ALL PRIVILEGES ON database_name.* TO 'username'@'localhost';
 ```
#### Remove Grants

```
REVOKE ALL PRIVILEGES, GRANT OPTION FROM 'someuser'@'localhost';
```
 

 # 5.How to SHOW, DELETE & CREATE DATABASES & SELECT DATABASES
#### Show Databases
 ```
  mysql>SHOW {DATABASES | SCHEMAS}
    [LIKE 'pattern' | WHERE expr]
    
 mysql>SHOW DATABASE;
 
```
#### Create Database

```
 mysql>CREATE DATABASE database_name;
```
#### Select Database

```
 mysql> use database_name;
```
# 6.CREATE a TABLE with Columns and their data types

# Create Table

```
CREATE TABLE users(
id INT AUTO_INCREMENT,
   first_name VARCHAR(100),
   last_name VARCHAR(100),
   email VARCHAR(50),
   password VARCHAR(20),
   location VARCHAR(100),
   dept VARCHAR(100),
   is_admin TINYINT(1),
   register_date DATETIME,
   PRIMARY KEY(id)
);
```

# 7.Insert ROWS & RECORDS (single and multiple)

# Single
```
INSERT INTO users (first_name), values ('Robbie');
```
# Multiple
```
INSERT INTO users (first_name, last_name, email, password, location, dept, is_admin, register_date) values ('Bradley', 'Nowell', 'email@gmail.com', '123456','nelson', 'web-development program', 1, now());
```
# 8.SELECT with the WHERE Clause

```
SELECT * FROM users WHERE city='nelson';
SELECT * FROM users WHERE location='santa cruz' AND dept='investing';
SELECT * FROM users WHERE is_admin = 1;
SELECT * FROM users WHERE is_admin > 0;
```
# 9. SELECT with the WHERE Clause using a range

```
SELECT * FROM users WHERE age BETWEEN 30 AND 45;
```
# 10. DELETE an individual ROW

```
 DROP TABLE tablename;
 ```
 # 11. UPDATE a ROW
 
 ```
 UPDATE users SET email = 'email@gmail.com' WHERE id = 3;
```
# How to add a new column and modify it

```
ALTER TABLE users ADD age VARCHAR(33);
ALTER TABLE users MODIFY COLUMN age INT(33);
```
# 12.Order by and use Distinct

```
SELECT * FROM users ORDER BY last_name ASC;
SELECT * FROM users ORDER BY last_name DESC;

SELECT DISTINCT location FROM users;
 ```
 # 14.Concatenate Columns
 
 ```
 SELECT CONCAT(first_name, ' ', last_name) AS 'Name', dept FROM users;
```
# 15.Select Distinct Rows

```
SELECT DISTINCT location FROM users;
```
#  16.LIKE to Search

```
 SELECT * FROM users WHERE dept LIKE 'd%';
SELECT * FROM users WHERE dept LIKE 'dev%';
SELECT * FROM users WHERE dept LIKE '%t';
SELECT * FROM users WHERE dept LIKE '%e%';
```
# 17.Select using IN

```
SELECT * FROM users WHERE dept IN ('design', 'crypto');
```
# 18.Create & Remove Index

```
CREATE INDEX LIndex On users(location);
DROP INDEX LIndex ON users;
```
# 19.Create Two Tables demonstrating a one to many relationship that shows a PK & FK


```
CREATE TABLE books (
  id serial,
  title varchar(100) NOT NULL,
  author varchar(100) NOT NULL,
  published_date timestamp NOT NULL,
  isbn char(12),
  PRIMARY KEY (id),
  UNIQUE (isbn)
);

CREATE TABLE reviews (
  id serial,
  book_id integer NOT NULL,
  reviewer_name varchar(255),
  content varchar(255),
  rating integer,
  published_date timestamp DEFAULT CURRENT_TIMESTAMP,
  PRIMARY KEY (id),
  FOREIGN KEY (book_id) REFERENCES books(id) ON DELETE CASCADE
);
```
# 20.Inner Join

```
SELECT
  users.first_name,
  users.last_name,
  posts.title,
  posts.content
FROM users
INNER JOIN posts
ON users.id = posts.user_id
ORDER BY posts.title;
```
# JOIN Multiple Tables

```
SELECT
comments.body,
posts.title,
users.first_name,
users.last_name
FROM comments
INNER JOIN posts on posts.id = comments.post_id
INNER JOIN users on users.id = comments.user_id
ORDER BY posts.title;
```



