# Java虚拟机
*Java虚拟机包括一套字节码指令集合，一组寄存器，一个栈，一个垃圾回收堆，和一个存储方法域*
Java虚拟机可以一次一条指令的方式解释字节码（映射到实际的处理器指令），或者由JIT编译器进一步编译
* 执行字节码时，把字节码解释成具体平台上的机器指令执行

高级用法
* 拓展Java语言
* 将其他语言编译成Java字节码
* JVM只设置了4个寄存器 pc, optop, frame, vars
作为基于栈结构的计算机，Java栈是JVM存储信息的主要方法。
当JVM得到一个Java字节码应用程序后，便为该代码中一个类的每一个方法创建一个栈框架，以保存该方法的
状态信息