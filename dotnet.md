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

 public DbSet<Student> Students { get; set; } - we can use this property to play around with students table yhat has been created or will be created in sql server.

 
 
