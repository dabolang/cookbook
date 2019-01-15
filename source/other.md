# 随笔
## WriteLockDisposable
写入锁定,使用ReaderWriterLockSlim实现。
## DataSettingsManager
当安装时会创建 **~/App_Data/dataSettings.json** 文件,该文件会保存数据库连接,当设置时 **DataSettingsManager.DatabaseIsInstalled** 为 true
> **~/App_Data/dataSettings.json** 常量可在 **Nop.Core.Data.NopDataSettingsDefaults** 类中找到

