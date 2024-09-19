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


# Adding Code in Home Controller.cs

just add CodeFirstContext context in constructor such as:
 public HomeController(ILogger<HomeController> logger, CodeFirstdbContext context)
 {
     _logger = logger;
 }

then hower the mouse cursor over context and press ctrl + . and select "create and assign field context"

# Now Make views
Delete already existed index view file
add Tolist function to the IAction method of the index present in HomeController.cs from the context class through database

public IActionResult Index()
{
    var data  = context.Students.ToList();
    return View(data);
}

Now  right click on view and make index view with razorpage

# automatic generation
delete home controller and home folder in views
make new controller and select "MVC controller with views and entityframwork"
Complete crud will be generayed automatically
