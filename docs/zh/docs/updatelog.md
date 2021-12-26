# SOUI 更新到 2.0

更新：
1、修改 uiresbuilder，增加资源 ID 自动生成功能。包括自动提取所有布局中控件的
name，自动生成 ID，自动提取字符串表，颜色表。具体使用方式参见下一篇。
2、修改布局中引用字符串的方式。原来使用%str-name%这种方式来引用在字符串表中
定义的字符串，修改为使用和 android 一样的方式：@string/str-name，不支持嵌套。
3、增加颜色表，可以在布局 XML 中使用@color/color-name 这种方式使用颜色表中定
义的颜色值。
4、给 EventArg 增加一个 bubbleUp 属性，默认为 true, 应用中处理一个事件后可以将
bubbleUp 设置成 false，此时之前订阅的事件处理方法将不再调用（中断事件的冒泡过
程）。
5、增加一个 STreeView 控件，STreeView 中一个采用 MVC 模式设计的高性能
TreeCtrl，目前该控件还在测试阶段（欢迎使用，欢迎补充功能）。
6、在 SOUI 中增加 soui-version.h，版本号移动到该文件中定义。
