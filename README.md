 # 👑 .NET/.NET Core Dynamic Service Registration

This is a NET 5.0 and .NET Core dynamic service registration library which enables you to register all your services into .NET 5.0 and .NET Core Dependency Injection container at once without exposing the service implementation.
 
 ## ⭐ Give a star
   
   **If you find this library useful to you, please don't forget to encouraging me to do such more stuffs by giving a star (⭐) to this repository. Thank you.**

## ✈️ How do I get started?

First install the lastest version of `
TanvirArjel.Extensions.Microsoft.DependencyInjection` [nuget package](https://www.nuget.org/packages/TanvirArjel.Extensions.Microsoft.DependencyInjection) into your project as follows:
 
    Install-Package TanvirArjel.Extensions.Microsoft.DependencyInjection
    
Now in your `ConfigureServices` method of the `Startup` class:

```C#
public static void ConfigureServices(IServiceCollection services)
{
    services.AddServicesOfAllTypes();
}
```
    
Moreover, if you want only specific assemblies to be scanned during type scanning:

```C#
public static void ConfigureServices(IServiceCollection services)
{
    // Assemblies start with "TanvirArjel.Web", "TanvirArjel.Application" will only be scanned.
    string[] assembliesToBeScanned = new string[] { "TanvirArjel.Web", "TanvirArjel.Application" };
    services.AddServicesOfAllTypes(assembliesToBeScanned);
}
```

### For Blazor WebAssembly App:

```C@
builder.Services.AddServicesOfAllTypes(Assembly.GetExecutingAssembly());
```
        
## 🛠️ Usage:

Now mark your services with any of the `ScopedServiceAttribute`, `TransientServiceAttribute` and `SingletonServiceAttribute` attributes as follows:

```C#
// Mark with ScopedServiceAttribute if you want to register `IEmployeeService` as scoped service.
[ScopedService]
public interface IEmployeeService
{
    Task CreateEmployeeAsync(Employee employee);
}

internal class EmployeeService : IEmployeeService 
{
    public async Task CreateEmployeeAsync(Employee employee)
    {
       // Implementation here
    };
}
```

### For hosted service:

```C#
[HostedService]
public class TestBackgroundService : BackgroundService
{
    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        Console.WriteLine("Hosted service called.");
        await Task.CompletedTask.ConfigureAwait(false);
    }
}
```
  
## 🐞 Bug Report
   
   Dont forget to submit an issue if you face. we will try to resolve as soon as possible.
