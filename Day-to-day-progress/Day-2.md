# :computer:Day-2 :

:point_right: Introduction on Microsoft SQL server. <br>
:point_right: Learned about various [datatypes in MSSQL](https://www.w3schools.com/sql/sql_datatypes.asp).<br>
:point_right: Learned few basic commands like create, insert, update, delete :

<!-- Working in MSSQL but wrote MySQL below to highlight the code. -->

``` MySQL 
create database test;
use test;
create table student(
	stu_ID int NOT NULL,
	stu_Name varchar(40),
	stu_Age int,
	stu_City varchar(12),
	primary key(stu_ID)
);

insert into student values
(1, 'Ram', 20, 'Delhi'),
(2, 'Shyam', 18, 'Bombay'),
(3, 'Arun', 21, 'Chennai');

select * from student; 

update student 
set stu_age = 17, stu_City = 'kolkata' 
where stu_ID = 2 ;

select * from student;

delete from student where stu_ID = 3;

select * from student;
```
:point_right: Learned about [stored procedures](https://www.w3schools.com/sql/sql_stored_procedures.asp) :
 
<!-- Working in MSSQL but wrote MySQL below to highlight the code. -->
 ```MySQL
  -- Creating stored procedures using no parameters :
  create procedure selectAllStudents 
  as 
  select * from student
  go;
  
  -- Executing the stored procedure above 
  exec selectAllStudents ;
  
  -- Creating stored procedure using parameters :
  create procedure selectSpecificStudent @stu_ID int, @stu_City varchar(12)
  as
  select * from student where stu_ID = @stu_ID AND stu_City = @stu_City
  go
  
   -- Executing the stored procedure above
  exec selectSpecificStudent @stu_ID = 1, @stu_City = 'Delhi';  
  
 -- Creating stored procedure using insert command :
 create procedure spInsertStudentDetails @stu_ID int, @stu_Name varchar(40), @stu_Age int, @stu_City varchar(12)
 as
 begin
 -- set nocount on added to prevent extra result sets from
 -- interfering with select statements. 
 set nocount on;
 insert into student (stu_ID, stu_Name, stu_Age, stu_City)  values(@stu_ID, @stu_Name, @stu_Age, @stu_City)
 end;
 
 -- Executing the stored procedure above
 exec spInsertStudentDetails  3, 'Dhyan', 21, 'Agartala';
'''
