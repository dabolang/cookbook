# 应用启动
ASP.NET Core 中的应用启动通过 **Startup** 类配置服务和应用的请求管道。<br>
nop通过**Nop.Web.Framework.Infrastructure.Extensions.ServiceCollectionExtensions**对**IServiceCollection**接口进行了扩展
``` C#
/// <summary>
/// Add services to the application and configure service provider
/// </summary>
/// <param name="services">Collection of service descriptors</param>
public IServiceProvider ConfigureServices(IServiceCollection services)
{
    return services.ConfigureApplicationServices(Configuration);
}

/// <summary>
/// Configure the application HTTP request pipeline
/// </summary>
/// <param name="application">Builder for configuring an application's request pipeline</param>
public void Configure(IApplicationBuilder application)
{
    application.ConfigureRequestPipeline();
}
```
## 配置服务
### 加载配置文件  
首先加载 **NopConfig**,**HostingConfig**配置文件
### HttpContext支持  
``` C#
//add accessor to HttpContext
services.AddHttpContextAccessor();
```
### IEngine 实例化  
``` C#
//create, initialize and configure the engine
var engine = EngineContext.Create();
    engine.Initialize(services);
```
Initialize方法进行了如下设置
+ API 访问支持TLS 1.2
+ 使用NopFileProvider为默认文件提供者,可以通过CommonHelper.DefaultFileProvider 获得
+ 添加services.AddMvcCore()
+ 插件初始化 PluginManager.Initialize(mvcCoreBuilder.PartManager, nopConfig)
#### 插件初始化  
PluginManager.Initialize方法用于初始化插件  
``` C#
//initialize plugins
var nopConfig = provider.GetRequiredService<NopConfig>();
var mvcCoreBuilder = services.AddMvcCore();
        PluginManager.Initialize(mvcCoreBuilder.PartManager, nopConfig);
```

### 配置服务
``` C#
var serviceProvider = engine.ConfigureServices(services, configuration);
```
### 启动定时任务
## 请求管道