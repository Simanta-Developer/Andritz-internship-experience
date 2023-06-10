# :computer: Day-12 :
:point_right: I learned about [Form validation and its types](https://www.c-sharpcorner.com/UploadFile/0c1bb2/Asp-Net-form-validation-using-javascript/) : <br>
>  It can be broadly classified in two types :  <br>
> * Client side validation .  <br>
> * Server side validation .  <br>

:point_right: For this CRUD app we are using ASP.NET MVC model validations.  <br>
:point_right: Steps to implement validation :
1. In model.cs file we added `Required` field in square brackets : 
``` C#
using System;
using System.Collections.Generic;
using System.ComponentModel.DataAnnotations; // Reference for ASP.NET MVC model validation
using System.Linq;
using System.Web;

namespace ADOproject1.Models
{
    public class SignUpModel
    {
        public int S_ID { get; set; }

        [Required(ErrorMessage = "Username is required.")] // Applying Required validation field
        public string Username { get; set;}

        [Required(ErrorMessage = "Password is required.")] // Applying Required validation field
        public string Password { get; set;}
    }
}

```
2. Set the configuration inside the <appSettings> tag in the web.config file :  <br>
``` HTML
  <appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
  </appSettings>
```
3. Add the JavaScript references inside the “BundleConfig.cs” file, creating a new script bundle :
``` C#
   bundles.Add(new ScriptBundle("~/bundles/jqueryval").Include(
                        "~/Scripts/jquery.unobtrusive*",
                        "~/Scripts/jquery.validate*"));
```  
4. Render these scripts in the “_Layout.cshtml” file :
``` HTML
   @Scripts.Render("~/bundles/jqueryval")  
``` 
:point_right: I used this [article](https://www.c-sharpcorner.com/UploadFile/13048b/model-validation-in-Asp-Net-mvc909/) for my reference .
  
  
