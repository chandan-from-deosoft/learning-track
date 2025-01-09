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


step -- create solution and project
add package -
Microsoft.EntityFrameworkCore.SqlServer]
Microsoft.EntityFrameworkCore.Tools
