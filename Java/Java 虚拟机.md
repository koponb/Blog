Java 的标准运行环境（JRE）包含 Java API 类库和 Java虚拟机（JVM）两部分。JVM 主要是将字节码文件（.class）解释成为特定的机器码进行运行并对其运行时内存进行管理， 使得 Java 程序具备了 “write once,run anywhere” 的跨平台特性。

# 1 Run-Time Data Areas（运行时数据区）

JVM 在执行程序时会把它管理的内存划分为各种运行时数据区域。其中有些数据区域是在 JVM 启动时创建的，只有在 JVM 退出时才会被销毁。其他数据区域跟随用户线程的创建和结束而建立和销毁。

JVM 所管理的内存包含如下几个运行时数据区域。

 

## 1.1 The pc Register（程序计数器）
## 1.2 Java Virtual Machine Stacks（虚拟机栈）
## 1.6 Native Method Stacks（本地方法栈）

## 1.3 Heap (堆)
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


# 2 OOM

# 3 垃圾回收

## 引用

# 4 Class 字节码

# 5 类的生命周期

![](https://raw.githubusercontent.com/937447974/Blog/master/Resources/2015111101.png)

&#160;

----------

# Appendix

## Related Documentation

[揭秘Java虚拟机（JVM设计原理与实现）](http://product.dangdang.com/25111315.html)

[深入Java虚拟机(第二版)](http://product.dangdang.com/23259731.html)

[The Java® Virtual Machine Specification](https://docs.oracle.com/javase/specs/jvms/se9/html/index.html)

## Revision History

| 时间 | 描述 |
| ---- | ---- |
| 2017-10-26 | 博文完成 |

## Copyright

CSDN：http://blog.csdn.net/y550918116j

GitHub：https://github.com/937447974