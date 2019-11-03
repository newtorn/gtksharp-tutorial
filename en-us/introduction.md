# Introduction to GTK#

This is an introductory GTK# programming tutorial. The tutorial is targeted for the C# programming language. It has been created and tested on Linux. The GTK# programming tutorial is suited for novice and intermediate programmers. Here are the [images](../assets.zip) used in this tutorial.



## GTK+

*GTK+* is a library for creating graphical user interfaces. The library is created in C programming language. The GTK+ library is also called the GIMP Toolkit. Originally, the library was created while developing the GIMP image manipulation program. Since then, the GTK+ became one of the most popular toolkits under Linux and BSD Unix. Today, most of the GUI software in the open source world is created in Qt or in GTK+. The GTK+ is an object oriented application programming interface. The object oriented system is created with the Glib object system, which is a base for the GTK+ library. The `GObject` also enables to create language bindings for various other programming languages. Language bindings exist for C++, Python, Perl, Java, C# and other programming languages.

The GTK+ itself depends on the following libraries.

- Glib
- Pango
- ATK
- GDK
- GdkPixbuf
- Cairo

The `Glib` is a general purpose utility library. It provides various data types, string utilities, enables error reporting, message logging, working with threads and other useful programming features. The `Pango` is a library which enables internationalisation. The `ATK` is the accessibility toolkit. This toolkit provides tools which help physically challenged people work with computers. The `GDK` is a wrapper around the low-level drawing and windowing functions provided by the underlying graphics system. On Linux, GDK lies between the X Server and the GTK+ library. Recently, much of its functionality have been delegated to the Cairo library. The `GdkPixbuf` library is a toolkit for image loading and pixel buffer manipulation. *Cairo* is a library for creating 2D vector graphics. It has been included in GTK+ since version 2.8.

Gnome and XFce desktop environments have been created using the GTK+ library. SWT and wxWidgets are well known programming frameworks that use GTK+. Prominent software applications that use GTK+ include Firefox or Inkscape.

## GTK#

GTK# is a wrapper over the GTK+ for the C# programming language. The library facilitates building graphical GNOME applications using Mono or any other compliant CLR. Gtk# is an event-driven system like any other modern windowing library where every widget in an application has handler methods that get called when particular events happen. Applications built using Gtk# will run on many platforms including Linux, Microsoft, Windows and Mac OS X. GTK# is part of the Mono initiative. There are basically two widget toolkits in Mono: Winforms and the GTK#. The GTK# is considered to be native for the Linux/Unix operating system.

## Compiling GTK# applications

We use the gmcs compiler to compile our GTK# applications.

```
$ gmcs -pkg:gtk-sharp-2.0 -r:/usr/lib/mono/2.0/Mono.Cairo.dll application.cs
```

The above line compiles a GTK# application that also uses the Cairo library.

## Sources

- [go-mono.com](http://www.go-mono.com/)
- [wikipedia.org](http://wwww.wikipedia.org/)

In this part of the GTK# tutorial, we have introduced the GTK# library.

[Previous](./readme.md) [Next](./firststeps.md)