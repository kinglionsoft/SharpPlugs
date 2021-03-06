
<img src="https://raw.githubusercontent.com/liangshiw/SharpPlugs/master/doc/img/logo.png" width="200" height="200" /> 

# SharpPlugs 

.Net Core 鋒利扩展   
[中文文档](/doc/readme_cn.md)


[![Build status](https://ci.appveyor.com/api/projects/status/74whrxjajlnacjma?svg=true)](https://ci.appveyor.com/project/ShiWei-L/sharpplugs)
[![NuGet](https://img.shields.io/nuget/v/SharpPlug.Core.svg)](https://www.nuget.org/packages/SharpPlug.Core/)
[![NuGet](https://img.shields.io/nuget/dt/SharpPlug.Core.svg)](https://www.nuget.org/packages/SharpPlug.Core/)

## Current Features

- [DI](/doc/DI.md) 
- AutoMapper
- ElasticSearch
- WebAPiRoute
- EntityFramework Repoistory

## Get Started

First of all need to have a core project at asp.net Core, Here I've created a asp.net core MVC project

![asp.net core Project](/doc/img/getStarted/createProject.png)

Now, install SharpPlugs Core packages
```powershell
dotnet add package SharpPlug.Core
```

AddSharpPlugCore during Startup
```c#
 services.AddSharpPlugCore(opt=>{
      opt.DiAssembly.Add(Assembly.GetExecutingAssembly());
 });
```
![asp.net core Project](/doc/img/getStarted/2.png)

Now we have the function of the dependency injection, I create a TestService classes with TestService interface

*Automatic dependency injection is a naming rules, ends in Service or  Repository is automatically injected by default*

```c#
public class TestService : ITestService,IScopedDependency
{

    public string Hello()
    {
         return "Hello World";
    }
}

public  interface ITestService
{
    string Hello();
}
```
In the injected ITestService HomeController
```c#
public class HomeController : Controller
{
    private readonly ITestService _testService;
    public  HomeController(ITestService testService)
    {
        _testService = testService;
    }
    public IActionResult Index()
    {
        return View();
    }

    public IActionResult Hello()
    {
        return Json(_testService.Hello())   ;
    }
       
}
```
Now press F5 to debug，In your browser's address bar input /home/Hello，The request will be stay in the breakpoint

![asp.net core Project](/doc/img/getStarted/3.png)

Now we press F5 to let it continue to run , We will see the Hello World output

![asp.net core Project](/doc/img/getStarted/4.png)

Want to know more usage?Please see the [advanced document](/doc/document.md) 

## Nuget Packages

SharpPlugs is distributed as nuget packages.

|Package|Status|
|:------|:-----:|
|SharpPlug.Core|[![NuGet version](https://badge.fury.io/nu/SharpPlug.Core.svg)](https://badge.fury.io/nu/SharpPlug.Core)|
|SharpPlug.ElasticSearch|[![NuGet version](https://badge.fury.io/nu/SharpPlug.ElasticSearch.svg)](https://badge.fury.io/nu/Abp.AspNetCore)|
|SharpPlug.AutoMapper|[![NuGet version](https://badge.fury.io/nu/SharpPlug.AutoMapper.svg)](https://badge.fury.io/nu/SharpPlug.AutoMapper)|
|SharpPlug.WebApi|[![NuGet version](https://badge.fury.io/nu/SharpPlug.WebApi.svg)](https://badge.fury.io/nu/SharpPlug.WebApi)|
|SharpPlug.EntityFrameworkCore|[![NuGet version](https://badge.fury.io/nu/SharpPlug.EntityFrameworkCore.svg)](https://badge.fury.io/nu/SharpPlug.EntityFrameworkCore)|