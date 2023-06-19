# :computer: Day-18 :
:point_right: I added login page which takes input as email and password along with its validation . <br>
:point_right: Steps I followed to make login page :
1. Created a file named as `LoginModel.cs` inside model folder :
```C#
using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations; //This is need for model validation check
using System.Linq;
using System.Web;

namespace ADOproject1.Models
{
    public class LoginModel
    {
        [Required(ErrorMessage = "Email is required.")]
        [EmailAddress(ErrorMessage = "Invalid email address.")]
        public string E_mail { get; set; }

        [Required(ErrorMessage = "Password is required.")]
        public string Password { get; set; }
    }
}
```
2. Created a new action method `Login` inside `Home` controller :
```C#
// For GET request :
 public ActionResult Login()
 {
     return View();
 }
// For POST request :
 [HttpPost]
 public ActionResult Login(LoginModel lgup)
 {
     try 
     {
         if (ModelState.IsValid)
         {
             SignupRepository SgupRepo = new SignupRepository();
                    
             var user = SgupRepo.GetAllSignupUser().Find(u => u.E_mail == lgup.E_mail && u.Password == lgup.Password); // Check whether the email and its corrosponding
                                                                                                                          password is correct .
             if (user != null)   // if user object is found
             {
                 return RedirectToAction("ReadAllSgUser", "Home");
             }
             else
             {
                 ViewBag.Message = "Email or Password is incorrect";
             }

          }
               
          ModelState.Clear();
          return View();
      }

      catch
      {
          ViewBag.Message = "Login unsuccessfull";
          return View();
      }            
}

```
3. Added `view` with the same action method name Login using create template with alert prompt :
``` HTML
<div>
    @if (@ViewBag.Message != null)
    {
        <script type="text/javascript">

             alert("@ViewBag.Message");
        </script>
    }
</div>
```


 
