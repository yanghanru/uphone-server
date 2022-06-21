
|序号  <div style="width:60px"> |功能点  <div style="width:60px"> |描述  <div style="width:60px"> |生效 <div style="width:60px"> |
|:-----------------|:-------------------------|:----------------------|:-----------------------|
|1    |服务白名单         |只有加入到白名单中的应用才有 su 权限。白名单配置文件 /system/etc/su_app_white_list.conf<br>每一行代表一个应用，需要填写包名表示白名单应用, # 作为分割符，# 号之后为注释（可写可不写）<br># cat su_app_white_list.conf<br>com.tencent.android.qqdownloader # 应用宝<br>com.android.vending # 谷歌应用商店|重启手机|
|2       |限制APP安装                       |为了防止用户登录云手机界面后安装恶意应用，可以限制APP安装方式<br>* 增加系统开关，默认允许所有应用通过图形化安装应用，无限制<br>* 只能使用命令行来安装应用，意味着无法使用应用宝，浏览器，文件管理器等安装应用<br>使用方式<br>setprop persist.ucloud.appgraphinstall.flag 1 # 无限制<br>setprop persist.ucloud.appgraphinstall.flag 0 # 只能使用命令行安装，禁止图形化安装大包，但可以应用热更新小包|立即生效|
|3       |应用崩溃自动拉起         |修改容器/system/etc/app_restart_list.conf文件，将需要自动重启的应用包名写入app_restart_list.conf文件，按行分隔<br>例如：<br>com.tencent.tmgp.sgame<br>com.ucloud.crashdemo|立即生效|
|4       |手机内部获取自身id|获取方式<br>getprop persist.ucloud.ro.uphone.id|-|
|5       |launcher                    |用户可以自定义launcher，需将launcher提供给ucloud|-|
|6     |服务保活           |ucloud云手机可以对用户服务保活，需将apk文件提供给ucloud|-|
|7   |辅助模式                 |* 准备辅助服务的包名和服务名<br>* 执行系统命令，修改系统配置<br>settings put secure enabled_accessibility_services com.kptech.sback/com.kptech.sback.KpAccessibilityService<br>如果有多个服务，多个服务之间使用冒号分隔|立即生效|
