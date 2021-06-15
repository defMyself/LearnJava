# 面向对象

* Java程序员注重于创建程序员定义的，称为类和接口的类型
* Java的核心在于类（我们用它创建对象），而不是函数
* 设计员用设计模式构造类和对象集合
* 创造型设计模式描述实例化对象的技术
* 结构型设计模式使得设计者能够把类和对象组织成更大的结构
* 行为型设计模式为对象分配责任



## 对象思想：问题陈述分析

> 某公司打算建造一栋两层高的办公楼，并未它装一部电梯。公司要求开发一个面向对象的模拟程序，对电梯的运行进行建模，判断它是否符合要求。公司要求该模拟包含一个有电梯井（`elevator shaft`）和电梯车厢(`elevator car`)组成的电梯系统。



## 对象思想：确定问题陈述中的类

### 1. 确定问题陈述中的类

### 2. 对象建模



## 对象思想： 确定类属性

## 对象思想： 确定对象的状态和活动

* 活动图

## 对象思想： 确定类操作



## 对象思想： 对象间协作



## 思考问题： 开始编写电梯模拟器的类

* 可见性
* 导航
* 实现



## 对象思想：在电梯模拟器中结合继承

## 三种设计模式的探索

* 单例：防止系统创建一个类的多个对象
* 直至运行时才确定即将创建的对象类型

5中创造性模式

* 抽象类工厂
* 创建者
* 工厂
* 原型
* 单例



### 单例模式

> 有时，系统应只包含类的一个对象--即，一旦实例化该对象，程序就不应该创建该类的其他对象。
>
> 如:一个系统仅使用一个对象与数据库进行连接，该对象负责管理数据库连接从而确保其他对象不能初始化不必要的连接
>
> 单例设计模式保证系统最多只能实例化一个类对象

```java
public final class Singleton {
    private static Singleton singleton = new Singleton();
    
    private Singleton() {
        System.err.println("Singleton object created.");
    }
    
    public static Singleton getSingletonInstance() {
        return singleton;
    }
}
```

```java
public class SingletonTest {
    public static void main(String args[])
    {
        Singleton firstSingleton;
        Singleton secondSingleton;
        
        firstSingleton = Singleton.getSingletonInstance();
        secondSingleton = Singleton.getSingletonInstance();
        
    }
}
```



python单例

* 基类
* 元类
* 装饰器
* 模块



```python
class Singleton(object):
    def __new__(cls, *args, **kwargs):
        if not hasattr(cls, '_instance'):
            cls._instance = super(Singleton, cls).__new__(cls, *args, **kwargs)
        return cls._instance

class MyClass(Singleton):
    a = 1
    
```

python `metaclass`

```python
class Singleton(type):
    def __call__(cls, *args, **kwargs):
        if not hasattr(cls, '_instance'):
            cls._instance = super(Singleton, cls).__call__(*args, **kwargs)
        return cls.__instance

class MyClass(metaclass=Singleton):
    a = 1
    
    
```



代理模式允许系统使用一个对象替代另一个对象



## 对象思想： 事件处理

## 对象思想： 利用UML设计接口

## 对象思想：用例

## 对象思想：多线程

## 对象思想：并行设计模式

* 单线程执行设计模式
* 受保护的挂起设计模式
* 障碍设计模式
* 读写互锁设计模式
* 两阶段终止设计模式

## 对象思想：视图中的动画和声音

