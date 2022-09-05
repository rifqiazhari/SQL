# ER DIAGRAM
![alt text](Screenshot(604).png)
![alt text](Screenshot(605).png)
![alt text](Screenshot(606).png)
![alt text](Screenshot(607).png)
![alt text](Screenshot(608).png)
# SQL
CREATE TABLE Employee (
    emp_id INT PRIMARY KEY,
    first_name VARCHAR(30),
    last_name VARCHAR(30),
    birth_date DATE,
    sex VARCHAR(1),
    salary INT,
    supervis_id INT,
    branch_id INT
);

CREATE TABLE Branch (
    branch_id INT PRIMARY KEY,
    branch_name VARCHAR(30),
    mgr_id INT,
    mgr_start_date DATE,
    FOREIGN KEY(mgr_id) REFERENCES Employee(emp_id) ON DELETE SET
);

CREATE TABLE Client (
    client_id INT PRIMARY KEY,
    client_name VARCHAR(30),
    branch_id INT,
    FOREIGN KEY(branch_id) REFERENCES Branch(branch_id) ON DELETE SET NULL
);


ALTER TABLE Employee
ADD FOREIGN KEY(supervis_id)
REFERENCES Employee(emp_id)
ON DELETE SET NULL;

ALTER TABLE Employee
ADD FOREIGN KEY(branch_id)
REFERENCES Branch(branch_id)
ON DELETE SET NULL;

CREATE TABLE Works_With(
    emp_id INT,
    client_id INT,
    total_sales INT,
    PRIMARY KEY (emp_id, client_id),
    FOREIGN KEY(emp_id) REFERENCES Employee(emp_id) ON DELETE CASCADE,
    FOREIGN KEY(client_id) REFERENCES Client(client_id) ON DELETE CASCADE
);

CREATE TABLE Branch_Supplier(
    branch_id INT,
    supplier_name VARCHAR(30),
    supply_type VARCHAR(30),
    PRIMARY KEY (branch_id, supplier_name),
    FOREIGN KEY(branch_id) REFERENCES Branch(branch_id) ON DELETE CASCADE
);

-- Corporate
INSERT INTO Employee VALUES(100, 'David', 'Wallace', '1967-11-17', 'M', 250000, NULL, NULL);
INSERT INTO Branch VALUES(1, 'Corporate', 100, '2006-02-09');

UPDATE Employee --DUA ARAH
SET branch_id = 1
WHERE emp_id = 100;

INSERT INTO Employee VALUES(101, 'Jan', 'Levinson', '1961-05-11', 'F', 110000, 100, 1);

-- Scranton
INSERT INTO Employee VALUES(102, 'Michael', 'Levinson', '1964-03-15', 'M', 75000, 100, NULL);
INSERT INTO Branch VALUES(2, 'Scranton', 102, '2006-02-09');

UPDATE Employee--DUA ARAH
SET branch_id = 2
WHERE emp_id = 102;

INSERT INTO Employee VALUES(103, 'Angela', 'Martin', '1971-06-25', 'F', 63000, 102, 2);
INSERT INTO Employee VALUES(104, 'Kelly', 'Kapoor', '1980-02-05', 'F', 55000, 102, 2);
INSERT INTO Employee VALUES(105, 'Stanley', 'Hudson', '1958-02-19', 'M', 69000, 102, 2);

-- Stamford
INSERT INTO Employee VALUES(106, 'Josh', 'Porter', '1969-09-05', 'M', 78000, 100, NULL);
INSERT INTO Branch VALUES(3, 'Stamford', 106, '1998-02-13');

UPDATE Employee--DUA ARAH
SET branch_id = 3
WHERE emp_id = 106;

INSERT INTO Employee VALUES(107, 'Andy', 'Bernard', '1973-07-22', 'M', 65000, 106, 3);
INSERT INTO Employee VALUES(108, 'Jim', 'Halpert', '1978-10-01', 'M', 71000, 106, 3);


# Trigger
![alt text](Screenshot (614).png)<br/>
create table trigger_test(
	message VARCHAR(100)
);

DELIMITER $$
create
	trigger triggername before insert 
	on employee
	for each row begin
		insert into trigger_test values('added new employee');
	end$$
DELIMITER ;

insert into employee
values(120,'Oscar', 'Martinez', '1968-02-19', 'M', 69000, 106, 3);

select * from employee;
use girrafe;

select * from trigger_test ;

DELIMITER $$
create
	trigger triggername2 before insert 
	on employee
	for each row begin
		insert into trigger_test values(new.first_name);
	end$$
DELIMITER ;

insert into employee
values(122,'Udatna', 'Martinez', '1968-02-19', 'M', 69000, 106, 3);

insert into employee
values(123,'Mbaku', 'Martinez', '1968-02-19', 'M', 69000, 106, 3);
