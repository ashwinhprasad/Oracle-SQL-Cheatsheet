# SQL Cheatsheet

**Basic create, Insert and Display**

```sql
/* Create Table students */
CREATE TABLE students( name VARCHAR2(30), email VARCHAR2(50), dob DATE, branch VARCHAR2(10));

/* Insert values into table */
INSERT INTO students(name,email,dob,branch) VALUES('ashwin prasad','ashwinprasad202@gmail.com','09-Mar-2002','csbs');

/* Insert multiple rows */
INSERT ALL
INTO students(name,email,dob,branch) VALUES('johndoe','johndoe@gmail.com','01-Nov-2001','cse')
INTO students(name,email,dob,branch) VALUES('janedoe','janedoe@gmail.com','05-Dec-2000','csbs')
INTO students(name,email,dob,branch) VALUES('Luffy','luffy@gmail.com','21-Feb-2005','mech')
SELECT 1 FROM dual;

/* display all students from table */
SELECT * FROM students;
```
