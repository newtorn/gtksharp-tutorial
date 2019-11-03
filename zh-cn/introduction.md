# GTK简介

这是GTK＃编程入门教程。本教程针对C＃编程语言。它已在Linux上创建并经过测试。GTK＃编程教程适合新手和中级程序员。这是本教程中使用的[图像](../assets.zip)。

## GTK +

*GTK +*是用于创建图形用户界面的库。该库是用C编程语言创建的。GTK +库也称为GIMP Toolkit。最初，该库是在开发GIMP图像处理程序时创建的。从那时起，GTK +成为Linux和BSD Unix下最受欢迎的工具包之一。如今，开源世界中的大多数GUI软件都是在Qt或GTK +中创建的。GTK +是面向对象的应用程序编程接口。面向对象的系统是使用Glib对象系统创建的，该系统是GTK +库的基础。该`GObject`还能够创建各种其他编程语言的语言绑定。存在用于C ++，Python，Perl，Java，C＃和其他编程语言的语言绑定。

GTK +本身依赖以下库。

- Glib
- Pango
- ATK
- GDK
- GdkPixbuf
- Cairo

该`Glib`是一个通用工具库。它提供各种数据类型，字符串实用程序，启用错误报告，消息日志记录，使用线程和其他有用的编程功能。这`Pango`是一个可以实现国际化的图书馆。这`ATK`是辅助功能工具包。该工具包提供的工具可帮助残障人士使用计算机。它`GDK`是基础图形系统提供的低级绘图和窗口功能的包装。在Linux上，GDK位于X Server和GTK +库之间。最近，它的许多功能已委托给Cairo图书馆。该`GdkPixbuf`库是用于图像加载和像素缓冲区操作的工具箱。*Cairo*是用于创建2D矢量图形的库。自2.8版起，它已包含在GTK +中。

Gnome和XFce桌面环境已使用GTK +库创建。SWT和wxWidgets是使用GTK +的众所周知的编程框架。使用GTK +的著名软件应用程序包括Firefox或Inkscape。

## GTK

GTK＃是针对C＃编程语言的GTK +的包装。该库有助于使用Mono或任何其他兼容的CLR构建图形GNOME应用程序。Gtk＃是一个事件驱动的系统，就像任何其他现代的窗口库一样，其中应用程序中的每个小部件都具有处理程序方法，这些处理程序方法在发生特定事件时被调用。使用Gtk＃构建的应用程序将在许多平台上运行，包括Linux，Microsoft，Windows和Mac OSX。GTK＃是Mono计划的一部分。Mono中基本上有两个窗口小部件工具箱：Winforms和GTK＃。GTK＃被认为是Linux / Unix操作系统的本机。

## 编译GTK＃应用程序

我们使用gmcs编译器来编译我们的GTK＃应用程序。

```
$ gmcs -pkg:gtk-sharp-2.0 -r:/usr/lib/mono/2.0/Mono.Cairo.dll application.cs
```

上一行编译了一个也使用Cairo库的GTK＃应用程序。

## 资料来源

- [go-mono.com](http://www.go-mono.com/)
- [wikipedia.org](http://wwww.wikipedia.org/)

在GTK＃教程的这一部分中，我们介绍了GTK＃库。

[上一个](./readme.md) [下一个](./firststeps.md)

