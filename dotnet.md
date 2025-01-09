ASP.NET Core MVC CRUD Operations using .NET 8 and Entity Framework Core

link url - https://youtu.be/_uSw8sh7xKs?si=VL6193agJ3_TfQ5r

create a folder
open visual studio
choose template
filter - C# and web
select template - ASP.NET Core Web App (MVC)
provide - project-name, location, solution name
project-name - StudentPortal.Web
solution-name - StudentPortal
choose framework - .NET 8.0
authentication type - none

created - folder structure for mvc

Program.cs - main file - configuration
  builder object
  builder.Services.AddControllersWithView
  
Controller - default controller - HomeController
            HomeController has two actions method - index, privacy
  app.MapControllerRoute(
    name: "deafult"
    pattern: "{controller=Home}/{action=Index}/{id?}");
    - default view- Index()  -> goes to view folder name same as controller - HomeController - home folder in view
    view - home - index.html and privacy.html

launchsettings.json - profiles - https - applicationUrl -localhost:port

App - Entity Framework talk to sql server

project steps -
step -1 - create solution and project
install dependencies -
dependencies - manage nuget packages
add package -
browse 
Microsoft.EntityFrameworkCore.SqlServer]
Microsoft.EntityFrameworkCore.Tools - migrations - stay in sync with db and application

step -2 - create DbContext file - it is bridge b/w entityframework core and database. using properties of this class we will be able to talk to tables of sql server.

create new folder - Data - ApplicationDbContext.cs
this class will inherit DbContext, this DbContext cass comes from MSEntityCoreFramework
create a constructor - pass DBContextOptions<type>
public class ApplicationDbContext(): DBContext 
{
  //create constructor - ctor
  public ApplicationDbContext(DBContextOptions<ApplicationDbContext> options): base(options)
  { }
this contructor is used inside program.cs file, where we will be giving the DbContextOptions into and injecting it inside the ApplicationDbContext 

now, we think about what we will CRUD i.e. basically a table an entity

models - create a model -folder - Entities 
an entity is an class that has an identity. i.e. any class that has a unique id or identity

create new class - inside entities - Student.cs
public class Student {

  public Guid Id {get; set;}
  public string Name {get; set;}

  //prop - double tab
 public string Email { get; set; }
 public string Phone { get; set; }
 public bool Subscribed { get; set; }  
}
the Id will be automatically created by entityFramework, so from the form we want to capture the name, Email, Phone, Subscribed

entity Student will be used n ApplicationDbContext
how to use - by creating a property - DbSet<> - is repsresenting a collection of a particular type. here type is Students

 public DbSet<Student> Students { get; set; } - we can use this property to play around with students table yhat has been created or will be created soon in sql server db.

we want to inject this DbContext into our application using dependecy injection and later on beacuase we have injected this class into our app we should be able to use this inside our controllers and basically access the tables of the db we are about to create.

step - inject the ApplicationDbContext inside our app
Program.cs

below builder.Services
//inject DbContext - it tells which db and table we are about to create
//UseSqlServer - takes connection string of type string
//appsettings.json - 
add "ConnectionStrings": {
  "StudentPortal": "Server=DESKTOP-5EVKAPH\\SQLEXPRESS;Database=StudentPortalDb;Trusted_Connection=True;TrustServerCertificate=True"
}
builder.Services.AddDbContext<ApplicationDbContext>(options => options.UseSqlServer(builder.Configuration.GetConnectionString("StudentPortal")));
- UseSqlServer () takes a string - a keyname which we have defined in appsettings.json - conncetionStrings - StudentPortal - exact sanme name required

- here we are injecting our ApplicationDbContext and we are telling the application for this context plz use sql-server database and this is the connection string to this particular server and database.

- 
run entity core migration to create table  -
package manager - tools - Nuget package manager - package manager console
PM >
//create migration
Add-Migration "Initial Migration"
- creates a folder migrations - hash - initial-migration.cs
- two methods - up() and down()
- Up - create table - taking all this info from ApplicationDbContext
- so we are telling Entity frmewokr core to create a DbSet which is a table in terms of sql server
we are telling it to create a new table called student with properties as defined in Student.cs
- at this moment we only have created a class file, nothing has been create in sql server db.
- cmd for look for migration file generated and alos at database. if it is able to  find the db, it will execute what is not executed yet and it will sync up db with the project.

- if db is existing basically it is already sync it up
- refresh db - check table created
- PM > Update-Database 

 
