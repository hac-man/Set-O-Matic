<a id="readme-top"></a>
<!-- PROJECT SHIELDS -->
<!-- PROJECT LOGO -->

<br />
<div align="center">
  <img src="images/SetOMatic.png" alt="Set-O-Matic logo" width="128">
  <h1 align="center">Set-O-Matic</h1>
  <p align="center"><strong>
    Simple strongly-typed settings provider
  </strong>
  </p>
</div>


## What is Set-O-Matic?

Set-O-Matic is a simple set of T4 templates that automatically creates a strongly-typed Settings class that is dynamically loaded with values from App.config or Web.config at runtime. 


```csharp    
     int threads;
     DateTime cutoffDate;
     string connString;

     //this:
     threads = Settings.appSettings.MaxThreadCount;
     cutoffDate = Settings.appSettings.CutoffDate;
     connString = Settings.connectionStrings.DevDB;

     //instead of this:
     threads = int.Parse(ConfigurationManager.AppSettings["MaxThreadCount"]);
     cutoffDate = DateTime.Parse(ConfigurationManager.AppSettings["CutoffDate"]);
     connString = ConfigurationManager.ConnectionStrings["DeDB"].ConnectionString;
```


## Why use Set-O-Matic?
* Fewer application errors
* All settings (including connection strings) are accessible via IntelliSense
* No need to cast settings to intended types (settings are strongly-typed)
* Compiler-checked code is cleaner code. Help the compiler help you!

## Features
* Extremely lightweight. 
* All settings are automatically available via the *Settings* static class
* Setting values are automatically retrieved from the config file at runtime
* Allows the use of IntelliSense to reference all application settings
* Provides a connectionString child class(es) making all connection strings available via the Settings class
* Supports custom configuration sections without the need to add any supporting code
* Seamlessly handles transformed config files since values are loaded at runtime
* Type-checking at application startup makes it easy to catch invalid values
* No more casting of int, date, or other non-string values
* No dependencies to be deployed. All necessary functionality is included in complied application file (.exe)
* Overall robustness of application code is increased due to fewer opportunities for errors
  
**Config setting to Settings property Examples:**

`<add name="Active" value="true">` becomes `public bool Active {get; set;}`

**Usage:** `if (Settings.Active){...}`

`<add name="CutoffDate" value="01/01/2025">` becomes `public DateTime CutoffDate {get; set;}`

**Usage:** `DateTime endDt = Settings.CutoffDate;`


<!-- GETTING STARTED -->
## Getting Started

Getting started with Set-O-Matic is simple:
1.  Install
2. Start using the newly created static Settings class

### Prerequisites

Set-O-Matic works with any .Net Framework project in any Visual Studio version that supports T4 templates and uses a Web.config or App.config file. There are no additional dependencies. 

### Installation

Install the Latest [Set-O-Matic package](https://www.nuget.org/packages/SetOMatic/) from NuGet.org using the NuGet CLI ( `$ dotnet add package SetOMatic --version 1.0.0.7` ) or Visual Studio's Package Manager. 

### Configuration

The Set-O-Matic class files (`Settings.cs` and `SetOMatic.cs`) will be created automatically in a new `Settings` folder in the root of the project. The `Settings` object can then immeidiatly be referenced in code and will contain all current settings and connection strings defined in the application's App.config or Web.config file.

No additiional configuration is needed

<!-- USAGE EXAMPLES -->
### Usage

1. To use Set-O-Matic, type `Settings.` in any code file. IntelliSense will list all available settings.
   
<img src="images/appSettings.png" alt="Using SetOMatic">

2. Select the setting you wish to use.
   
<img src="images/appSetting2.png" alt="Using SetOMatic">

#### Notes

Settings that are contained in the *appSettings* section of the config file can be accessed using _`Settings.appSettings.`_
Custom application settings sections can be accessed using _`Settings.[custom_section_name].`_ :

  <img src="images/CustomSectionConfig.png" alt="Custom Section">
  <img src="images/CustomSection.png" alt="Custom Section">

Unlike when using .Net's ConfigurationManager class, no custom section code is required to access custom sections defined in the config file.

**Connection strings** contained in the `connectionStrings` section of the config file can be accessed using _`Settings.connectionStrings.`_
Custom connection string sections can be accessed using `Settings.[custom connection string section name].`

  <img src="images/connectionString.png" alt="Updating Settings">
  
### Updating settings

If settings are added to or removed from the config file, the Settings class should be updated by right-clicking on the files 

`/Settings/SetOMatic.tt`  
`/Settings.Settings.tt` 

and selecting Run custom tool`

<img src="images/RunCustomTool.png" alt="Updating Settings">

The `Settings.cs` and `SetOMatic.cs` files will be updated with the new settings.

There is no need to run the custom tool after modifying setting *values* only since they are loaded dynamically at runtime
