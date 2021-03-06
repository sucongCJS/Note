# 面向对象

类是对对象的抽象

抽象类是对类的抽象

接口是对行为的抽象

# 关系

- 接口：空心圆+直线（唐老鸭类实现了‘讲人话’）；
- 依赖：虚线+箭头（动物和空气的关系）；
- 关联：实线+箭头（企鹅需要知道气候才迁移）；
- 聚合：空心四边形(指向总, 雁群)+实线+箭头（雁群和大雁的关系）；
- 合成/组合：实心四边形+实线+箭头（鸟和翅膀的关系）；
- 泛化/继承：空心三角形+实线（动物和鸟的继承关系）；
- 实现：空心三角形+虚线（实现大雁飞翔的接口）； 

# 类图

## 设计模式

![image-20191124123022711](D:\Note\软工\term.assets\image-20191124123022711.png)

![image-20191124133620420](D:\Note\软工\term.assets\image-20191124133620420.png)

![image-20191124142923966](D:\Note\软工\term.assets\image-20191124142923966.png)

# 时序图

![image-20191124155329627](D:\Note\软工\term.assets\image-20191124155329627.png)

 **同步消息=**=调用消息（Synchronous Message）

 消息的发送者把控制传递给消息的接收者，然后停止活动，等待消息的接收者放弃或者返回控制。用来表示同步的意义。

 **异步消息（Asynchronous Message**）

 消息发送者通过消息把信号传递给消息的接收者，然后继续自己的活动，不等待接受者返回消息或者控制。异步消息的接收者和发送者是并发工作的。

 **返回消息（Return Message**）

 返回消息表示从过程调用返回

###  自关联消息（Self-Message）

 表示方法的自身调用以及一个对象内的一个方法调用另外一个方法。

# 原则

![image-20191124193738398](D:\Note\软工\term.assets\image-20191124193738398.png)

![image-20191124193750784](D:\Note\软工\term.assets\image-20191124193750784.png)

![image-20191124200532664](D:\Note\软工\term.assets\image-20191124200532664.png)

![image-20191124195835071](D:\Note\软工\term.assets\image-20191124195835071.png)