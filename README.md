# Oracle SQL Cheatsheet

This Repository contains the basics of oracle sql for quick references

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

/* delete table */
DROP TABLE students;
```

**Altering Table and Columns**

```sql
/* add a new column */
ALTER TABLE students ADD(location VARCHAR2(30));

/* make email id primary key*/
ALTER TABLE students ADD CONSTRAINT empk PRIMARY KEY(email);

/* modify a particular column */
ALTER TABLE students MODIFY(branch VARCHAR2(5));
```

**Updating values in a Table**

```sql
/* update the location of a student */
UPDATE students SET location='nanganllur' WHERE email='luffy@gmail.com';
```

**Filtering**

```sql
/* filtering students based on branch */
SELECT * FROM students WHERE branch='csbs';

/*(selection and projection) */
SELECT name from students WHERE branch='csbs';

/* selecting multiple columns as a single column */
SELECT name||' - '||email FROM students;

/* using alias to change column title */
SELECT name||' - '||email AS "Basic Student Info" FROM students;

/* return all unique departments */
SELECT DISTINCT dept FROM students;

/* Second letter of the student name should be z */
SELECT * FROM students WHERE name LIKE '_z%';

/* second letter should be 'a' and last letter should be 'i' */
SELECT * FROM students WHERE name LIKE '_a%i';

/* Between */
SELECT name FROM students WHERE marks BETWEEN 50 AND 80;
```

**Constraints**

```sql
/* Column Constraint */
CREATE TABLE students(
name VARCHAR2(50) NOT NULL,
email VARCHAR2(100) CONSTRAINT email_uniq UNIQUE NOT NULL,
id NUMBER(5) CONSTRAINT pk PRIMARY KEY,
dept VARCHAR2(10) DEFAULT('CSBS'),
mark NUMBER(3)
);

/* Table Constraint (Composite Primary Key)*/
CREATE TABLE ENROLL(
student_id NUMBER(3),
course_id NUMBER(3),
CONSTRAINT pk PRIMARY KEY (student_id,course_id)
);

/* CHECK Constraint*/
CREATE TABLE students(
name VARCHAR2(30),
marks NUMBER(3) CONSTRAINT chk_mark CHECK (marks >= 0 AND marks <= 100)
);


/* FOREIGN KEY */
/* Creating user table */
CREATE TABLE passenger(
username VARCHAR2(20),
passenger_id NUMBER NOT NULL,
phone VARCHAR2(10),
CONSTRAINT user_pk PRIMARY KEY(passenger_id)
);

/* Foreign Key Table */
CREATE TABLE trains(
train_id NUMBER,
trainname VARCHAR2(20),
passengers NUMBER,
CONSTRAINT train_pk PRIMARY KEY(train_id),
CONSTRAINT train_pass_fk FOREIGN KEY (passengers) REFERENCES passenger(passenger_id)
);

```

**Delete**

```sql
/* DELETE */
DELETE FROM students WHERE id=2;

/* DELETE all rows from table */
TRUNCATE TABLE students;
```

**Order By**

```sql
/* ascending order of marks */
SELECT * FROM students ORDER BY mark;

/* descending order of marks */
SELECT * FROM students ORDER BY mark desc;
```

**Dual Table**

dual is a dummy table that can be used for doing some temporary operations

```sql
/* Displays 1 */
SELECT 1 FROM dual;

/* Displays Ashwin Prasad */
SELECT 'Ashwin '||'Prasad' FROM dual;
```

**String Manupulation**

```sql
/* To upper case */
SELECT UPPER('fly high') FROM dual;

/* To lower case */
SELECT LOWER('SAKURAMITSUTSUKI') FROM dual;

/* First letter Upper */
SELECT INITCAP('hikariare') FROM dual;

/* Concatenate 2 strings */
SELECT CONCAT('Monkey ','D Luffy') FROM dual;

/* prints given range of characters from a string */
SELECT SUBSTR('Imagination',6) FROM dual;

/* Optional 3rd parameter */
SELECT SUBSTR('Imagination',6,3) FROM dual;

/* returns Length of string */
SELECT LENGTH('spyair') FROM dual;

/* checks if a string is a substring of another string  */
SELECT INSTR('Erwin Smith','win') FROM dual;

/* Left Padding for encrypt */
SELECT LPAD('91765',10,'*') FROM dual;

/* Right Padding for encrypt */
SELECT RPAD('91765',10,'*') FROM dual;

/* TRIM */
SELECT TRIM('              Oracle vs mysql            ') FROM dual;

/* Replace */
SELECT REPlACE('Network Model','network','hierarchical') FROM dual;

/* Convert student names to upper case */
UPDATE students SET sname = UPPER(sname);
```

**Copy Original to Duplicates**
```sql 
/* create table students */
CREATE TABLE original(
    name VARCHAR2(50),
    age NUMBER(2),
    school VARCHAR2(100),
    mark NUMBER(3)
);

/* Insert Into Table original  */
INSERT ALL
INTO original(name,age,school,mark) VALUES('ashwin',19,'Modern',82)
INTO original(name,age,school,mark) VALUES('luffy',21,'east blue',12)
INTO original(name,age,school,mark) VALUES('zoro',25,'Wano Kuni',64)
INTO original(name,age,school,mark) VALUES('Sanji',25,'All Blue',92)
INTO original(name,age,school,mark) VALUES('nami',21,'Fishmen',96)
INTO original(name,age,school,mark) VALUES('robin',26,'poneglyphs',100)
SELECT 1 FROM dual;

/* duplicate table */
CREATE TABLE duptable(
    name VARCHAR2(50),
    age NUMBER(2),
    school VARCHAR2(100),
    mark NUMBER(3)
);

/* copy original to duptable */
INSERT INTO duptable(SELECT * FROM original);

/* Print duplicate table rows */
SELECT * FROM duptable;
```