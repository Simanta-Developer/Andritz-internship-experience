# :computer: Day-15 : 
:point_right: I learned how to validate whether the registered Email already exists. <br>
:point_right: I used [Remote Validation](https://www.c-sharpcorner.com/article/remote-validation-in-asp-net-mvc/) which is using POST method. <br>
:point_right: Steps to implement registered Email already exists validation : <br>
1. In model.cs file we added Remote field in square brackets :
```C#
using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations;
using System.Linq;
using System.Net.Http;
using System.Web;
using System.Web.Mvc;

namespace ADOproject1.Models
{
    public class SignUpModel
    {
        public int S_ID { get; set; }

        [Required(ErrorMessage = "Username is required.")]
        public string Username { get; set;}

        [Required(ErrorMessage = "E_mail is required.")]                                                              // Format for remote field:
        [Remote("IsAlreadySigned", "Home", HttpMethod = "POST", ErrorMessage = "Registered EmailId already exists.")] // [Action Name,Controller name,method, error mesaage] 
        public string E_mail { get; set; }                                 

        [Required(ErrorMessage = "Password is required.")]
        public string Password { get; set;}

        [Required(ErrorMessage = "Confirm Password is required.")]
        public string Confirm_Password { get; set; }
    }
}

```
2. Inside the Home controller we need to make action method fo type  JsonResult :
``` C#
public JsonResult IsAlreadySigned(string E_mail)  // return true or false
        {
            SignupRepository SgupRepo = new SignupRepository();
            bool isExist = SgupRepo.GetAllSignupUser().Any(u => u.E_mail.ToLower() == E_mail.ToLower());   //Check whether Email exists in GetAllSignupUser list.
            return Json(!isExist, JsonRequestBehavior.AllowGet);  // If exists then return false, true otherwise .
        }

```
:point_right: I didn't need to make view since it already exists (i.e index.cshtml upon which it will display all input fields as well as error) . <br>
:point_right: I used this [article](https://www.c-sharpcorner.com/UploadFile/f1047f/check-if-usernameemail-already-registered-using-remote-vali/) for my reference .
