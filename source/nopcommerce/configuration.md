# 配置文件

## NopConfig

<!--table-->

| 项 | 说明 |
| --- | --- |
| DisplayFullErrorStack | 该值指示是否在生产环境中显示完整错误 |
| AzureBlobStorageConnectionString | Azure BLOB 连接字符串 |
|AzureBlobStorageContainerName|Azure BLOB 容器名称|
|AzureBlobStorageEndPoint|Azure BLOB 默认终结点|
|RedisCachingEnabled|该值指示是否使用Redis缓存，默认false不使用|
|RedisCachingConnectionString|Redis连接字符串|
|PersistDataProtectionKeysToRedis|该值指示是否使用Redis数据保护,默认false不使用|
|UserAgentStringsPath|完整 browscap 文件路径|
|CrawlerOnlyUserAgentStringsPath|爬虫 browscap 文件路径,使用全部该项设置为空|
|UseFastInstallationService|该值指示是否使用快速安装|
|DisableSampleDataDuringInstallation|该值指示是否安装时使用示例数据,默认false|
|PluginsIgnoredDuringInstallation|安装时忽略插件列表|
|IgnoreStartupTasks|该值指示是否应忽略启动任务,默认false|
|ClearPluginShadowDirectoryOnStartup|该值指示在应用程序启动时是否清除/Plugins/bin目录(插件目录),默认true|
|CopyLockedPluginAssembilesToSubdirectoriesOnStartup|该值指示在应用程序启动时是否将“锁定”程序集从/Plugins/bin目录复制到临时子目录,默认false|
|UseUnsafeLoadAssembly|不安全方式加载程序集，默认true|
|UsePluginsShadowCopy|该值指示在应用程序启动时是否将插件库复制到/plugins/bin目录，默认true|
|UseRowNumberForPaging|该值指示是否使用与SQL Server 2008和SQL Server 2008R2的向后兼容性，默认false|
|UseSessionStateTempDataProvider|该值指示是否将TempData存储在session中，默认false|

<!--endtable-->

<!--table-->

| Name | Data | Length |
| --- | --- | --- |
| Prefix | 0x01 0x56 | 2 Bytes |
| Version | 0x01 | 1 Byte |
| PublicKey | Take the last 20 bytes in raw public key | 20 Bytes |
| Checksum | After performing SHA256 calculation twice on the byte array obtained in step 3, take the first 4 bytes of the operation result | 4 Bytes |

<!--endtable-->

## HostingConfig