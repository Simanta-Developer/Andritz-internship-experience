# :computer: Day-9 :
:point_right: I wrote the code for sign-up user details. <br>
:point_right:  Steps I followed to add sign-up user details are :
1. Created a stored procedure to run insert query :
``` MySQL
create procedure sp_insertdata

@Username nvarchar(255),
@Password varchar(50),
as
begin

insert into tbl_signup (Username, E_mail, Password, Confirm_Password) values(@Username, @Password)

end
```
2. In `SignupRepository.cs` file I added `addUser` function :
``` C#
public bool addUser(SignUpModel objSignUpModel) 
{
    SqlCommand com = new SqlCommand("sp_insertdata", con);
    com.CommandType = CommandType.StoredProcedure;
    //com.Parameters.AddWithValue("@S_ID", objSignUpModel.S_ID);  // No need to set S_ID since it is in auto-increment mode .
    com.Parameters.AddWithValue("@Username", objSignUpModel.Username);
    com.Parameters.AddWithValue("@Password", objSignUpModel.Password);
    
    con.Open();
    int i = com.ExecuteNonQuery();
    con.Close();
    if (i > 0)
    {
        return true;
    }
    else
    {
         return false;
    }
}
```
3. Added action method named `Index` inside `Home` controller :
``` C#
// For GET request :
public ActionResult Index()
{
    return View();
}
// For POST request :
[HttpPost]
public ActionResult Index(SignUpModel sgup)
{
    try
    {
        if (ModelState.IsValid)
        {
            SignupRepository SgupRepo = new SignupRepository();

            if (SgupRepo.addUser(sgup))
            {               
                ViewBag.Message = "User details added successfully";
            }
            else
            {
                ViewBag.Message = "User details not added successfully";
                return View();
            }
         }
         ModelState.Clear();     // Clear all the input data in the view field after the sucessfull compilation
         return View();
    }
    catch
    {
         ViewBag.Message = "User details not added successfully";
         return View();
    }
}
```
4. Created a view with the same action method name using create template .

:point_right: Learned how to use debugger in .NET MVC framework during the debug process.


