# Ex. No: 5 Creating Triggers using PL/SQL
## Date: 01/09/23
## AIM: 
To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
```
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suju','SALES',500000)
```
### Create employee table

![270734960-ab8e1001-ad81-4cee-b147-9e6ccbffe6b7](https://github.com/22008539/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/118707617/7f887113-48aa-43c5-bdcc-3a4a0a643eb0)

### Create salary_log table

![270735026-86466cf5-53f7-4063-9ccc-e364e7072d5e](https://github.com/22008539/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/118707617/7987da0b-8dc0-420b-bb4e-23643ed65255)
### PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employed
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employed values(1,'Shakthi','IT',1000000);
insert into employed values(2,'Suju','SALES',500000);

-- Update the salary of an employee
UPDATE employed
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employed;

-- Display the salary_log table
SELECT * FROM sal_log;
```

### Output:

![270736789-98d6405f-b231-485b-b7c5-38e605977906](https://github.com/22008539/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/118707617/7178a54e-f4a9-4607-8ef9-02e860c29eb9)
![270736840-c1caabb7-a19c-44b3-9343-e135eafc4d07](https://github.com/22008539/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/118707617/8b74b550-2a12-4dc4-a724-e65b8b9d6fa7)

## Result:
The program has been implemented successfully...
