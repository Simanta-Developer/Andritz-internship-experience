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
:point_right: I also learned and applied password validation using javascript as well as model validation : 
* Using javascript :
1. Inside the Index.cshtml file, I specified id for  Password and Confirm_Password fields :
``` HTML
<!-- id For Password field is txtPassword -->
@Html.EditorFor(model => model.Password, new { htmlAttributes = new { @class = "form-control", @id = "txtPassword" } })
<!-- id For Confirm_Password field is txtConfirmPassword -->
@Html.EditorFor(model => model.Password, new { htmlAttributes = new { @class = "form-control", @id = "txtConfirmPassword" } })

```
2. Then I wrote javascript code to check whether the Password and Confirm_Password fields matches or not using `script` tag inside Index view.
``` Javascript
<script type="text/javascript">
        function Validate() {
            var password = document.getElementById("txtPassword").value;
            var confirmPassword = document.getElementById("txtConfirmPassword").value;
            if (password != confirmPassword) {
                alert("Passwords do not match.");
                return false;
            }
            return true;
        }
 </script>
```
* Using Model validation :
1. Used compare validation above confirm password field inside SignUpModel.cs file :
``` C#
[System.ComponentModel.DataAnnotations.Compare("Password", ErrorMessage = "Confirm  Password doesn't match, Try again !")]
public string Confirm_Password { get; set; }
```
 



