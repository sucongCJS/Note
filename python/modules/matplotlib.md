# 动图

```python
import matplotlib.pyplot as plt
import matplotlib.animation as animation  # 制作动图
import numpy as np

fig, ax = plt.subplots()

x = np.arange(0, 2*np.pi, 0.01)
line, = ax.plot(x, np.sin(x)) # 返回类型得是可迭代对象, 加上逗号变元组最方便, 也可以讲 line, 写成 [line]

# 
def animate(i):
    line.set_ydata(np.sin(x+i/10))
    return line, 

# 初始化
def init(): 
    line.set_ydata(np.sin(x))
    return line,

# 验证返回值是元组: print(type(init()))

ani = animation.FuncAnimation(fig=fig, func=animate, frames=100, init_func=init, interval=20, blit=True)


plt.show()

```

