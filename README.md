# assignment-8.2
1) Concat

emp_details = LOAD '/home/acadgild/ramesh/emp.txt' USING PigStorage(',')
   as (id:int, firstname:chararray, lastname:chararray, age:int, phone:chararray, city:chararray, grade:int);
emp_name_concat = foreach emp_details Generate CONCAT (firstname, lastname);
dump emp_name_concat;

2) Tokenize

emp1 = LOAD '/home/acadgild/ramesh/emp1.txt' USING PigStorage(',')
   as (id:int,name:chararray,age:int,city:chararray);

emp_token = foreach emp1 Generate Flatten(TOKENIZE(name)) as name;
dump = emp_token;

3) Sum

employee_group = Group emp_details all;
sum = foreach employee_group Generate 
   (emp_details.id,emp_details.firstname),SUM(emp_details.age);
dump sum;

4) Min

min = foreach employee_group Generate 
   (emp_details.id,emp_details.firstname),MiN(emp_details.age);
dump min;
5) Max
max = foreach employee_group Generate 
   (emp_details.id,emp_details.firstname),MAX(emp_details.age);
dump max;
6) Limit

limit_data = LIMIT emp_details 5; 
dump limit_data;

7) Store

 STORE emp_details INTO ' /home/acadgild/pig/ ' USING PigStorage (',');
8) Distinct

distinct_data = DISTINCT emp_details;

9) Flatten

emp_token = foreach emp1 Generate Flatten(TOKENIZE(name)) as name;
dump = emp_token;

10) IsEmpty

cogroup_data = COGROUP emp_details by age, emp1 by age;
isempty_data = filter cogroup_data by IsEmpty(emp_age);
dump isempty_data;   
