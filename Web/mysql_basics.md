1. `sudo apt install mysql-server`
2. `sudo systemctl status mysql`
3. `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password'`
4. `sudo mysql_secure_installation`
5. `sudo mysql -u root -p`
6. `sudo mysql`
7. `sudo snap install mysql-workbench-community`

```
CREATE DATABASE xyz;
USE XYZ;

CREATE TABLE employee(
id INT PRIMARY KEY,
name VARCHAR(50),
salary INT);

INSERT INTO employee
(id,name,salary)
VALUES
(1,'Praveenraj R S',2500),
(2,'Raj R S',3000);

SELECT * FROM employee
```

### DB: Hotel, Table: Customers
```sql
CREATE DATABASE Hotel;
USE Hotel;

CREATE TABLE Customers(
CustomerID int Primary key,
CustomerName varchar(100),
CustomerNumber Varchar(10));

SELECT * FROM Customers;

INSERT INTO Customers(CustomerID, CustomerName, CustomerNumber)
VALUES
(1,"Praveen","8610008619"),
(2,"Raj","1234567890"),
(3,"Raj","0987654321");

SELECT * FROM Customers;
SELECT CustomerName, CustomerID FROM Customers;

SELECT DISTINCT CustomerName FROM Customers;
SELECT COUNT(DISTINCT CustomerName) FROM Customers;
```