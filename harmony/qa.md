### The type of the target device does not match the deviceType configured in the module.json5 file of the selected module

第一次创建了项目、配置好了环境后启动项目,编辑器提示:The type of the target device does not match the deviceType configured in the module.json5 file of the selected module.主要是说说当前选中的设备和配置文件中设定的设备类型不匹配.如果我们在创建项目、配置环境的时候,都是根据文档一步一步操作的,那么应该就不会出现设备和设定的设备类型不匹配的情况.那么出现问题的原因就有可能是配置的环境变量呢,没有被重新加载.

解决方式:

重启编辑器

参考:https://developer.huawei.com/consumer/cn/forum/topic/0202128717526318526

### 安装模拟器的时候总是提示空间不够

HarmonyOS应用开发的这一套环境全部搭建下来,挺占用存储空间的.很多开发者可能使用的是Mac,我们都知道,Mac价格比较贵,所以呢,硬盘可能并不是很大,以我的设备256G的SSD为例,在安装IDE、配置环境的时候,磁盘有10多个G的空间,结果在项目启动的时候,总是提示空间不够,所以为了环境的正式启动,在搭建Harmony这一套开发环境的时候,至少留足20G的空间吧.

我本身做前端,本地很多的前端项目,node_modules占用了很大的磁盘空间,这也是让开发者很头疼的一个问题.