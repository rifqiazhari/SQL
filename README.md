# ER DIAGRAM
![alt text](Screenshot(604).png)
![alt text](Screenshot(605).png)
![alt text](Screenshot(606).png)
![alt text](Screenshot(607).png)
![alt text](Screenshot(608).png)
# SQL
`CREATE TABLE Employee (`<br/>
&emsp;&emsp;`emp_id INT PRIMARY KEY,`<br/>
&emsp;&emsp;`first_name VARCHAR(30),`<br/>
&emsp;&emsp;`last_name VARCHAR(30),`<br/>
&emsp;&emsp;`birth_date DATE,`<br/>
&emsp;&emsp;`sex VARCHAR(1),`<br/>
&emsp;&emsp;`salary INT,`<br/>
&emsp;&emsp;`supervis_id INT,`<br/>
&emsp;&emsp;`branch_id INT`<br/>
`);`<br/>

`CREATE TABLE Branch (`<br/>
&emsp;&emsp;`branch_id INT PRIMARY KEY,`<br/>
&emsp;&emsp;`branch_name VARCHAR(30),`<br/>
&emsp;&emsp;`mgr_id INT,`<br/>
&emsp;&emsp;`mgr_start_date DATE,`<br/>
&emsp;&emsp;`FOREIGN KEY(mgr_id) REFERENCES Employee(emp_id) ON DELETE SET`<br/>
`);`<br/>

`CREATE TABLE Client (`<br/>
&emsp;&emsp;`client_id INT PRIMARY KEY,`<br/>
&emsp;&emsp;`client_name VARCHAR(30),`<br/>
&emsp;&emsp;`branch_id INT,`<br/>
&emsp;&emsp;`FOREIGN KEY(branch_id) REFERENCES Branch(branch_id) ON DELETE SET NULL`<br/>
`);`<br/>


`ALTER TABLE Employee`<br/>
`ADD FOREIGN KEY(supervis_id)`<br/>
`REFERENCES Employee(emp_id)`<br/>
`ON DELETE SET NULL;`<br/>

`ALTER TABLE Employee`<br/>
`ADD FOREIGN KEY(branch_id)`<br/>
`REFERENCES Branch(branch_id)`<br/>
`ON DELETE SET NULL;`<br/>

`CREATE TABLE Works_With(`<br/>
&emsp;&emsp;`emp_id INT,`<br/>
&emsp;&emsp;`client_id INT,`<br/>
&emsp;&emsp;`total_sales INT,`<br/>
&emsp;&emsp;`PRIMARY KEY (emp_id, client_id),`<br/>
&emsp;&emsp;`FOREIGN KEY(emp_id) REFERENCES Employee(emp_id) ON DELETE CASCADE,`<br/>
&emsp;&emsp;`FOREIGN KEY(client_id) REFERENCES Client(client_id) ON DELETE CASCADE`<br/>
`);`<br/>

`CREATE TABLE Branch_Supplier(`<br/>
&emsp;&emsp;`branch_id INT,`<br/>
&emsp;&emsp;`supplier_name VARCHAR(30),`<br/>
&emsp;&emsp;`supply_type VARCHAR(30),`<br/>
&emsp;&emsp;`PRIMARY KEY (branch_id, supplier_name),`<br/>
&emsp;&emsp;`FOREIGN KEY(branch_id) REFERENCES Branch(branch_id) ON DELETE CASCADE`<br/>
`);`<br/>

`-- Corporate`<br/>
`INSERT INTO Employee VALUES(100, 'David', 'Wallace', '1967-11-17', 'M', 250000, NULL, NULL);`<br/>
`INSERT INTO Branch VALUES(1, 'Corporate', 100, '2006-02-09');`<br/>

`UPDATE Employee --DUA ARAH`<br/>
`SET branch_id = 1`<br/>
`WHERE emp_id = 100;`<br/>

`INSERT INTO Employee VALUES(101, 'Jan', 'Levinson', '1961-05-11', 'F', 110000, 100, 1);`<br/>

`-- Scranton`<br/>
`INSERT INTO Employee VALUES(102, 'Michael', 'Levinson', '1964-03-15', 'M', 75000, 100, NULL);`<br/>
`INSERT INTO Branch VALUES(2, 'Scranton', 102, '2006-02-09');`<br/>

`UPDATE Employee--DUA ARAH`<br/>
`SET branch_id = 2`<br/>
`WHERE emp_id = 102;`<br/>

`INSERT INTO Employee VALUES(103, 'Angela', 'Martin', '1971-06-25', 'F', 63000, 102, 2);`<br/>
`INSERT INTO Employee VALUES(104, 'Kelly', 'Kapoor', '1980-02-05', 'F', 55000, 102, 2);`<br/>
`INSERT INTO Employee VALUES(105, 'Stanley', 'Hudson', '1958-02-19', 'M', 69000, 102, 2);`<br/>

`-- Stamford`<br/>
`INSERT INTO Employee VALUES(106, 'Josh', 'Porter', '1969-09-05', 'M', 78000, 100, NULL);`<br/>
`INSERT INTO Branch VALUES(3, 'Stamford', 106, '1998-02-13');`<br/>

`UPDATE Employee--DUA ARAH`<br/>
`SET branch_id = 3`<br/>
`WHERE emp_id = 106;`<br/>

`INSERT INTO Employee VALUES(107, 'Andy', 'Bernard', '1973-07-22', 'M', 65000, 106, 3);`<br/>
`INSERT INTO Employee VALUES(108, 'Jim', 'Halpert', '1978-10-01', 'M', 71000, 106, 3);`<br/>


# Trigger
![alt text](Screenshot (614).png)<br/>
`create table trigger_test(`<br/>
&emsp;&emsp;`message VARCHAR(100)`<br/>
`);`<br/>

`DELIMITER $$`<br/>
`create`<br/>
&emsp;&emsp;`trigger triggername before insert `<br/>
&emsp;&emsp;`on employee`<br/>
&emsp;&emsp;`for each row begin`<br/>
&emsp;&emsp;&emsp;&emsp;`insert into trigger_test values('added new employee');`<br/>
&emsp;&emsp;`end$$`<br/>
`DELIMITER ;`<br/>

`insert into employee`<br/>
`values(120,'Oscar', 'Martinez', '1968-02-19', 'M', 69000, 106, 3);`<br/>

`select * from employee;`<br/>
`use girrafe;`<br/>

`select * from trigger_test;`<br/>

`DELIMITER $$`<br/>
`create`<br/>
&emsp;&emsp;`trigger triggername2 before insert`<br/>
&emsp;&emsp;`on employee`<br/>
&emsp;&emsp;`for each row begin`<br/>
&emsp;&emsp;&emsp;&emsp;`insert into trigger_test values(new.first_name);`<br/>
&emsp;&emsp;`end$$`<br/>
`DELIMITER ;`<br/>

`insert into employee`<br/>
`values(122,'Udatna', 'Martinez', '1968-02-19', 'M', 69000, 106, 3);`<br/>

`insert into employee`<br/>
`values(123,'Mbaku', 'Martinez', '1968-02-19', 'M', 69000, 106, 3);`<br/>
