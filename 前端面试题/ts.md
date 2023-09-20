1.ts与js比较

| ts       | js       |
| -------- | -------- |
| 静态编译 | 动态执行 |

 <b><font color='black' size=3 face="">2.ts相比 JS 的优势</font></b> 

1. 更早(写代码的同时)发现错误， <b><font color='SEAGREEN' size=3 face="">  <b><font color='red' size=3 face=""><b><font color='black' size=3 face=""> <b><font color='black' size=3 face="">减少找 Bug、改 Bug 时间</font></b> </font></b> </font></b></font></b>  ，提升开发效率。

2. 程序中任何位置的代码都有 <b><font color='red' size=3 face="">代码提示</font></b>  ，随时随地的安全感，增强了开发体验。

3. 强大的 <b><font color='red' size=3 face="">类型系统</font></b> 提升了代码的可维护性，使得 <b><font color='red' size=3 face="">重构代码更加容易</font></b> 。

4. 支持 <b><font color='red' size=3 face="">最新的 ECMAScript 语法</font></b>  ，优先体验最新的语法，让你走在前端技术的最前沿。

5. TS  <b><font color='red' size=3 face="">类型推断</font></b> 机制， <b><font color='red' size=3 face=""> 不需要</font></b> 在代码中的 <b><font color='red' size=3 face="">每个地方都显示标注类型</font></b>  ，让你在享受优势的同时，尽量降低了成本。

除此之外， Vue 3 源码使用 TS 重写、 Angular 默认支持 TS、 React 与 TS 完美配合， TypeScript 已成为大中型前端 项目的首先编程语言。

 <b><font color='black' size=3 face="">3.TS概述</font></b> 

TypeScript 是 JS 的超集， TS 提供了 JS 的所有功能，并且额外的增加了： <b><font color='red' size=3 face=""> 类型系统</font></b> 。

4.ts基础类型概述

1 JS 已有类型 2 TS 新增类型

| js已有类型                                                   | ts新增类型                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 原始类型：  <b><font color='black' size=3 face="">number/string/boolean/null/undefined/symbol</font></b>   <br /> 对象类型 ： object (包括， <b><font color='black' size=3 face="">数组、对象、函数</font></b> 等对象)。 | <b><font color='black' size=3 face="">联合类型、自定义类型(类型别名)、接口、元组、字面量类型、枚举、 void、 any </font></b> 等 |

4.ts接口

当一个对象类型被多次使用时， 一般会使用 <b><font color='black' size=3 face="">接口 ( interface)</font></b> 来描述对象的类型， 达到 <b><font color='red' size=3 face="">复用</font></b> 的目的

 <b><font color='red' size=3 face="">interface</font></b> 

![image-20230920174825713](C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230920174825713.png)

5.接口继承extends 

如果两个接口之间有相同的属性或方法，可以 <b><font color='red' size=3 face="">将公共的属性或方法抽离出来 ，通过继承来实现复用</font></b> 

6.元组

它确切地知道包含多少个元素 ，以及特定索引对应的类型

![image-20230920175110047](C:\Users\十年之火\AppData\Roaming\Typora\typora-user-images\image-20230920175110047.png)

1. 元组类型可以确切地标记出有多少个元素，以及每个元素的类型。

2. 该示例中，元素有两个元素，每个元素的类型都是 number。

7.let 与 const

let指变量

const指常量



8.any类型

可以对该值进行任意操作 ，并且不会有代码提示



9.TypeScript 高级类型

class 类、类型兼容性、交叉类型、泛型(参数和返回值类型相同)、索引签名类型、映射类型（ <b><font color='black' size=3 face="">基于旧类型创建新类型(对象类型)</font></b>  ）