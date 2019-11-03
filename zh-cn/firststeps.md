# GTK的第一步

在GTK＃编程教程的这一部分中，我们将进行编程的第一步。我们将创建简单的程序。

## 简单的例子

第一个代码示例是一个简单的示例，它显示了居中的窗口。

center.cs

```csharp
using Gtk;

class SharpApp : Window {

    public SharpApp() : base("Center")
    {
        SetDefaultSize(250, 200);
        SetPosition(WindowPosition.Center);

        DeleteEvent += delegate { Application.Quit(); };

        Show();    
    }

    public static void Main()
    {
        Application.Init();
        new SharpApp();        
        Application.Run();
    }
}
```

该代码示例在屏幕中央显示一个小窗口。

```csharp
$ gmcs -pkg:gtk-sharp-2.0 center.cs
```

这是我们编译代码示例的方式。

```csharp
using Gtk;
```

现在我们可以`Gtk`直接使用名称空间中的对象。我们可以用`Window`代替`Gtk.Window`。

```csharp
class SharpApp : Window {
```

我们的应用程序基于`SharpApp`类。此类从该类继承`Window`。

```csharp
public SharpApp() : base("Center")
{
    ...   
}
```

这是构造函数。它构建了我们的应用程序。它还通过`base()`关键字调用其父构造函数。

```csharp
SetDefaultSize(250, 200);
```

这行为我们的窗口设置默认大小。

```csharp
SetPosition(WindowPosition.Center);
```

这条线使窗口在屏幕上居中。

```csharp
DeleteEvent += delegate { Application.Quit(); };
```

我们将代理插入`DeleteEvent`。当我们单击标题栏中的关闭按钮时，将触发此事件。或按Alt + F4。我们的代表永久退出了申请。

```csharp
Show();
```

现在我们显示窗口。在调用该`Show()`方法之前，该窗口不可见。

```csharp
public static void Main()
{
    Application.Init();
    new SharpApp();        
    Application.Run();
}
```

该`Main()`方法是应用程序的入口点。它启动并运行程序。

## 图标

在下一个示例中，我们显示应用程序图标。大多数窗口管理器在标题栏的左上角以及任务栏上都显示图标。

icon.cs

```csharp
using Gtk;
using System;

class SharpApp : Window {

    public SharpApp() : base("Icon")
    {
        SetDefaultSize(250, 160);
        SetPosition(WindowPosition.Center);
        SetIconFromFile("web.png");

        DeleteEvent += new DeleteEventHandler(OnDelete);

        Show();      
    }

    public static void Main()
    {
        Application.Init();
        new SharpApp();
        Application.Run();
    }

    void OnDelete(object obj, DeleteEventArgs args)
    {
        Application.Quit();
    }
}
```

该代码示例显示了应用程序图标。

```csharp
SetIconFromFile("web.png");
```

该`SetIconFromFile()`方法为窗口设置一个图标。从当前工作目录中的磁盘加载映像。

```csharp
DeleteEvent += new DeleteEventHandler(OnDelete);
```

这是另一种方式，我们如何将事件处理程序插入事件。只是有点冗长。

```csharp
void OnDelete(object obj, DeleteEventArgs args)
{
    Application.Quit();
}
```

这是delete事件的事件处理程序。

![图标](../assets/icon.png)图：图标

## 按钮

在下一个示例中，我们将使用GTK＃库进一步增强我们的编程技能。

button.cs

```csharp
using Gtk;

class SharpApp : Window
{

    public SharpApp() : base("Buttons")
    {
        SetDefaultSize(250, 200);
        SetPosition(WindowPosition.Center);

        DeleteEvent += delegate { Application.Quit(); };

        Fixed fix = new Fixed();

        Button btn1 = new Button("Button");
        btn1.Sensitive = false;
        Button btn2 = new Button("Button");
        Button btn3 = new Button(Stock.Close);
        Button btn4 = new Button("Button");
        btn4.SetSizeRequest(80, 40);

        fix.Put(btn1, 20, 30);
        fix.Put(btn2, 100, 30);
        fix.Put(btn3, 20, 80);
        fix.Put(btn4, 100, 80);

        Add(fix);
        ShowAll();
    }


    public static void Main() 
    {
        Application.Init();
        new SharpApp();
        Application.Run();
    }
}
```

我们在窗口上显示四个不同的按钮。我们将看到容器窗口小部件和子窗口小部件之间的区别，并将更改子窗口小部件的某些属性。

```csharp
Fixed fix = new Fixed();
```

`Fixed`小部件是不可见的容器小部件。其目的是包含其他子窗口小部件。

```csharp
Button btn1 = new Button("Button");
```

A `Button`是子窗口小部件。子窗口小部件放置在容器内。

```csharp
btn1.Sensitive = false;
```

我们使此按钮不敏感。这意味着我们无法单击它。图形化的小部件为灰色。

```csharp
Button btn3 = new Button(Stock.Close);
```

第三个按钮在其区域内显示图像。GTK＃库具有我们可以使用的内置图像库。

```csharp
btn4.SetSizeRequest(80, 40);
```

在这里，我们更改按钮的大小。

```csharp
fix.Put(btn1, 20, 30);
fix.Put(btn2, 100, 30);
...
```

在这里，我们将按钮小部件放置在固定容器小部件内。

```csharp
Add(fix);
```

我们将`Fixed`容器设置为`Window`小部件的主要容器。

```csharp
ShowAll();
```

我们可以调用`ShowAll()`方法，也可以`Show()`在每个小部件上调用方法。包括容器。

![纽扣](../assets/buttons.png)图：按钮

在本章中，我们在GTK＃编程库中创建了第一个程序。

[上一个](./introduction.md) [下一个](./layout.md)