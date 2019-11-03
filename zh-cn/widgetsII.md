# GTK中的小部件II

在GTK＃编程教程的这一部分中，我们继续介绍GTK＃小部件。

我们将介绍`Entry`小部件，`Scale`小部件`ToggleButton`和`Calendar`。

## 条目

该`Entry`是单行文本输入字段。该小部件用于输入文本数据。

entry.cs

```csharp
using Gtk;
using System;

class SharpApp : Window {

    Label label;

    public SharpApp() : base("Entry")
    {
        SetDefaultSize(250, 200);
        SetPosition(WindowPosition.Center);
        BorderWidth = 7;
        DeleteEvent += delegate { Application.Quit(); };

        label = new Label("...");

        Entry entry = new Entry();
        entry.Changed += OnChanged;

        Fixed fix = new Fixed();
        fix.Put(entry, 60, 100);
        fix.Put(label, 60, 40);

        Add(fix);

        ShowAll();
    }

    void OnChanged(object sender, EventArgs args)
    {
        Entry entry = (Entry) sender;
        label.Text = entry.Text;
    }

    public static void Main()
    {
        Application.Init();
        new SharpApp();
        Application.Run();
    }
}
```

此示例显示了条目小部件和标签。我们输入的文本将立即显示在标签控件中。

```csharp
Entry entry = new Entry();
```

`Entry` 小部件已创建。

```csharp
entry.Changed += OnChanged;
```

如果`Entry`窗口小部件中的文本已更改，我们将调用该`OnChanged()`方法。

```csharp
void OnChanged(object sender, EventArgs args)
{
    Entry entry = (Entry) sender;
    label.Text = entry.Text;
}
```

我们从小`Entry`部件获取文本并将其设置为标签。

![条目小部件](../assets/entry.png)图：条目小部件

## 规模

它`Scale`是一个小部件，可让用户通过在有限间隔内滑动旋钮来以图形方式选择一个值。我们的示例将显示音量控制。

hscale.cs

```csharp
using Gtk;
using System;

class SharpApp : Window {

    Gdk.Pixbuf mute, min, med, max;
    Image image;

    public SharpApp() : base("Scale")
    {
        SetDefaultSize(260, 150);
        SetPosition(WindowPosition.Center);
        DeleteEvent += delegate { Application.Quit(); };

        HScale scale = new HScale(0, 100, 1);
        scale.SetSizeRequest(160, 35);
        scale.ValueChanged += OnChanged;

        LoadPixbufs();

        image = new Image(mute);

        Fixed fix = new Fixed();
        fix.Put(scale, 20, 40);
        fix.Put(image, 219, 50);

        Add(fix);

        ShowAll();
    }

    void LoadPixbufs() 
    {
        try {
            mute = new Gdk.Pixbuf("mute.png");
            min = new Gdk.Pixbuf("min.png");
            med = new Gdk.Pixbuf("med.png");
            max = new Gdk.Pixbuf("max.png");
        } catch {
            Console.WriteLine("Error reading Pixbufs");
            Environment.Exit(1);
        }
    }

    void OnChanged(object obj, EventArgs args)
    {
        HScale scale = (HScale) obj;
        double val = scale.Value;

        if (val == 0) {
            image.Pixbuf = mute;
        } else if (val > 0 && val < 30) {
            image.Pixbuf = min;
        } else if (val > 30 && val < 80) {
            image.Pixbuf = med;
        } else {
            image.Pixbuf = max;
        }
    }

    public static void Main()
    {
        Application.Init();
        new SharpApp();
        Application.Run();
    }
}
```

在上面的示例中，我们有`HScale`和`Image`小部件。通过拖动比例，我们可以更改`Image`小部件上的图像。

```csharp
HScale scale = new HScale(0, 100, 1);
```

`HScale`小部件已创建。参数是下边界，上边界和阶跃。

```csharp
HScale scale = (HScale) obj;
double val = scale.Value;
```

在该`OnChange()`方法中，我们获得了比例小部件的值。

```csharp
if (val == 0) {
    image.Pixbuf = mute;
} else if (val > 0 && val <= 30) {
    image.Pixbuf = min;
} else if (val > 30 && val < 80) {
    image.Pixbuf = med;
} else {
image.Pixbuf = max;
}
```

根据获得的值，我们在图像小部件中更改图片。

![HScale小部件](../assets/scale.png)图：HScale小部件

## 切换按钮

`ToggleButton`是具有两种状态的按钮：已按下和未按下。通过单击可以在这两种状态之间切换。在某些情况下此功能非常合适。

togglebuttons.cs

```csharp
using Gtk;
using System;

class SharpApp : Window {

    DrawingArea darea;
    Gdk.Color col;

    public SharpApp() : base("ToggleButtons")
    {
        col = new Gdk.Color(0, 0, 0);

        SetDefaultSize(350, 240);
        SetPosition(WindowPosition.Center);
        BorderWidth = 7;
        DeleteEvent += delegate { Application.Quit(); };

        ToggleButton red = new ToggleButton("Red");
        red.SetSizeRequest(80, 35);
        red.Clicked += OnRed;

        ToggleButton green = new ToggleButton("Green");
        green.SetSizeRequest(80, 35);
        green.Clicked += OnGreen;

        ToggleButton blue = new ToggleButton("Blue");
        blue.SetSizeRequest(80, 35);
        blue.Clicked += OnBlue;

        darea = new DrawingArea();
        darea.SetSizeRequest(150, 150);
        darea.ModifyBg(StateType.Normal, col);

        Fixed fix = new Fixed();
        fix.Put(red, 30, 30);
        fix.Put(green, 30, 80);
        fix.Put(blue, 30, 130);
        fix.Put(darea, 150, 30);

        Add(fix);

        ShowAll();
    }

    void OnRed(object sender, EventArgs args) 
    {
        ToggleButton tb = (ToggleButton) sender;

        if (tb.Active) {
            col.Red = 65535; 
        } else {
            col.Red = 0;
        }

        darea.ModifyBg(StateType.Normal, col);         
    }

    void OnGreen(object sender, EventArgs args) 
    {
        ToggleButton tb = (ToggleButton) sender;

        if (tb.Active) {
            col.Green = 65535; 
        } else {
            col.Green = 0;
        }

        darea.ModifyBg(StateType.Normal, col);
    }

    void OnBlue(object sender, EventArgs args) 
    {
        ToggleButton tb = (ToggleButton) sender;

        if (tb.Active) {
            col.Blue = 65535; 
        } else {
            col.Blue = 0;
        }

        darea.ModifyBg(StateType.Normal, col);
    }

    public static void Main()
    {
        Application.Init();
        new SharpApp();
        Application.Run();
    }
}
```

在我们的示例中，我们显示了三个切换按钮和一个`DrawingArea`。我们将区域的背景色设置为黑色。切换按钮将切换颜色值的红色，绿色和蓝色部分。背景颜色取决于我们按下的切换按钮。

```csharp
col = new Gdk.Color(0, 0, 0);
```

这是将使用切换按钮更新的颜色值。

```csharp
ToggleButton red = new ToggleButton("Red");
red.SetSizeRequest(80, 35);
red.Clicked += OnRed;
```

该`ToggleButton`控件创建。我们将其尺寸设置为80x35像素。每个切换按钮都有其自己的处理程序方法。

```csharp
darea = new DrawingArea();
darea.SetSizeRequest(150, 150);
darea.ModifyBg(StateType.Normal, col);
```

该`DrawingArea`窗口小部件是用于显示颜色，由切换按钮混合的微件。开始时，它显示为黑色。

```csharp
if (tb.Active) {
    col.Red = 65535; 
} else {
    col.Red = 0;
}
```

我们根据`Active`属性的值更新颜色的红色部分。

```csharp
darea.ModifyBg(StateType.Normal, col);
```

我们更新`DrawingArea`小部件的颜色。

![ToggleButton小部件](../assets/togglebuttons.png)图：ToggleButton小部件

## 日历

我们最终的窗口小部件是`Calendar`窗口小部件。它用于处理日期。

calendar.cs

```csharp
using Gtk;
using System;

class SharpApp : Window {

    private Label label;

    public SharpApp() : base("Calendar")
    {
        SetDefaultSize(300, 270);
        SetPosition(WindowPosition.Center);
        DeleteEvent += delegate { Application.Quit(); };

        label = new Label("...");

        Calendar calendar = new Calendar();
        calendar.DaySelected += OnDaySelected;

        Fixed fix = new Fixed();
        fix.Put(calendar, 20, 20);
        fix.Put(label, 40, 230);

        Add(fix);

        ShowAll();
    }

    void OnDaySelected(object sender, EventArgs args)
    {
        Calendar cal = (Calendar) sender;
        label.Text = cal.Month + 1 + "/" + cal.Day + "/" + cal.Year;
    }

    public static void Main()
    {
        Application.Init();
        new SharpApp();
        Application.Run();
    }
}
```

我们有一个`Calendar`小部件和一个`Label`。从日历中选择的日期显示在标签中。

```csharp
Calendar calendar = new Calendar();
```

`Calendar` 小部件已创建。

```csharp
Calendar cal = (Calendar) sender;
label.Text = cal.Month + 1 + "/" + cal.Day + "/" + cal.Year;
```

在该`OnDaySelected()`方法中，我们将引用引至`Calendar`小部件，然后将标签更新为当前选择的日期。

![日历](../assets/calendar.png)图：日历

在本章中，我们结束了有关GTK＃小部件的讨论。

[上一个](./widgets.md) [下一个](./customwidget.md)