# Department Summary
 Description
 Given two tables, Employee and Department, generate a summary of how many employees are in each department. Each department should be listed, whether they currently have any employees or not. The results should be sorted from high to low by number of employees, and then alphabetically by department when departments have the same number of employees. The results should list the department name followed by the employee count. The column names are not tested, so use whatever is appropriate.

# Schema
 |---------------------------------------------------------------------------------------|
 |              EMPLOYEE                                                                 |
 |---------------------------------------------------------------------------------------|
 | Name	   | Type	  | Description                                                      |
 |---------|----------|------------------------------------------------------------------|
 | ID	   | Integer  | Employee ID number. This is a primary key                        |
 | NAME    | String   | Employee name                                                    |
 | SALARY  | Integer  | Employee salary                                                  |
 | DEPT_ID | Integer  |	ID of the employee's department, a foreign key to DEPARTMENT.ID  |
 

 |              DEPARTMENT                                     |
 |-------------------------------------------------------------|
 | Name      | 	Type   | Description                           |
 |-----------|---------|---------------------------------------|
 | ID	     | Integer | Department ID. This is a primary key  |
 | NAME	     | String  | Department name                       |
 | LOCATION	 |String   | Department location                   |

# Sample Data Tables
 |          EMPLOYEE               |
 |---------------------------------|
 | ID | NAME	| SALARY | DEPT_ID |
 |----|---------|--------|---------|
 | 1  | Candice	| 4685	 | 1       |
 | 2  | Julia	| 2559	 | 2       |
 | 3  | Bob	    | 4405	 | 4       |
 | 4  | Scarlet	| 2350	 | 1       |
 | 5  | Ileana	| 1151	 | 4       |
 
 | DEPARTMENT                  |
 |-----------------------------|
 | ID | NAME	   | LOCATION  |
 |----|------------|-----------|
 | 1  | Executive  | Sydney    |
 | 2  | Production | Sydney    |
 | 3  | Resources  | Cape Town |
 | 4  | Technical  | Texas     |
 | 5  | Management | Paris     |
 
# Sample Output
    Executive 2
    Technical 2
    Production 1
    Management 0
    Resources 0

# MySQl
    select d.name,count(e.id) as employee_count
    from department d
    left join employee e
    on d.id = e.dept_id
    group by d.id,d.name
    order by employee_count desc, d.name asc;

# Your Output (stdout) 
 +----------------------+----------------+
 | name                 | employee_count |
 +----------------------+----------------+
 | Product              |            132 |
 | Engineering          |            129 |
 | Legal                |            127 |
 | Sales                |            126 |
 | Recruitment          |            123 |
 | Finance              |            122 |
 | Research&Development |            122 |
 | Operations           |            119 |
 | Human Resources      |              0 |
 | Marketing            |              0 |
 +----------------------+----------------+

# Result
    The query is correct. Hidden test case passed.