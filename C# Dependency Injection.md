**Множественная регистрация сервисов:**

```
services.AddScoped<ICustomLogger, FileLogger>();
services.AddScoped<ICustomLogger, DbLogger>();
services.AddScoped<ICustomLogger, EventLogger>();

public HomeController(IEnumerable<ICustomLogger> loggers)
{
   
}
```

- https://www.infoworld.com/article/3597989/use-multiple-implementations-of-an-interface-in-aspnet-core.html
