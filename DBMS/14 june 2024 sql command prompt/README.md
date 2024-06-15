
#### run on sql command prompt  and only run one time
```
sql plus
```


#### run on sql command prompt and start server 
```
SET SERVEROUTPUT ON

```

#### fisrt you Login as a hr or sys 
```
connect hr
password hr
```



#### NOTE :- cursor work in sql result that means it very fast

```
declare
  cursor c1 is select first_name, salary from employees;
  vename employees.first_name%type;
  vsal employees.salary%type;
  begin
    open c1;
  loop
   fetch c1 into vename, vsal;
   exit when c1%notfound;
 dbms_output.put_line(vename ||' '||vsal);
 end loop;
 close c1;
 end;
 /
                    
```


```

declare
  cursor c1 is select * from employees;
  r employees%rowtype;
  begin
    open c1;
  loop
   fetch c1 into r;
   exit when c1%notfound;
 dbms_output.put_line(r.first_name ||' '|| r.salary);
 end loop;
 close c1;
 end;
 /

```


#### cursor foor loop

```
declare
  cursor c1 is select * from employees;
  begin
  FOR r in c1
  loop
 dbms_output.put_line(r.first_name ||' '|| r.salary);
 end loop;
 end;
 /


```




#### create table and insert value
```
CREATE TABLE emp4(
ename VARCHAR(5),
sal NUMBER(6,2)
)

// insert row into emp4

SQL> insert into emp4 values('&ename',&sal);
Enter value for ename: A
Enter value for sal: 100
old   1: insert into emp4 values('&ename',&sal)
new   1: insert into emp4 values('A',100)

1 row created.

SQL> insert into emp4 values('&ename',&sal);
Enter value for ename: B
Enter value for sal: 200
old   1: insert into emp4 values('&ename',&sal)
new   1: insert into emp4 values('B',200)

1 row created.

SQL> insert into emp4 values('&ename',&sal);
Enter value for ename: C
Enter value for sal: 300
old   1: insert into emp4 values('&ename',&sal)
new   1: insert into emp4 values('C',300)

1 row created.
```

#### check your database of emp4 values
```
declare
  cursor c1 is select * from emp4;
  begin
  FOR r in c1
  loop
 dbms_output.put_line(r.ename ||' '|| r.sal);
 end loop;
 end;
 /

```


#### update emp4 values
```
declare
  cursor c1 is select * from emp4;
  begin
  FOR r in c1
  loop
  update emp4 set sal = r.sal + 1000 where ename = r.ename;
 end loop;
 end;
 /
```


#### again check your database of emp4 values
```
declare
  cursor c1 is select * from emp4;
  begin
  FOR r in c1
  loop
 dbms_output.put_line(r.ename ||' '|| r.sal);
 end loop;
 end;
 /

```


#### update emp4 values but this genrates errors explore it
```
declare
  cursor c1 is select * from emp4 update of sal nowait;
  begin
  FOR r in c1
  loop
  update emp4 set sal = r.sal + 1000 where current of c1;
 end loop;
 end;
 /
```
 



