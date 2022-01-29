此项目为 [Home Assistant](https://www.home-assistant.io/) 的[巴法云](https://cloud.bemfa.com/)插件。

## 功能
将 Home Assistant 实体同步至巴法云，并使用小爱同学/天猫精灵/小度音箱控制。

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg?style=for-the-badge)](https://github.com/hacs/integration)

## 使用
  1. 注册巴法云账号，并获取 uid
  2. 将此项目 clone 至 Home Assistant 配置目录的 custom\_components 目录下。
  3. 重启 Home Assistant 服务。
  4. 在 Home Assistant 的集成页面，搜索 "bemfa" 并添加。
  5. 根据提示输入巴法云的 uid, 并选择需要同步至巴法云的实体。
  6. 在智能音箱App中添加巴法云设备:
     * 小爱同学: 在米家app-->我的-->其他平台设备-->点击添加-->找到"巴法"，输入巴法云账号即可，设备会自动同步到米家。
     * 天猫精灵: 打开天猫精灵app，在app中搜索：巴法云。找到巴法云技能，点击绑定账号，登陆你的巴法云账号.
     * 小度音箱: 打开小度音箱app或者小度app，在app首页点+号-->添加设备-->搜索巴法，找到"巴法"，输入巴法云账号即可。

## 优势
  1. 操作简单，只需要下载一个插件，且是可视化配置。
  2. 无需公网 ip, 无需 RN.

## 实现原理
巴法云使用 MQTT 与终端设备通信，每个设备对应一个主题。

此插件根据用户选择的需要同步的实体，调用巴法云 API 创建对应主题，将此实体的实时状态发布至此主题，并订阅此主题的信息以控制它。

## Q/A
  - Q: 哪些实体支持同步至巴法云？

    A: 受巴法云的限制，目前仅支持开关类，灯类，风扇类，窗帘类，空调类和温度/湿度/开关/光照传感器，并且对每种语音助手的支持各有稍许区别，例如小度音箱不支持风扇类和空调类实体，具体参考[巴法云文档](https://cloud.bemfa.com/docs/#/)。此外，此插件将扫地机虚拟成开关类设备，因此可通过语音开关扫地机。

  - Q: 如何更改实体名字？

    A: 默认名字为此实体在 Home Assistant 平台上的名字，因此可以修改 Home Assistant 平台上的名字，然后重新配置插件；

       或者，可以直接登陆巴法云平台修改主题名，不过此方法会在下次重新配置插件时同步回去。

  - Q: 配置完成之后如何增加/删除实体？

    A: 目前只能先删除插件，然后重新配置。不过不用担心，重新配置时会默认选中上次配置的实体，这样可减少一些不便。

  - Q: Home Assistant 中米家的设备本来就支持小爱同学配置，还需要同步至巴法云么？

    A: 不需要，并且不建议同步。因为受巴法云平台限制，某些指令并不支持。例如空调类设备不支持“空调制冷”，“空调制热”这样的指令，只支持“空调加热”。

  - Q: 同时有小爱同学和天猫精灵，如何只同步非米家设备至小爱同学，并同步所有设备至天猫精灵？

    A: 目前没有太好的方案，一个可行的方案是注册2个巴法云账号，分别配置不同的实体进行同步，然后将2个账号分别绑定到小爱同学和天猫精灵。
