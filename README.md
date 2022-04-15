# Entity framework

Project demo and help create Database First and Code first in Entity Framework

## Add Entity Framework

(via NuGet Package)[https://entityframeworkcore.com/approach-code-first]

or command Install-Package EntityFramework

Microsoft.EntityFrameworkCore.SqlServer

Microsoft.EntityFrameworkCore.Tools

Microsoft.EntityFrameworkCore.Design

## Code first 

### From AppDBContext create Migradtions with command

(Link)[https://xuanthulab.net/ef-core-tao-migration-trong-entityframework-voi-c-csharp.html]

In visual studio Open: Tools > Nuget Packet Manager > Nuget Manager Console

Type command to create Migrations: Add-Migration Initial -c AppDBContext 

Type command to update db to database server: Update-Database

Add-migration MyFirstMigration ( class define)

### Net core command with .NET Tool

(Link)[https://docs.microsoft.com/en-us/ef/core/cli/dotnet]

Install dotnet ef global in powershell: dotnet tool install --global dotnet-ef [--version 5.0.16]

Create the first Migrations: dotnet ef migrations add InitAppDBContext --output-dir ./Entity/Migrations

/* Code in start up at netcore project
// Thực hiện Migrate - tạo db đúng cấu trúc Migration cuối cùng nếu chưa có
// Nếu DB đã có từ các Migration trước, sẽ cập nhật
var o = new DbContextOptions<Entity.AppDBContext>();
using (var webcontext = new Entity.AppDBContext(o) )
{
    //// Use on case DB First
    //context.Database.EnsureCreated();

    // Use on case Code First
    webcontext.Database.Migrate();

    // Seed() is function to create or update DB
}
*/

Chay all upgrage of db: dotnet ef database update

Nếu muốn tạo SQL Script cho Migration thì gõ: dotnet ef migrations script --output migrations.sql

Nếu muốn tạo View store procedure: 

/*
protected override void Up(MigrationBuilder migrationBuilder)
{
    // Remark GO command in script
    migrationBuilder.sql(@"Query_Here");
}
*/

## Database first
(Link)[https://www.devart.com/dotconnect/postgresql/docs/EFCore-Database-First-NET-Core.html]

### Install Entity Framework core
Install-Package Microsoft.EntityFrameworkCore.Tools

Install-Package [...].EFCore.Design

### Create or update dbcontext with UI in Visual Studio
Very simple with some video in Youtobe

### Run command to build DBContext with Nuget Manager Console
Create DBContent

Scaffold-DbContext "Data Source=(localdb)\ProjectsV13;Initial Catalog=Northwind; Integrated Security=True;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models/DB

Scaffold-DbContext "Data Source=(localdb)\ProjectsV13;Initial Catalog=Northwind; Integrated Security=True;Connect Timeout=30;Encrypt=False;TrustServerCertificate=False;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models/DB -Tables dept,emp

Update existing models
Scaffold-DbContext "<connection string>" -Provider Microsoft.EntityFrameworkCore.SqlServer -Tables Customers, Orders, Products -Force


### Run command to build DBContext with dotnet tool in powershell
Create With commnand:

dotnet ef dbcontext scaffold "Server=.\;Database=AdventureWorksLT2012;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -o Model -c "AdventureContext"


Updating the Model 
dotnet ef dbcontext scaffold "Server=.\;Database=AdventureWorksLT2012;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer --force
