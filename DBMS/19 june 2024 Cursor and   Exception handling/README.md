
#### perameterized cursor
```
DECLARE
e employees%rowtype;
CURSOR e_sal(low_salary NUMBER, high_salary NUMBER)
IS 
    SELECT *
    FROM employees
    WHERE SALARY BETWEEN low_salary AND high_salary;
BEGIN
    -- Low salary employees
    dbms_output.put_line('Low salary  employees');
    OPEN e_sal(2000,7000);
LOOP
    FETCH e_sal INTO e;
    EXIT WHEN e_sal%notfound;
    dbms_output.put_line(e.FIRST_NAME || ': '|| e.SALARY);
END LOOP;

    -- High salary employees
    dbms_output.put_line('High salary  employees');
    OPEN e_sal(8000,25000);
LOOP
    FETCH e_sal INTO e;
    EXIT WHEN e_sal%notfound;
    dbms_output.put_line(e.FIRST_NAME || ': '|| e.SALARY);
END LOOP;

CLOSE e_sal;

END;

/
```


#### default perameterzed  cursor
```
DECLARE
e employees%rowtype;
CURSOR e_sal(low_salary NUMBER :=2000, high_salary NUMBER :=7000)
IS 
    SELECT *
    FROM employees
    WHERE SALARY BETWEEN low_salary AND high_salary;
BEGIN
    -- Low salary employees
    dbms_output.put_line('Low salary  employees');
    OPEN e_sal;
LOOP
    FETCH e_sal INTO e;
    EXIT WHEN e_sal%notfound;
    dbms_output.put_line(e.FIRST_NAME || ': '|| e.SALARY);
END LOOP;

CLOSE e_sal;

END;

/

```




#### Nested cursor 

```
DECLARE 
    e_dept_no employees.department_id%TYPE;

    CURSOR cur_departments IS
        SELECT * 
        FROM departments;

    CURSOR cur_employees IS
        SELECT * 
        FROM employees e
        WHERE e.department_id = e_dept_no;

    v_deptrec departments%ROWTYPE;

    v_emprec employees%ROWTYPE;

BEGIN
    OPEN cur_departments;
    LOOP
        FETCH cur_departments INTO v_deptrec;
        exit WHEN cur_departments%NOTFOUND;
        e_dept_no := v_deptrec.department_id;


    dbms_output.put_line('-----------------------------');
    dbms_output.put_line('Department Name : '||v_deptrec.department_name);
    dbms_output.put_line('-----------------------------');

    OPEN cur_employees;
    LOOP
    FETCH cur_employees INTO v_emprec;
    exit WHEN cur_employees%NOTFOUND;
    dbms_output.put_line('Employees : '||v_emprec.first_name ||chr(9)||'Salary: '||v_emprec.salary);

    END LOOP;
    CLOSE cur_employees;

    END LOOP;
    CLOSE cur_departments;
END;
/
```



####  Exception Handling System defined
```
// code genrate error
DECLARE 
dividend NUMBER := 10;
divisor NUMBER := 0;
result NUMBER;

BEGIN
    BEGIN
    result := dividend/divisor;
    dbms_output.put_line('Result : ' || result);
    EXCEPTION
        WHEN ZERO_DIVIDE THEN
           dbms_output.put_line('Error : Division by Zero');
    END;
END;
/

```

#### Exception Handling System defined
```
// code not genrate error
DECLARE 
dividend NUMBER := 10;
divisor NUMBER := 5;
result NUMBER;

BEGIN
    BEGIN
    result := dividend/divisor;
    dbms_output.put_line('Result : ' || result);
    EXCEPTION
        WHEN ZERO_DIVIDE THEN
           dbms_output.put_line('Error : Division by Zero');
    END;
END;
/

```



#### Exception Handling System defined
```
// if user not exist than this code show error
DECLARE
emp_name VARCHAR2(100);
emp_id NUMBER :=225;

BEGIN
    BEGIN
    SELECT first_name INTO emp_name FROM employees WHERE employee_id = emp_id;
    dbms_output.put_line('Employees Name  : ' || emp_name);
    EXCEPTION
        WHEN NO_DATA_FOUND THEN
           dbms_output.put_line('Error : No matching record found');
    END;
END;
/
```



#### Exception Handling System defined
```
// if user not exist than this code not show error
DECLARE
emp_name VARCHAR2(100);
emp_id NUMBER :=100;

BEGIN
    BEGIN
    SELECT first_name INTO emp_name FROM employees WHERE employee_id = emp_id;
    dbms_output.put_line('Employees Name  : ' || emp_name);
    EXCEPTION
        WHEN NO_DATA_FOUND THEN
           dbms_output.put_line('Error : No matching record found');
    END;
END;
/
```
