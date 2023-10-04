# Ex. No: 5 Creating Triggers using PL/SQL

## AIM:
To create a Trigger using PL/SQL.

## Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

## Program:
```
CREATE TABLE employe(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE salary_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employe values(1,'Kar','IT',1000000);
insert into employe values(2,'Boha','SALES',500000)
```
## Create employee table
![image](https://github.com/Brindha77/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/118889143/3f321740-7209-4fa9-bb97-c8d1f861d5aa)

## Create salary_log table
![image](https://github.com/Brindha77/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/118889143/3ce554ad-7f85-4590-8112-0ff4d5f1e974)

## PLSQL Trigger code
```
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employe
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employe values(1,'Kar','IT',1000000);
insert into employe values(2,'Boha','SALES',500000);

-- Update the salary of an employee
UPDATE employe
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employe;

-- Display the salary_log table
SELECT * FROM sal_log;
```
## Output:
![db ex 5](https://github.com/Brindha77/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/118889143/40b9a2ab-e8d1-4712-8a18-786ac0bf690e)

## Result:
Thus the program for creating triggers has been implemented successfully.
