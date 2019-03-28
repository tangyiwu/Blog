Java类加载过程

# 加载

把class字节码通过classLoader加载进内存

# 验证

校验字节流是否符合jvm规范

对于元数据的验证，比如该类是否继承了被final修饰的类？类中的字段是否与父类冲突？是否出现了不合理的重载？

对于字节码的验证，比如验证语义的合理性，验证类型转化的合理性

对于符号引用的验证，比如验证符号引用中通过全限定名是否可以找到对应的类？验证符号引号对应的变量和方法是否可以被当前类访问？

# 准备

为类变量分配内存并赋于初始值，比如8种基本类型是0，引用变量是null，常量初始值就是代码中给定的值，如`final static a = 123`，那么准备阶段a的初始值就是123.

# 解析

将**符号引用**替换成**直接引用**

- 符号引用：用来唯一标识变量、方法、类的相关信息

- 直接引用：一个内存地址或者一个偏移量。比如类方法，类变量的直接引用是指向方法区的指针；而实例方法，实例变量的直接引用是从实例的头指针算起到这个实例变量位置的偏移量。

  举个例子：

  ```
  public class Demo {
      public static void a() {}
      
      public void b() {}
  }
  
  Demo d = new Demo();
  ```

  在解析过程中，"a"和"b"是实例d的两个符号引用，分别标识静态方法a和实例方法b，实例d的内存地址是0xff101010，a、b的直接引用分别是0xff000100和1024，解析后，a、b的方法引用分别被替换成了0xff000100和（0xff101010+1024）

# 初始化

对类变量进行初始化，也就是对static修饰的变量和代码块进行初始化。

例如：

```
public class StaticFieldClass {

    static {
        System.out.println("first static block");
    }

    public StaticFieldClass() {
        System.out.println("constructor");
    }

    public static void staticMethod() {
        System.out.println("static method");
    }

    static {
        System.out.println("last static block");
    }

    public static int value = 123;
}

public class NotInitialization {
    public static void main(String[] args) {
		StaticFieldClass sfc = new StaticFieldClass();
    }
}
```

输出是：

```
first static block
last static block
constructor
```

