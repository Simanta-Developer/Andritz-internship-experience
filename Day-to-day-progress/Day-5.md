# :computer: Day-5 :
:point_right: I learned about the term [ADO](https://learn.microsoft.com/en-us/sql/ado/microsoft-activex-data-objects-ado?view=sql-server-ver16) . <br>
:point_right: I also learned the process of database connectivity using ADO in .NET MVC framework . <br>
:point_right:  Steps that I followed to do database connectivity using ADO are :
1. Inside `WebConfig` file I provided connection string inside `<connectionStrings>` as follows :
``` HTML
 <connectionStrings>
  <!--  -->
	<add name="SUCS" connectionString="Data Source=NDLN21110396\SQLEXPRESS;Initial Catalog=DBSignUp;uid=sa;pwd=Admin@1234;" providerName="System.Data.SqlClient" />
 </connectionStrings>
```
2. To connect with the database wherever I need, I wrote the code given below :
``` C#
SqlConnection con = new SqlConnection(ConfigurationManager.ConnectionStrings["SUCS"].ToString());
```




