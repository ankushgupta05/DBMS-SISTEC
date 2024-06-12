####  create user

```
CREATE USER ankush
IDENTIFIED BY sistec
```



#### create  user and then login from that user name and then write below code
```
CREATE TABLE student(
 first_name VARCHAR(15),
 last_name VARCHAR(10),
 roll_number NUMBER(10)
)


// output :-   'insufficient privileges'
```



#### login sys user and give privilege to the create user
```
GRANT create session, create table, create sequence, create view
TO ankush
```



#### login sys user and give space to the create user
```
ALTER USER ANKUSH quota 200M on system
```

#### now 'ankush' user can create table 
```
CREATE TABLE student(
 first_name VARCHAR(15),
 last_name VARCHAR(10),
 roll_number NUMBER(10)
)

```



### roll assign to the users
```
// create user 1
CREATE USER ankush1
IDENTIFIED BY sistec

// create user 2
CREATE USER ankush
IDENTIFIED BY sistec


// create roll
CREATE ROLE manager;

// assign feature to the roll
GRANT create table, create view 
TO manager


//  give privileges to the user both
GRANT manager TO ankush1, ankush2
```

### object privileges

#### privileges on select clause
```
//login user'ankush1'and run below code but  below code give error bcz 'ankush1' not have privileges
SELECT * FROM HR.employees;


//  give privileges to the users
GRANT select
ON employees
TO ankush,ankush1,ankush2


// now beoly code successfully execute
SELECT * FROM HR.employees;
```




#### privileges on update clause
```
GRANT update(department_name)
ON employees
TO ankush,ankush1,ankush2

```



### passing On your privileges
```
```




```
```




```
```




```
```




```
```




```
```

