## Chapter 3 神经网络

#### 3.1感知机模型

$y= \begin{cases}0 & \left(b+w_1 x_1+w_2 x_2 \leqslant 0\right) \\ 1 & \left(b+w_1 x_1+w_2 x_2>0\right)\end{cases}$

b是被称为偏置的参数，用于控制神经元被激活的容易程度；而**w**1**和**w**2**是表示各个信号的权重的参数，用于控制各个信号的重要性。

```
一般而言，“朴素感知机”是指单层网络，指的是激活函数使用了阶跃函数
```

**A** 的模型。“多层感知机”是指神经网络，即使用**sigmoid**函数（ 后述）等平滑的激活函数的多层网络。

---

#### 3.2激活函数

##### S**igmoid函数**（**sigmoid function**）：

$h(x)=\frac{1}{1+\exp (-x)}$

阶跃函数的实现：

```python
def step(x):
	if x>0:
		return 1;
	else:
		return 0;
```

```python
def step_function(x):
	y = x > 0 #y的结果为bool值，若x为ndarray，y为bool数组
	return y.astype(np.int) #bool数组转换为int数组，True为1
```

```
感知机中神经元之间流动的是0或1的二元信号，而神经网络中流动的是连续的实数值信号(激活函数为sigmoid函数)。
```

##### ReLU函数

$h(x)= \begin{cases}x & (x>0) \\ 0 & (x \leqslant 0)\end{cases}							$

```python
def ReLU(x)
	return np.maxmum(0,x)

```

---

#### 3.5输出层的设计

机器学习的问题大致可以分为分类问题和回归问题。分类问题是数据属于哪一个类别的问题。比如，区分图像中的人是男性还是女性的问题就是分类问题。而回归问题是根据某个输入预测一个（连续的）数值的问题。比如，根据一个人的图像预测这个人的体重的问题就是回归问题（类似“57.4kg”这样的预测）。

神经网络可以用在分类问题和回归问题上，不过需要根据情况改变输出层的激活函数。一般而言，回归问题用恒等函数，分类问题用softmax函数。

##### Softmax

分类问题中使用的softmax函数可以用下面的式表示

    $	y_k=\frac{\exp \left(a_k\right)}{\sum_{i=1}^n \exp \left(a_i\right)}$

上面的softmax函数的实现虽然正确描述了式，但在计算机的运算上有一定的缺陷。这个缺陷就是溢出问题。

$\begin{aligned} y_k=\frac{\exp \left(a_k\right)}{\sum_{i=1}^n \exp \left(a_i\right)} & =\frac{\mathrm{C} \exp \left(a_k\right)}{\mathrm{C} \sum_{i=1}^n \exp \left(a_i\right)} \\ & =\frac{\exp \left(a_k+\log \mathrm{C}\right)}{\sum_{i=1}^n \exp \left(a_i+\log \mathrm{C}\right)} \\ & =\frac{\exp \left(a_k+\mathrm{C}^{\prime}\right)}{\sum_{i=1}^n \exp \left(a_i+\mathrm{C}^{\prime}\right)}\end{aligned}$


$$
\ln (c)=-\max (a)
$$

```python
def softmax(a):
c = np.max(a)
exp_a = np.exp(a - c) # 溢出对策
sum_exp_a = np.sum(exp_a)
y = exp_a / sum_exp_a
return y
```

求解机器学习问题的步骤可以分为 “学习” (1) 和 “推理” 两个阶段。首先, 在学习阶段进行模型的学习 ${ }^2$, 然后, 在推理阶段, 用学到的模型对未知的数据进行推理 (分类)。如前所述, 推理阶段一般会省略输出层的 softmax 函数。在输出层使用 softmax 函数是因为它和神经网络的学习有关系 (详细内容请参考下一章)。

预处理在神经网络（深度学习）中非常实用，其有效性已在提高识别性能和学习的效率等众多实验中得到证明。在刚才的例子中，作为一种预处理，我们将各个像素值除以 255，进行了简单的正规化。实际上，很多预处理都会考虑到数据的整体分布。比如，利用数据整体的均值或标准差，移动数据，使数据整体以 0为中心分布，或者进行正规化，把数据的延展控制在一定范围内。除此之外，还有将数据整体的分布形状均匀化的方法，即数据白化（whitening）等。

#### Summary

本章所学的内容

- 神经网络中的激活函数使用平滑变化的 sigmoid 函数或 ReLU 函数。
- 通过巧妙地使用 NumPy 多维数组, 可以高效地实现神经网络。
- 机器学习的问题大体上可以分为回归问题和分类问题。
- 关于输出层的激活函数, 回归问题中一般用恒等函数, 分类问题中一般用 softmax 函数。
- 分类问题中, 输出层的神经元的数量设置为要分类的类别数。
- 输入数据的集合称为批。通过以批为单位进行推理处理, 能够实现高速的运算。
