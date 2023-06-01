# :computer: Day-3 : 
:point_right: I wrote code for creating and manipulating MVC.<br>
:point_right: Code for creating the `controller` :
```c#
using System; // not initialized
using System.Collections.Generic; // not initialized
using System.Linq;// not initialized
using System.Security.Cryptography.X509Certificates; // not initialized
using System.Web; // not initialized
using System.Web.Mvc; // initialized

namespace WebApplication2.Controllers
{
    public class HomeController : Controller
    {
        public string Index(){
            return "Hello from Home controller index"
        }
    } 
}    
```

:point_right: Code for controller with parameters :
```c#
namespace WebApplication2.Controllers
{
    public class EmployeeController : Controller
    {
        // for single parameter , use the url format : DomainName/ControllerName/actionMethod?parameter=value
        public string EmployeeDetails(int id)

        {   
            string profile = string.Empty;
            if (id == 1)
            {
                profile = "ID is one";
            }
            else if (id == 2)
            {
                profile = "ID is two";
            }
            else
            {
                profile = "No record";
            }
            return profile;
            
            // For multiple parameter , use the url format : DomainName/ControllerName/actionMethod?parameter1=value1&parameter2=value2....
            public string Address(int id, string dept){            
                 return "id is" + id + "and department is " + dept;
            }
            // To make a parameter nullable we use ? symbol as shown below
            public string Nullable(int id, int ? code = null) {
                 return "id is" + id + "and department is " + code;
            }
        }

    }
    
```
:point_right:  Code to call `view` using controller :
```c#
    public class HomeController : Controller
    {
        // ActionResult is the parent class of all return types.
        public ActionResult Index(){
            return View();
        }
        // ViewResult is the inherited from ActionResult.
        public ViewResult AboutUs() {
            return View();
        }
    }
```
:point_right: Code for the `view` are :
```HTML  
// For every action method there is view, the following view is for the controller : home and action method : Index
@{
    Layout = null;
}

<!DOCTYPE html>

<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>AboutUs</title>
</head>
<body>
    <div> 
        <p> Hello, I am from Home contorller, view result </p>
        <a href="/Home/Index"> Home - Index </a> <br/> // paths are added to facilitate navigation.
        <A href="/Home/AboutUs"> Home - About Us </a>
    </div>
</body>
</html>
```
:point_right: We can also create view with the different name with respect to controllers and call them as follows :
```c#
     public ActionResult Index(){
            return View("Rename"); // It calls the view Rename which is different from Index. 
     }
```
:point_right: We can also call folder which have different name then controller using `tilde sign(~)` as follows
```c#
     public ActionResult Index(){
            return View("~/View/MyView/myNewView"); // It calls Views folder MyView which contains view named myNewView.
```
:point_right: We can also create special folder inside View, which is known as `Shared` folder. It contains views which can be accessed by every controller. 
> Its name should be `Shared` only.
 
:point_right:The code for the model are
```c#
namespace WebApplication3.Models
{
    public class Employee
    {
        public int ID { get; set; } 
        public string Name { get; set; }
        public int EmployeeID { get; set; }

    }
}
```
:point_right: The code for the controller for the above model is :
```c#
using System.Web.Mvc;
using WebApplication3.Models; // Importing models in controller
public class EmployeeController : Controller
    {
        // GET: Employee
        public ActionResult Index()
        {
            var data = GetEmployee(); // declare variable data which stores the above data from GetEmployee().
            return View(data); // pass the value to the View
        }

        private Employee GetEmployee() {  //This function initailizes and return the values of ID, Name, EmployeeID
            return new Employee()
            {
                ID = 1,
                Name = "Test",
                EmployeeID = 1234

            };
        }
    }

```
:point_right: The code for the View for the above model is :
``` HTML
@model WebApplication3.Models.Employee  <!-- using models from Employee folder. -->

<!DOCTYPE html>

<html>
<head>
    <meta name="viewport" content="width=device-width" />
    <title>Index</title>
</head>
<body>
    <div> 
        @Model.ID             // Display ID
        @Model.Name          // Display Name
        @Model.EmployeeID   // Display EmployeeID
    </div>
</body>
</html>
```


