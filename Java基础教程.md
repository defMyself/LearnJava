# Java基础教程

## 基本数据类型
## 面向对象
## Java设计模式
## Java虚拟机

## Java程序的编译执行
Java中的编译分为两个部分
1. 源码文件编译成字节码文件（前端编译）
2. 字节码文件被虚拟机加载后编译成机器码（后端编译）

在后端编译中，虚拟机再运行过程中做一些编译流程，将字节码转换成可悲虚拟机识别执行的机器码

* 前端包括词法分析，语法分析，语义分析，中间代码生成
* 词法分析产生字符流
* 语法分析产生语法树
* 语义分析产生语法树
* 前端产生中间代码

* 后端编译由中间代码开始，包括机器无关代码优化，代码生成，机器相关代码优化

## 前端编译
前端编译主要流程：
1. 对源文件进行词法分析产生字符流
2. 对字符流进行语法分析产生抽象语法树
3. 对语法树进行语义分析，确保语义正常
4. 语义分析通过以后生成中间代码（字节码）

具体到javac, 编译过程大致分为：
1. 解析与填充符号表
2. 插入式注解处理器的处理注解
3. 语义分析与字节码生成


* Java源文件是一个个字符构成，编译器所能识别的是Token。需要通过词法分析将字符流转换成Tokenji集合
```java
int a = b + c;
```

IDEA JDT AstView插件可以查看抽象语法树

* 词法分析主要由com.sum.tools.javac.parser.Scannaer类来实现
* 根据Token集合生成抽象语法树，每一个节点代表着程序代码中的一个语法结构

```java
public class HelloWorld {
        public static void main(String[] args) {
                System.out.println("Hello world");
        }
}
```

```shell
javac HelloWorld.java
```

```shell
javac HelloWorld
```

*ClassFile*结构
```c

ClassFile {
  u4             magic; // 魔数，固定值 0xCAFEBABE
  u2             minor_version; // 副版本号
  u2             major_version; // 主版本号
  u2             constant_pool_count; // 常量池计数器
  cp_info        constant_pool[constant_pool_count-1]; // 常量池
  u2             access_flags; // 访问标志
  u2             this_class; // 类索引
  u2             super_class; // 父类索引
  u2             interfaces_count; // 接口计数器
  u2             interfaces[interfaces_count]; // 接口表
  u2             fields_count; // 字段计数器
  field_info     fields[fields_count]; // 字段表
  u2             methods_count; // 方法计数器
  method_info    methods[methods_count]; // 方法表
  u2             attributes_count; // 属性计数器
  attribute_info attributes[attributes_count]; // 属性表
}

```
*整个classfile文件是一张表*

* 常量池中存放的两种常量：字面量和符号引用
* 符号引用分为三类：类和接口的全限定符，字段的名称和描述符，方法名称和描述符