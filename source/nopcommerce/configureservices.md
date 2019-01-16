# 配置服务
## 启动服务配置
### NopDbStartup DB配置
主要配置EF相关服务。

``` C#
/// <summary>
/// Add and configure any of the middleware
/// </summary>
/// <param name="services">Collection of service descriptors</param>
/// <param name="configuration">Configuration of the application</param>
public void ConfigureServices(IServiceCollection services, IConfiguration configuration)
{
    //add object context
    services.AddNopObjectContext();

    //add EF services
    services.AddEntityFrameworkSqlServer();
    services.AddEntityFrameworkProxies();
}
```
AddNopObjectContext 扩展用于配置数据库上下文,配置EF使用惰性加载.

``` C#
/// <summary>
/// Register base object context
/// </summary>
/// <param name="services">Collection of service descriptors</param>
public static void AddNopObjectContext(this IServiceCollection services)
{
    services.AddDbContext<NopObjectContext>(optionsBuilder =>
    {
        optionsBuilder.UseSqlServerWithLazyLoading(services);
    });
}
```
同时添加EF相关服务。
### NopCommonStartup 公共配置
> 响应压缩 [参考](https://docs.microsoft.com/zh-cn/aspnet/core/performance/response-compression?view=aspnetcore-2.2)
``` C#
//compression
services.AddResponseCompression();
```
> 配置选项 [参考](https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/configuration/options?view=aspnetcore-2.2)
``` C#
//add options feature
services.AddOptions();
```
> 内存缓存配置 [参考](https://docs.microsoft.com/zh-cn/aspnet/core/performance/caching/memory?view=aspnetcore-2.2)
``` C#
//add memory cache
services.AddMemoryCache();
```
> 分布式缓存配置 [参考](https://docs.microsoft.com/zh-cn/aspnet/core/performance/caching/distributed?view=aspnetcore-2.2)
``` C#
//add distributed memory cache
services.AddDistributedMemoryCache();
```
> session配置 [参考](https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/app-state?view=aspnetcore-2.2)

设置cookie名字为 **.Nop.Session**  
设置cookie请求协议限制为Https, **SecuritySettings.ForceSslForAllPages** 值默认为true,
[Cookie配置参考](https://docs.microsoft.com/zh-cn/aspnet/core/security/authentication/cookie?view=aspnetcore-2.2)

``` C#
/// <summary>
/// Adds services required for application session state
/// </summary>
/// <param name="services">Collection of service descriptors</param>
public static void AddHttpSession(this IServiceCollection services)
{
    services.AddSession(options =>
    {
        options.Cookie.Name = $"{NopCookieDefaults.Prefix}{NopCookieDefaults.SessionCookie}";
        options.Cookie.HttpOnly = true;

        //whether to allow the use of session values from SSL protected page on the other store pages which are not
        options.Cookie.SecurePolicy = DataSettingsManager.DatabaseIsInstalled && EngineContext.Current.Resolve<SecuritySettings>().ForceSslForAllPages
            ? CookieSecurePolicy.SameAsRequest : CookieSecurePolicy.None;
    });
}
```
> 防止跨站点请求伪造 (XSRF/CSRF) [参考](https://docs.microsoft.com/zh-cn/aspnet/core/security/anti-request-forgery?view=aspnetcore-2.2)

设置cookie名字为 **.Nop.Antiforgery**  

``` C#
/// <summary>
/// Adds services required for anti-forgery support
/// </summary>
/// <param name="services">Collection of service descriptors</param>
public static void AddAntiForgery(this IServiceCollection services)
{
    //override cookie name
    services.AddAntiforgery(options =>
    {
        options.Cookie.Name = $"{NopCookieDefaults.Prefix}{NopCookieDefaults.AntiforgeryCookie}";

        //whether to allow the use of anti-forgery cookies from SSL protected page on the other store pages which are not
        options.Cookie.SecurePolicy = DataSettingsManager.DatabaseIsInstalled && EngineContext.Current.Resolve<SecuritySettings>().ForceSslForAllPages
            ? CookieSecurePolicy.SameAsRequest : CookieSecurePolicy.None;
    });
}
```
### AuthenticationStartup 身份认证配置
### NopMvcStartup MVC配置
## AutoMaper配置
## Autofac配置
## 运行启动任务