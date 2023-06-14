# :computer: Day-11 :
:point_right: I learned and added features for update and delete records in CRUD sign-up application. <br>
:point_right: Steps I did follow to add update features in CRUD application : <br>
1. Created a stored procedure to run update query :
```MySQL
create procedure sp_updatedata 
(  
  @S_ID int,
  @Username nvarchar(255),
  @Password varchar(50),  
)  
as  
begin  
   Update tbl_Signup  
   set Username = @Username,   
   Password=@Password , 
   where S_ID = @S_ID  
End 
```
2. In `SignupRepository.cs` file I added UpdateSignupUser function :
``` C#
public bool UpdateSignupUser(SignUpModel objSignUpModel)
{
    SqlCommand com = new SqlCommand("sp_updatedata", con);
    com.CommandType = CommandType.StoredProcedure;
    com.Parameters.AddWithValue("@S_ID", objSignUpModel.S_ID);
    com.Parameters.AddWithValue("@Username", objSignUpModel.Username);
    com.Parameters.AddWithValue("@Password", objSignUpModel.Password);
    con.Open();
    int i = com.ExecuteNonQuery();
    con.Close();
    if (i >= 1)
    {
        return true;
    }
    else
    {
        return false;
    }
}
```
3. Added action method named EditSgUserDetails inside `Home` controller :
``` C#
// For GET request :
public ActionResult EditSgUserDetails(int id)
{
        SignupRepository SgupRepo = new SignupRepository();
        return View(SgupRepo.GetAllSignupUser().Find(sgup => sgup.S_ID == id));
}
// For POST request :
[HttpPost]

 public ActionResult EditSgUserDetails(int id, SignUpModel obj)
 {
         try
         {
                SignupRepository SgupRepo = new SignupRepository();

                SgupRepo.UpdateSignupUser(obj);
                return RedirectToAction("GetAllSignupUser");
          }
          catch
          {
                return View();
          }
  }
```
3. Created a view with the same action method name using edit template. <br>

:point_right: Steps I did follow to add delete features in CRUD application : <br>
1. Created a stored procedure to run delete query : 
``` MySQL
create procedure sp_deletedata
(
  @S_ID int
)
as
begin
delete from tbl_Signup where S_ID = @S_ID 
end
```
2. In `SignupRepository.cs` file I added DeleteSignupUser function :
``` C#
public bool DeleteSignupUser(int Id)
{
     SqlCommand com = new SqlCommand("sp_deletedata", con);

     com.CommandType = CommandType.StoredProcedure;
     com.Parameters.AddWithValue("@S_ID", Id);

     con.Open();
     int i = com.ExecuteNonQuery();
     con.Close();
     if (i >= 1)
     {
        return true;
     }
     else
     {
        return false;
     }            
}    
```
3. Added action method named DeleteSgUserDetails inside `Home` controller :
``` C#
public ActionResult DeleteSgUserDetails(int id)
{
     try
     {
         SignupRepository SgupRepo = new SignupRepository();
         if (SgupRepo.DeleteSignupUser(id))
         {
             ViewBag.AlertMsg = "Employee details deleted successfully";

         }
         return RedirectToAction("GetAllSignupUser");
      }
     catch
     {
         return View();
     }
}
```

