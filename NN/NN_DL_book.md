[Neural_Networks and Deep_Learning](http://neuralnetworksanddeeplearning.com/chap1.html)

修改单个 perceptron 的权重和偏置去达到想要的output可能会导致其他的 perceptron 也发生很大的变化, 我们需要 gradually modify 权重和偏置来达到想要的结果, 所以可以使用一种 artificial neuron 叫做 sigmoid neuron. 对于权值和偏置做小的修改智慧导致结果有小的改变

而且sigmoid有斜率, 并不是非零即一的函数, 所以才能梯度下降

# ?
1. 三层的识别手写数字识别为什么用 10 个 output neurons? 而不用4个? (一个neurons 有01两种值, 4个总共能表示 $2^4$ = 16 个呢)
the ultimate justification is empirical(经验主义的)

除去输入输出层, 单单一层隐藏层无法将图像和比特 0 1 联系起来, 因为神经网络是通过图像来识别数字的

需要再加一层

# feedforward neural networks
there are no loops in the networks - information is always fed forward, never fed back.

- each neurons can have different values of weights and biases
-

# words
- calculus 微积分
- derivatives 导数
