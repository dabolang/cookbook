# 应用启动
ASP.NET Core 中的应用启动通过 **Startup** 类配置服务和应用的请求管道。  
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
## 请求管道