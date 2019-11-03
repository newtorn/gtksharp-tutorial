# GTK中的布局管理

在本章中，我们将展示如何在窗口或对话框中布置窗口小部件。

在设计应用程序的GUI时，我们决定要使用哪些小部件以及如何在应用程序中组织这些小部件。为了组织小部件，我们使用专门的不可见小部件，称为*布局容器*。在本章中，我们会提到`Alignment`，`Fixed`，`VBox`和`Table`。

## 固定

该`Fixed`容器的地方孩子部件在固定位置和固定的尺寸。此容器不执行自动布局管理。在大多数应用程序中，我们不使用此容器。我们在某些专业领域使用它。例如游戏，使用图表的专用应用程序，可以移动的可调整大小的组件（如电子表格应用程序中的图表），小的教学示例。

fixed.cs

```csharp
using Gtk;
using System;

class SharpApp : Window {

    private Gdk.Pixbuf rotunda;
    private Gdk.Pixbuf bardejov;
    private Gdk.Pixbuf mincol;

    public SharpApp() : base("Fixed")
    {
        SetDefaultSize(300, 280);
        SetPosition(WindowPosition.Center);
        ModifyBg(StateType.Normal, new Gdk.Color(40, 40, 40));
        DeleteEvent += delegate { Application.Quit(); };

        try {
            bardejov = new Gdk.Pixbuf("bardejov.jpg");
            rotunda = new Gdk.Pixbuf("rotunda.jpg");
            mincol = new Gdk.Pixbuf("mincol.jpg");
        } catch {
            Console.WriteLine("Images not found");
            Environment.Exit(1);
        }

        Image image1 = new Image(bardejov);
        Image image2 = new Image(rotunda);
        Image image3 = new Image(mincol);


        Fixed fix = new Fixed();

        fix.Put(image1, 20, 20);
        fix.Put(image2, 40, 160);
        fix.Put(image3, 170, 50);

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

在我们的示例中，我们在窗口上显示了三个小图像。我们明确指定放置这些图像的x，y坐标。

```csharp
ModifyBg(StateType.Normal, new Gdk.Color(40, 40, 40));
```

为了获得更好的视觉体验，我们将背景色更改为深灰色。

```csharp
bardejov = new Gdk.Pixbuf("bardejov.jpg");
```

我们将图像从磁盘加载到`Gdk.Pixbuf`对象。

```csharp
Image image1 = new Image(bardejov);
Image image2 = new Image(rotunda);
Image image3 = new Image(mincol);
```

的`Image`是，用于显示图像的小部件。它`Gdk.Pixbuf`在构造函数中包含对象。

```csharp
Fixed fix = new Fixed();
```

我们创建`Fixed`容器。

```csharp
fix.Put(image1, 20, 20);
```

我们将第一个图像放置在x = 20，y = 20坐标处。

```csharp
Add(fix);
```

最后，我们将`Fixed`容器添加到窗口中。

![固定](../assets/fixed.png)图：固定

## 对齐

该`Alignment`容器控制取向及其子控件的大小。

alignment.cs

```csharp
using Gtk;
using System;

class SharpApp : Window {


    public SharpApp() : base("Alignment")
    {
        SetDefaultSize(260, 150);
        SetPosition(WindowPosition.Center);
        DeleteEvent += delegate { Application.Quit(); };

        VBox vbox = new VBox(false, 5);
        HBox hbox = new HBox(true, 3);

        Alignment valign = new Alignment(0, 1, 0, 0);
        vbox.PackStart(valign);

        Button ok = new Button("OK");
        ok.SetSizeRequest(70, 30);
        Button close = new Button("Close");

        hbox.Add(ok);
        hbox.Add(close);

        Alignment halign = new Alignment(1, 0, 0, 0);
        halign.Add(hbox);

        vbox.PackStart(halign, false, false, 3);

        Add(vbox);

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

在代码示例中，我们在窗口的右下角放置了两个按钮。为此，我们使用一个水平框和一个垂直框以及两个对齐容器。

```csharp
Alignment valign = new Alignment(0, 1, 0, 0);
```

这会将子窗口小部件置于底部。

```csharp
vbox.PackStart(valign);
```

在这里，我们将`Alignment`小部件放置在垂直框中。

```csharp
HBox hbox = new HBox(true, 3);
...
Button ok = new Button("OK");
ok.SetSizeRequest(70, 30);
Button close = new Button("Close");

hbox.Add(ok);
hbox.Add(close);
```

我们创建一个水平框，并在其中放置两个按钮。

```csharp
Alignment halign = new Alignment(1, 0, 0, 0);
halign.Add(hbox);

vbox.PackStart(halign, false, false, 3);
```

这将创建一个对齐容器，它将其子窗口小部件放在右侧。我们将水平框添加到对齐容器中，然后将对齐容器包装到垂直框中。我们必须记住，对齐容器仅包含一个子窗口小部件。这就是为什么我们必须使用盒子。

![对准](../assets/alignment.png)图：对齐

## 表格

`Table`小部件将小部件按行和列排列。

Calculator.cs

```csharp
using Gtk;
using System;

class SharpApp : Window {


    public SharpApp() : base("Calculator")
    {
        SetDefaultSize(250, 230);
        SetPosition(WindowPosition.Center);
        DeleteEvent += delegate { Application.Quit(); };

        VBox vbox = new VBox(false, 2);

        MenuBar mb = new MenuBar();
        Menu filemenu = new Menu();
        MenuItem file = new MenuItem("File");
        file.Submenu = filemenu;
        mb.Append(file);

        vbox.PackStart(mb, false, false, 0);

        Table table = new Table(5, 4, true);

        table.Attach(new Button("Cls"), 0, 1, 0, 1);
        table.Attach(new Button("Bck"), 1, 2, 0, 1);
        table.Attach(new Label(), 2, 3, 0, 1);
        table.Attach(new Button("Close"), 3, 4, 0, 1);

        table.Attach(new Button("7"), 0, 1, 1, 2);
        table.Attach(new Button("8"), 1, 2, 1, 2);
        table.Attach(new Button("9"), 2, 3, 1, 2);
        table.Attach(new Button("/"), 3, 4, 1, 2);

        table.Attach(new Button("4"), 0, 1, 2, 3);
        table.Attach(new Button("5"), 1, 2, 2, 3);
        table.Attach(new Button("6"), 2, 3, 2, 3);
        table.Attach(new Button("*"), 3, 4, 2, 3);

        table.Attach(new Button("1"), 0, 1, 3, 4);
        table.Attach(new Button("2"), 1, 2, 3, 4);
        table.Attach(new Button("3"), 2, 3, 3, 4);
        table.Attach(new Button("-"), 3, 4, 3, 4);

        table.Attach(new Button("0"), 0, 1, 4, 5);
        table.Attach(new Button("."), 1, 2, 4, 5);
        table.Attach(new Button("="), 2, 3, 4, 5);
        table.Attach(new Button("+"), 3, 4, 4, 5);

        vbox.PackStart(new Entry(), false, false, 0);
        vbox.PackEnd(table, true, true, 0);

        Add(vbox);
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

我们使用`Table`小部件创建计算器框架。

```csharp
Table table = new Table(5, 4, true);
```

我们创建一个具有5行4列的表小部件。第三个参数是齐次参数。如果设置为true，则表中的所有小部件都具有相同的大小。所有窗口小部件的大小等于表容器中最大的窗口小部件。

```csharp
table.Attach(new Button("Cls"), 0, 1, 0, 1);
```

我们在表格容器上附加一个按钮。到表格的左上方单元格。前两个参数是单元格的左侧和右侧，后两个参数是单元格的顶部和左侧。

```csharp
vbox.PackEnd(table, true, true, 0);
```

我们将表格小部件打包到垂直框中。

![计算器骨架](../assets/calculator.png)图：计算器骨架

## 视窗

接下来，我们将创建一个更高级的示例。我们显示一个窗口，可以在JDeveloper IDE中找到它。

windows.cs

```csharp
using Gtk;
using System;

class SharpApp : Window {


    public SharpApp() : base("Windows")
    {
        SetDefaultSize(300, 250);
        SetPosition(WindowPosition.Center);
        BorderWidth = 15;
        DeleteEvent += delegate { Application.Quit(); };

        Table table = new Table(8, 4, false);
        table.ColumnSpacing = 3;

        Label title = new Label("Windows");

        Alignment halign = new Alignment(0, 0, 0, 0);
        halign.Add(title);

        table.Attach(halign, 0, 1, 0, 1, AttachOptions.Fill, 
            AttachOptions.Fill, 0, 0);

        TextView wins = new TextView();
        wins.ModifyFg(StateType.Normal, new Gdk.Color(20, 20, 20));
        wins.CursorVisible = false;
        table.Attach(wins, 0, 2, 1, 3, AttachOptions.Fill | AttachOptions.Expand,
            AttachOptions.Fill | AttachOptions.Expand, 1, 1);

        Button activate = new Button("Activate");
        activate.SetSizeRequest(50, 30);
        table.Attach(activate, 3, 4, 1, 2, AttachOptions.Fill, 
            AttachOptions.Shrink, 1, 1);

        Alignment valign = new Alignment(0, 0, 0, 0);
        Button close = new Button("Close");
        close.SetSizeRequest(70, 30);
        valign.Add(close);
        table.SetRowSpacing(1, 3);
        table.Attach(valign, 3, 4, 2, 3, AttachOptions.Fill,
            AttachOptions.Fill | AttachOptions.Expand, 1, 1);

        Alignment halign2 = new Alignment(0, 1, 0, 0);
        Button help = new Button("Help");
        help.SetSizeRequest(70, 30);
        halign2.Add(help);
        table.SetRowSpacing(3, 6);
        table.Attach(halign2, 0, 1, 4, 5, AttachOptions.Fill, 
            AttachOptions.Fill, 0, 0);

        Button ok = new Button("OK");
        ok.SetSizeRequest(70, 30);
        table.Attach(ok, 3, 4, 4, 5, AttachOptions.Fill, 
            AttachOptions.Fill, 0, 0);

        Add(table);
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

该代码示例显示了如何在GTK＃中创建类似的窗口。

```csharp
Table table = new Table(8, 4, false);
table.ColumnSpacing = 3;
```

该示例基于`Table`容器。列之间将有3 px的间距。

```csharp
Label title = new Label("Windows");

Alignment halign = new Alignment(0, 0, 0, 0);
halign.Add(title);

table.Attach(halign, 0, 1, 0, 1, AttachOptions.Fill, 
    AttachOptions.Fill, 0, 0);
```

这段代码创建了一个向左对齐的标签。标签放置在Table容器的第一行中。

```csharp
TextView wins = new TextView();
wins.ModifyFg(StateType.Normal, new Gdk.Color(20, 20, 20));
wins.CursorVisible = false;
table.Attach(wins, 0, 2, 1, 3, AttachOptions.Fill | AttachOptions.Expand,
    AttachOptions.Fill | AttachOptions.Expand, 1, 1);
```

文本视图小部件跨越两行两列。我们使小部件不可编辑并隐藏光标。

```csharp
Alignment valign = new Alignment(0, 0, 0, 0);
Button close = new Button("Close");
close.SetSizeRequest(70, 30);
valign.Add(close);
table.SetRowSpacing(1, 3);
table.Attach(valign, 3, 4, 2, 3, AttachOptions.Fill,
    AttachOptions.Fill | AttachOptions.Expand, 1, 1);
```

我们将关闭按钮放在文本视图小部件旁边的第四列中。（我们从零开始计数）将按钮添加到对齐小部件中，以便可以将其对齐到顶部。

![视窗](../assets/windows.png)图：Windows

在本章中，我们介绍了GTK＃小部件的布局管理。

[上一个](./firststeps.md) [下一个](./menus.md)