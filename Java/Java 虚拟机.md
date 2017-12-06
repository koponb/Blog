Java 的标准运行环境（JRE）包含 Java API 类库和 Java虚拟机（JVM）两部分。JVM 主要是将字节码文件（.class）解释成为特定的机器码进行运行并对其运行时内存进行管理， 使得 Java 程序具备了 “write once,run anywhere” 的跨平台特性。

# 1 Run-Time Data Areas（运行时数据区）

JVM 在执行程序时会把它管理的内存划分为各种运行时数据区域。其中有些数据区域是在 JVM 启动时创建的，只有在 JVM 退出时才会被销毁。其他数据区域跟随用户线程的创建和结束而建立和销毁。

JVM 所管理的内存包含如下几个运行时数据区域。

![](https://raw.githubusercontent.com/937447974/Blog/master/Resources/2017120601.png)

## 1.1 The pc Register（程序计数器）

JVM 可以同时执行多个线程，每个线程都有自己的 pc（程序计数器）寄存器。在任何时候，每个 JVM 线程都只会执行一个方法的代码，该方法称为线程的当前方法。 JVM 字节码解释器通过改变这个计数器的值来选取线程的下一条执行指令，如果这个方法是 Java 方法，那 PC 寄存器就保存 JVM 正在执行的字节码指令地址；如果该方法是 native 的，那 PC 寄存器的值是空（undefined）。

PC 寄存器占用较小的内存空间，容量至少应当能保存一个 returnAddress 类型的数据或一个本地指针，且该区域是唯一不会抛出 OutOfMemoryError 情况的区域。

## 1.2 Java Virtual Machine Stacks（虚拟机栈）

每个 JVM 线程都有一个私有的 JAVA 虚拟机栈，它与线程同时创建，主要保存 Java 方法的栈帧（Stack Frame）。每个方法的执行都会创建一个栈帧，随着方法调用而创建（入栈），随着方法结束而销毁（出栈）。

### 1.2.1 栈帧

栈帧是方法运行的基础结构，其中涉及如下信息：

1. Local Variables（局部变量）：局部变量表存放了编译期可知的各种基本数据类型（boolean, byte, char, short, int, float）、引用对象类型（reference）和 returnAddress 类型。
2. Operand Stacks（操作数栈）：JVM 的指令集基于栈，所有的计算逻辑都需要通过栈来完成，这个栈就是操作数栈。操作数栈的大小由 Java 编译器在编译期计算，计算结果记录在class文件的stack值。
3. Dynamic Linking（动态链接）：每一个栈帧内部都包含一个指向运行时常量池的引用，来支持当前方法的执行过程中实现动态链接。在 Class 文件里面，描述一个方法调用了其他方法，或者访问其成员变量是通过符号引用来表示的。动态链接将这些符号引用方法转换为具体的方法引用，将变量引用转换为运行时的栈偏移量地址。通过这种方式保证我们只需要编译修改的文件即可使程序正常运行。
4. Normal Method Invocation Completion（正常返回）：程序运行正常的返回处理。
5. Abrupt Method Invocation Completion（异常返回）：程序运行异常的返回处理逻辑。

### 1.2.2 异常

JVM 堆栈的错误操作会引起下面的异常：

1. 如果线程请求分配的栈深度超过 JVM 栈允许的最大深度时，会抛出 StackOverflowError 异常。如嵌套方法死循环调用。
2. 如果 JVM 栈动态扩展无法申请到足够的内存，或建立新的线程没有足够的内存去创建对应的虚拟机栈时，会抛出 OutOfMemoryError 异常；

## 1.3 Native Method Stacks（本地方法栈）

本地方法栈和虚拟机栈的功能一样，主要用于保存 native 方法的栈帧。

## 1.4 Heap (堆)

JVM 内控制一个堆，被所有 Java 虚拟机线程共享。堆随JVM的创建和结束而建立和销毁，主要用于存储所有类实例和数组。

### 1.4.1 垃圾回收

对象的堆存储是由垃圾回收机制自动管理的，用户无须显示的释放。Java 堆分为

1. 算法
2. 优化

### 1.4.2 异常

## 1.4 Method Area（方法区）

## 1.5 Run-Time Constant Pool（运行时常量池）


G1 eden space
G1 Old Gen
G1 survivor space

metaspace
codeheap profiled nmethods
codeheap non-nmethods
compressed class space
codeheap non-profiled nmethods

Eden Space (heap): The pool from which memory is initially allocated for most objects.

Survivor Space (heap): The pool containing objects that have survived the garbage collection of the Eden space.

Tenured Generation (heap): The pool containing objects that have existed for some time in the survivor space.

Permanent Generation (non-heap): The pool containing all the reflective data of the virtual machine itself, such as class and method objects. With Java VMs that use class data sharing, this generation is divided into read-only and read-write areas.

Code Cache (non-heap): The HotSpot Java VM also includes a code cache, containing memory that is used for compilation and storage of native code.

https://docs.oracle.com/javase/9/management/using-jconsole.htm#GUID-A81AE10A-0693-462A-B129-5E292F46523E__FIGURE3-7GENERATIONSOFDATAINGARBAGE-8F135AA1


# 2 OOM 优化

# 3 垃圾回收


# 4 Class 字节码

# 5 类的生命周期



&#160;

----------

# Appendix

## Related Documentation

[揭秘Java虚拟机（JVM设计原理与实现）](http://product.dangdang.com/25111315.html)

[深入Java虚拟机(第二版)](http://product.dangdang.com/23259731.html)

[The Java® Virtual Machine Specification](https://docs.oracle.com/javase/specs/jvms/se9/html/index.html)

[Java内存区域 JVM运行时数据区](http://blog.csdn.net/tjiyu/article/details/53915869)

## Revision History

| 时间 | 描述 |
| ---- | ---- |
| 2017-10-26 | 博文完成 |

## Copyright

CSDN：http://blog.csdn.net/y550918116j

GitHub：https://github.com/937447974