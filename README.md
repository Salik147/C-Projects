# C-Projects
This repository contains C# practice projects
# Crud through database first
Step 1 install packages


Microsoft.EntityFrameWorkCore

Microsoft.EntityFrameWorkCore.SqlServer

Microsoft.EntityFrameWorkCore.Tools

Microsoft.EntityFrameWorkCore.Design
By clicking on dependencies , manage nuget packages then brows and install


# Execute a command for Scaffold DbContext
Scaffold-Dbcontext "server=ServerName; database=DatabaseName; trusted_connection=True;" Microsoft.EntityFrameWorkCore.SqlServer -OutputDir Models 

paste the above command by opening Nuget Package Manager Console  which could be found in Tools options 

# Updating Database
Make changes in database and run the command given below
Scaffold-Dbcontext "server=ServerName; database=DatabaseName; trusted_connection=True;" Microsoft.EntityFrameWorkCore.SqlServer -OutputDir Models -force

# Moving Connecion string from db context class to appsetting.ini
remove connection string from dbcontext class and past in appsetting.ini file such as

"ConnectionStrings": {
  "dbcs": "server=ServerName; database=DatabaseName; trusted_connection=True;"
},

and remove lines in the bracket in contextdb class from where the above lines ahve been copied

# Register connection string in program.cs file

//service added by me !

var provider = builder.Services.BuildServiceProvider();
var config = provider.GetRequiredService<IConfiguration>();
builder.Services.AddDbContext<StudentDBContext>(item => item.UseSqlServer(config.GetConnectionString("dbcs")));

namespace will be added above as : using DatabaseFirst.Models;

