# Java Applet

> Java Applet 是一种Java程序。它一般运行在支持Java的Web浏览器内。因为它有完整的Java API支持，所以Applet是一个全功能的Java应用程序

**独立Java程序和Applet的不同**

* Java 中的Applet类继承了`java.applet.Applet`类
* Applet类没有定义`main()`,
* Applet被设计为嵌入在一个`html`页面
* Applet的安全机制称为沙箱安全

## `Applet`的声明周期

* `init`
* `start`
* `stop`
* `destroy`
* `paint`

