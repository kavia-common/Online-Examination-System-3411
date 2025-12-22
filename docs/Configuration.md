# Configuration and Environment

## Required Software
- Windows 10/11
- Visual Studio (2019 or later recommended) with .NET Framework development workload
- .NET Framework 4.8 targeting pack (project targets v4.8)
- SQL Server or SQL Server Express
- SQL Server Management Studio (SSMS) for database setup
- IIS Express (bundled with Visual Studio) or IIS for deployment

## Dependencies and Versions
- ASP.NET Web Forms targeting .NET Framework 4.8
- Bootstrap CSS (CSS/bootstrap.css included; version unspecified)
- NuGet packages included in repository:
  - Microsoft.CodeDom.Providers.DotNetCompilerPlatform (1.0.0)
  - Microsoft.Net.Compilers (1.0.0)
- Optional: CrystalDecisions.Web reference is present in the project file (ensure runtime availability if used)

## Configuration Files
- OnlineExamSystem/Web.config
  - <system.web> compilation and httpRuntime targets
  - <connectionStrings> dbconnection and OnlineExamConnectionString
- OnlineExamSystem/Web.Debug.config and Web.Release.config
  - Transform files for environment-specific settings (e.g., debug flag, connection strings)
- packages.config
  - NuGet dependencies

## Connection Strings
Set the connection strings to point to your SQL Server instance:
```xml
<connectionStrings>
  <add name="dbconnection" connectionString="Data Source=.\SQLEXPRESS;Initial Catalog=OnlineExamDB;Integrated Security=True" providerName="System.Data.SqlClient" />
  <add name="OnlineExamConnectionString" connectionString="Data Source=.\SQLEXPRESS;Initial Catalog=OnlineExamDB;Integrated Security=True" providerName="System.Data.SqlClient" />
</connectionStrings>
```

## Environment Variables and Secrets
- Current project does not require environment variables for runtime.
- For future secret management:
  - Use Web.config transforms to inject environment-specific values on publish.
  - In IIS, set environment variables and read them at application start if needed.
  - Consider encrypted connection strings using aspnet_regiis for production.

## Bootstrap and Client Assets
- The project includes CSS/bootstrap.css. To upgrade or add scripts:
  - Place CSS/JS in appropriate folders (e.g., CSS/, Scripts/)
  - Reference them in .aspx pages or master pages.

## Database Initialization
- Run the SQL script at database-script/Online-Examination-System-Databse-Script.sql
- Confirm login tables, question banks, courses, and exam schema are created as expected.
- If identity or roles are added later, document migrations and scripts here.

## Running and Ports
- Local development uses IIS Express via Visual Studio with an auto-assigned port.
- A preview environment may run on port 3001; configure IIS/IIS Express binding if you want to match that port.
