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

:point_right: Code for controller with parameters
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
                //profile =  "ID is ="+ id + "and dept is =" + dept;
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


