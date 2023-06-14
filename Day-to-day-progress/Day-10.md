# :computer: Day-10 :
:point_right: I made a feature for accessing or reading all user information . <br>
:point_right: It uses `get` request to display all user information . <br>
:point_right: Steps I followed to read all user details are :
1. Created a stored procedure to run select query :
```MySQL
create procedure sp_selectdata

as
begin

select * from tbl_Signup
end
```
2. In `SignupRepository.cs` file I added UpdateSignupUser function :
``` C#
public List<SignUpModel> GetAllSignupUser()
{
            
     List<SignUpModel> SgupList = new List<SignUpModel>();


     SqlCommand com = new SqlCommand("sp_selectdata", con);
     com.CommandType = CommandType.StoredProcedure;
     SqlDataAdapter da = new SqlDataAdapter(com);
     DataTable dt = new DataTable();

     con.Open();
     da.Fill(dt);
     con.Close();
     //Bind SignUpModel generic list using dataRow     
     foreach (DataRow dr in dt.Rows)
     {

        SgupList.Add(

                    new SignUpModel
                    {

                        S_ID = Convert.ToInt32(dr["S_ID"]),
                        Username = Convert.ToString(dr["Username"]),
                        E_mail = Convert.ToString(dr["E_mail"]),
                        Password = Convert.ToString(dr["Password"]),
                        Confirm_Password = Convert.ToString(dr["Confirm_Password"]),

                    }
                    );
      }

      return SgupList;
}
```
3. Added action method named `ReadAllSgUser` inside `Home` controller :
``` C#
// Get request to read all user information 
public ActionResult ReadAllSgUser()
{
      SignupRepository SgupRepo = new SignupRepository();
      ModelState.Clear();
      return View(SgupRepo.GetAllSignupUser());
}
```
4. Created a view with the same action method name using list template.
