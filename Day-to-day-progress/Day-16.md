# :computer: Day-16 :
:point_right: I learned how to modify stored procedures using `ALTER` command. <br>
:point_right: By using it I added extra fields in sign up table and modified datatype of certain fields.<br>
:point_right: I altered insert and update stored procedure. The code for alter insert procedure is given below :
``` MySQL
ALTER procedure [dbo].[sp_insertdata]

@Username nvarchar(255),
@E_mail nvarchar(255),
@Password varchar(50),
@Confirm_Password varchar(50)

as
begin

insert into tbl_signup (Username, E_mail, Password, Confirm_Password) values(@Username, @E_mail, @Password, @Confirm_Password)

end
```




