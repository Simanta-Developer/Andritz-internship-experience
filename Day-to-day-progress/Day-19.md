# :computer: Day-19 :
:point_right: I added Logout page and  functionality in CRUD application. <br>
:point_right: Steps I did follow to add `Logout` features in CRUD application : <br>
1. Added action method named `Logout` inside Home controller :
``` C#
 public ActionResult Logout()
    {

       FormsAuthentication.SignOut();  //Removes the forms-authentication ticket from the browser.
                                
                                
       Session["IsLoggedIn"] = false;   // Set Session Login variable to false .
       Session.Abandon();               // Destroy all the previous held sessions .
       return RedirectToAction("Login", "Home");

    }
```
2. In `_Layout.cshtml` file I added this logic :
``` HTML
 @{
         if (Session["IsLoggedIn"] != null && (bool)Session["IsLoggedIn"])    // Check whether the the session is not null and true .
         {
               <li>@Html.ActionLink("Logout", "Logout", "Home", new { area = "" }, new { @class = "nav-link" })</li> // Display Logout in navbar if logged in .
         }
                       
         else
         {
               <li>@Html.ActionLink("Login", "Login", "Home", new { area = "" }, new { @class = "nav-link" })</li>
         }
  }
```
:point_right: I also used `Forms Authentication` for implementing authentication over `Login` page. <br>
:point_right: Steps I did follow to add `Forms Authentication` features in CRUD application : <br>
1. Inside `<system.web>`  tag in `Web.config` file I included authentication tag like below :
``` HTML
<authentication mode="Forms">
		  <forms loginUrl="/Home/Login"> </forms> // link of the page over which authentication will be applied.
</authentication>
```
2. Inside the `Login` form we included :
``` C#
 if (user != null)
 {
       FormsAuthentication.SetAuthCookie(lgup.E_mail, true);  //The SetAuthCookie method adds a forms-authentication ticket to either
                                                             // the cookies collection or the URL if CookiesSupported is false. 
       Session["IsLoggedIn"] = true;
       return RedirectToAction("Success", "Home");
 }
 else
 {
       ViewBag.Message = "Email or Password is incorrect";
 }


```
3. Inside `Home` controller, `[Authorize]` tag is written above the action method in which we want to authenticate users first using login. For example :
``` C#
[Authorize]
public ActionResult Success()
{
    return View();
}
```
:point_right: I followed this [video](https://www.youtube.com/watch?v=LlHjY8s6tZQ&list=PLaFzfwmPR7_JuVN71I9pEpN8JadDTh0rg&index=54) .



