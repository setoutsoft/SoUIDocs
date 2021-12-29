# SoUI 版本更新日志

## 3.0.1.20

更新新版本propgrid控件。

## 3.0.1.19

调整realwnd参数。ver:3.0.1.19

## 3.0.1.18

修复上一版本的skinPool错误,版本号升级到3.0.1.18

## 3.0.1.5

清理编译警告，将skin的lazyload属性放到initfinished里处理。

## 3.0.1.2

update version to 3.0.1.2

## 3.0.0.28

fix caret show while there are transform matrix.

## 3.0.0.25

upgrade ver to 3.0.0.25

## 3.0.0.23

make SWindow::GetAttribute public.

## 3.0.0.18

update clone_demos.bat

## 3.0.0.17

调整语言翻译接口，简化语言中指定字体的方式。
      解决多字节版本编译问题。

## 3.0.0.13

Merge branch 'master' of <https://gitee.com/setoutsoft/soui3>

## 3.0.0.10

update version to 3.0.0.10

## 3.0.0.9

update ver to 3.0.0.9

## 3.0.0.6

更新向导模板文件

## 3.0.0.5

将SIntAnimator::getValue 移动到TValueAnimator中，减少代码重复。
在demo中注意处理数据动画完全后的release().

## 2.9.0.2

版本号升级到2.9.0.2
调整布局中include元素的用法，当被include使用的布局不是include结点时，支持从include节点传递布局属性。

## 2.8.0.6

update version to 2.8.0.6

## 2.8.0.5

调整SMenu的DpiAware实现。
增加SSliderBar, SProgress的dpiaware支持。

## 2.8.0.4

update version to 2.8.0.4

## 2.8.0.3

fix linearlayout bug.

## 2.8.0.2

update ver to 2.8.0.2

## 2.8.0.1

update version to 2.8.0.1

## 2.7.1.2

fix LresultFromObject link error.

## 2.7.1.1

fix bug for vs2010 compiling.

## 2.7.0.1

forward mousewheel to parent for single line edit

## 1.0到2.0版本日志

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
