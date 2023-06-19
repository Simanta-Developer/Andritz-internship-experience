# :computer: Day-17 :
:point_right: I learned about [Simple Mail Transfer protocol(SMTP)](https://www.geeksforgeeks.org/simple-mail-transfer-protocol-smtp/) .<br>
:point_right: By using it we are going to send mail to the user who signed up in the application .<br>
:point_right: Code for implementing SMTP protocol :
1. Created a new action method inside `Home` Controller named `SendEmail`
```C#
public void SendEmail(string recipientEmail, string subject, string body) // Passed mail that is used during sign-up, subject, body.
{
    try
    {
        // Configure the SMTP client
        using (var smtpClient = new SmtpClient("smtp.gmail.com", 587)) // (address of SMTP server, Port number)
        {
            // Set the credentials
            smtpClient.UseDefaultCredentials = false;
            smtpClient.Credentials = new NetworkCredential("simantacrud3@gmail.com", "bboiwsexhyrlwkru"); // Used app password from google

            // Enable SSL for secure communication
            smtpClient.EnableSsl = true;

            // Create the email message
            using (var message = new MailMessage("simantacrud3@gmail.com", recipientEmail))
            {
                // Set the subject and body of the email
                message.Subject = subject;
                message.Body = body;

                // Specify that the email body contains HTML content
                message.IsBodyHtml = true;

                // Send the email
                smtpClient.Send(message);
            }
        }
    }
    catch (Exception ex)
    {
        // Handle the exception if an error occurs during email sending
        TempData["ErrorMessage"] = "An error occurred while sending the email: " + ex.Message;
    }
}

```
2. Called `SendEmail` function inside action method `Index`
``` C#
//Partial code to show where SendEmail function has been called .
public ActionResult Index(SignUpModel sgup)
{
   try
   {
       if (ModelState.IsValid)
       {
          SignupRepository SgupRepo = new SignupRepository();
          EmailRepository EmailRepo = new EmailRepository();

          if (SgupRepo.addUser(sgup))
          {
              string subject = EmailRepo.SubjectRepo();
              string body = EmailRepo.BodyRepo();
              SendEmail(sgup.E_mail, subject, body); // Here we called for SendEmail function .
              ViewBag.Message = "User details added successfully";
              
              
```
              
              
                    



