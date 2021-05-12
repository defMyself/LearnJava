# Java反射

## 1.什么是反射

Java反射：在运行状态中，可以获得类任意类的属性和方法，可以调用任意对象的方法和属性，并能改变它的属性。

动态语言:动态语言在程序运行时，允许改变程序结构或变量类型

Java是准动态语言

Perl, Python, Ruby是动态语言

C++，Java,C#不是动态语言

## 2. 反射能做什么

代码可以在运行时装配，无需再组件之间进行源代码链接，降低代码的耦合度；还有动态代理的实现

## 3. 反射的具体实现

```java
package com.ys.reflex;
public class Person {
    private String name = "Tom";
    public int age = 18;
    public Person() {
        
    }
    
    private void say() {
        System.out.println("private say() ...");
    }
    public void work() {
        System.out.println("public work() ...");
    }
}
```

### 1. 得到`Class`的三种方式

1. 通过对象调用`getClass()`方法来获取
2. 直接通过`类名.class`的方式得到
3. 通过`Class`对象的`forName()`静态方法来获取

**一个类在`JVM`中只会有一个Class实例**

`Class`的方法

* `getName()`
* `getFields()`
* `getDeclaredField()`
* `getMethods()`
* `getDeclaredMethods()`
* `getConstructors()`
* `getCOnstructor(Class[] paraTypes)`
* `newInstance()`



```java
Person p1 = new Person();
Class c1 = p1.getClass();

Class c2 = Person.class;

Class c3 = Class.forName("com.ys.reflex.Person");


//获得类完整的名字
String className = c2.getName();
System.out.println(className);//输出com.ys.reflex.Person

//获得类的public类型的属性。
Field[] fields = c2.getFields();
for(Field field : fields){
   System.out.println(field.getName());//age
}

//获得类的所有属性。包括私有的
Field [] allFields = c2.getDeclaredFields();
for(Field field : allFields){
    System.out.println(field.getName());//name    age
}

//获得类的public类型的方法。这里包括 Object 类的一些方法
Method [] methods = c2.getMethods();
for(Method method : methods){
    System.out.println(method.getName());//work waid equls toString hashCode等
}

//获得类的所有方法。
Method [] allMethods = c2.getDeclaredMethods();
for(Method method : allMethods){
    System.out.println(method.getName());//work say
}

//获得指定的属性
Field f1 = c2.getField("age");
System.out.println(f1);
//获得指定的私有属性
Field f2 = c2.getDeclaredField("name");
//启用和禁用访问安全检查的开关，值为 true，则表示反射的对象在使用时应该取消 java 语言的访问检查；反之不取消
f2.setAccessible(true);
System.out.println(f2);

//创建这个类的一个对象
Object p2 =  c2.newInstance();
//将 p2 对象的  f2 属性赋值为 Bob，f2 属性即为 私有属性 name
f2.set(p2,"Bob");
//使用反射机制可以打破封装性，导致了java对象的属性不安全。
System.out.println(f2.get(p2)); //Bob

//获取构造方法
Constructor [] constructors = c2.getConstructors();
for(Constructor constructor : constructors){
    System.out.println(constructor.toString());//public com.ys.reflex.Person()
}

```

## 4. 根据反射获取父类属性

```java
public class Parent {
    public String publicField = "parent_publicField";
    protected String protectField = "parent_protectField";
    String defaultField = "parent_defaultField";
    private String privateField = "parent_privateField";

}

public class Son extends Parent {
    
}


public class ReflectionTest {

    @Test
    public void testGetParentField() throws Exception{
        Class c1 = Class.forName("com.ys.model.Son");
        //获取父类私有属性值
        System.out.println(getFieldValue(c1.newInstance(),"privateField"));
    }

    public static Field getDeclaredField(Object obj,String fieldName) {
        Field field = null;
        Class c = obj.getClass();
        for(; c != Object.class ; c = c.getSuperclass()){
            try {
                field = c.getDeclaredField(fieldName);
                field.setAccessible(true);
                return field;
            }catch (Exception e){
                //这里甚么都不要做！并且这里的异常必须这样写，不能抛出去。
                //如果这里的异常打印或者往外抛，则就不会执行c = c.getSuperclass(),最后就不会进入到父类中了
            }
        }
        return null;
    }
    public static Object getFieldValue(Object object,String fieldName) throws Exception{
        Field field = getDeclaredField(object,fieldName);

        return field.get(object);
    }
}




```

