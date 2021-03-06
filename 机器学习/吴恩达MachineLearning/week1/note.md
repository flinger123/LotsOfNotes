# 1. Introduction
目前存在集中不同的机器学习算法，大概可以分为两种，一种是监督学习，另一种是无监督学习。
- 监督学习：给定已有正确的数据集，运用学习算法，算出更多正确的结果。
    - 回归问题：算法的输出为连续的值，即定量输出
    - 分类问题：算法的输出为离散的值，即定性输出
- 无监督学习：没有正确答案，只有一个数据集，让算法从中找到某种结构，典型例子就是聚类算法。

    鸡尾酒晏例子：看图

    ![](http://www.ai-start.com/ml2014/images/743c1d46d4288f8884f0981d437a15c1.png)

用算法把声音和音乐分开，使用Octave仅需要一行代码：
```octave
[W,s,v] = svd((repmat(sum(x.*x,1),size(x,1),1).*x)*x');
```

# 2. 单变量线性回归(Linear Regression with One Variable)

房价例子（监督学习/回归问题）：给定正确的俄勒冈州波特兰市的住房价格数据集，预测Size条件下房价Price的值；看图：

![](http://www.ai-start.com/ml2014/images/8e76e65ca7098b74a2e9bc8e9577adfc.png)

这个回归问题的数据集如图所示：

![](http://www.ai-start.com/ml2014/images/44c68412e65e62686a96ad16f278571f.png)

那么，在这里，我们把这个问题标记如下：

- ![m](https://latex.codecogs.com/gif.latex?m)代表训练集中实例的数量
- ![x](https://latex.codecogs.com/gif.latex?x)代表特征/输入变量
- ![y](https://latex.codecogs.com/gif.latex?y)代表目标变量/输出变量
- ![(x,y)](https://latex.codecogs.com/gif.latex?(x,y))代表训练集中的实例
- ![](https://latex.codecogs.com/gif.latex?%5Cleft%20%28%20x%5E%7B%28i%29%7D%2Cy%5E%7B%28i%29%7D%20%5Cright%20%29)代表第i个观察实例
- ![h](https://latex.codecogs.com/gif.latex?h)代表学习算法的解决方案或函数也称为假设（hypothesis）

![](http://www.ai-start.com/ml2014/images/ad0718d6e5218be6e6fce9dc775a38e6.png)

这个是监督学习的工作方式，其中![h](https://latex.codecogs.com/gif.latex?h)根据![x](https://latex.codecogs.com/gif.latex?x)的输入得出![y](https://latex.codecogs.com/gif.latex?y)值，那么也可以说![h](https://latex.codecogs.com/gif.latex?h)是从![x](https://latex.codecogs.com/gif.latex?x)到![y](https://latex.codecogs.com/gif.latex?y)的函数映射

我将选择最初的使用规则![h](https://latex.codecogs.com/gif.latex?h)代表hypothesis，因而，要解决房价预测问题，我们实际上是要将训练集“喂”给我们的学习算法，进而学习得到一个假设![h](https://latex.codecogs.com/gif.latex?h)，然后将我们要预测的房屋的尺寸作为输入变量输入给![h](https://latex.codecogs.com/gif.latex?h)，预测出该房屋的交易价格作为输出变量输出为结果。那么，对于我们的房价预测问题，我们该如何表达？
一种可能的表达式为：![h_{\theta }\left ( x \right )=\theta _{0}+\theta _{1}x](https://latex.codecogs.com/gif.latex?h_%7B%5Ctheta%20%7D%5Cleft%20%28%20x%20%5Cright%20%29%3D%5Ctheta%20_%7B0%7D&plus;%5Ctheta%20_%7B1%7Dx)，因为只含有一个特征/输入变量，因此这样的问题叫作**单变量线性回归问题**。

那么代价函数(Cost Function)![J(\theta _{0},\theta _{1})](https://latex.codecogs.com/gif.latex?J%28%5Ctheta%20_%7B0%7D%2C%5Ctheta%20_%7B1%7D%29)就为：![ JJ(\theta _{0},\theta _ {1})=\frac{1}{2}m\sum_{i=1}^{m}(h_{\theta }(x^{(i)})-y^{(i)})^2 ](https://latex.codecogs.com/gif.latex?J(\theta&space;_{0},\theta&space;_&space;{1})=\frac{1}{2}m\sum_{i=1}^{m}(h_{\theta&space;}(x^{(i)})-y^{(i)})^2)
这里的![1/2m](https://latex.codecogs.com/gif.latex?\frac{1}{2}m)的参数无论怎么改变，其实都是一样的，只不过最后的曲线会小一些罢了

我们的目标就是调整![\theta _{0}](https://latex.codecogs.com/gif.latex?%5Ctheta%20_%7B0%7D)和![\theta _{1}](https://latex.codecogs.com/gif.latex?%5Ctheta%20_%7B0%7D)使代价函数的结果最小，即使得出的函数曲线尽量贴合数据

上述例子中相关的式子：

![](http://www.ai-start.com/ml2014/images/10ba90df2ada721cf1850ab668204dc9.png)

我们将![\theta _{0 }](https://latex.codecogs.com/gif.latex?\theta&space;_{0&space;})简化掉得到![h_{\theta }(x)=\theta _{1}x](https://latex.codecogs.com/gif.latex?h_{\theta&space;}(x)=\theta&space;_{1}x)，代价函数在![\theta==1](https://latex.codecogs.com/gif.latex?\theta=1)时，![J(\theta _{1})=0](https://latex.codecogs.com/gif.latex?J(\theta&space;_{1})=0)，即h正确拟合，左边这条函数曲线（直线）对应了所有的数据

![](http://www.ai-start.com/ml2014/images/2c9fe871ca411ba557e65ac15d55745d.png)
## 2.1 轮廓图（等高线图）

略

## 2.2 梯度下降(Gradient Descent)

梯度下降是很常用的最小化函数的方式；我们在这里使用梯度下降算法求代价函数的![](https://latex.codecogs.com/gif.latex?J%28%5Ctheta%20_%7B0%7D%2C%5Ctheta%20_%7B1%7D%29)最小值。

梯度下降的思想是，给定一系列θ值，然后我们找到一个能让代价函数下降最多的值的集合，然后重复这个步骤知道找到局部的最小值（local minimum），但是我们没有尝试完所有的组合，所以这个最小值不是全局最小值（global minimum）

梯度下降的过程如图所示：

![](http://www.ai-start.com/ml2014/images/db48c81304317847870d486ba5bb2015.jpg)

**批量**梯度下降（batch gradient descent）算法的公式为：

![](http://www.ai-start.com/ml2014/images/7da5a5f635b1eb552618556f1b4aac1a.png)

- α是学习率（learning rate），它决定了我们让代价函数下降的步长。
- 在批量梯度下降中，我们每一次都会让所有的参数同时变化（即所有的参数减去学习速率乘以代价函数的导数）
- ![\alpha \frac{\partial }{\partial \theta _{0} }J(\theta _{0},\theta _{1})](https://latex.codecogs.com/gif.latex?%5Calpha%20%5Cfrac%7B%5Cpartial%20%7D%7B%5Cpartial%20%5Ctheta%20_%7B0%7D%20%7DJ%28%5Ctheta%20_%7B0%7D%2C%5Ctheta%20_%7B1%7D%29)和![\alpha \frac{\partial }{\partial \theta _{1} }J(\theta _{0},\theta _{1})](https://latex.codecogs.com/gif.latex?%5Calpha%20%5Cfrac%7B%5Cpartial%20%7D%7B%5Cpartial%20%5Ctheta%20_%7B1%7D%20%7DJ%28%5Ctheta%20_%7B0%7D%2C%5Ctheta%20_%7B1%7D%29)其实是微分项

### 2.2.1 梯度下降的直观理解

举例，我们的梯度下降算法如下：

![\theta _ {j} :=\theta _ {j}-\alpha \frac{\partial }{\partial \theta _{j}}J(\theta)](https://latex.codecogs.com/gif.latex?\theta&space;_&space;{j}&space;:=\theta&space;_&space;{j}-\alpha&space;\frac{\partial&space;}{\partial&space;\theta&space;_{j}}J(\theta&space;_{j}))

描述：对![西塔](https://latex.codecogs.com/gif.latex?\theta)赋值，使得按梯度下降最快方向进行，一直迭代下去，最终得到局部最小值。其中![阿尔法](https://latex.codecogs.com/gif.latex?\alpha)是学习率（learning rate），它决定了我们沿着能让代价函数下降程度最大的方向向下迈出的步子有多大。

对于这个问题，变成了求下图红色斜线的斜率，也就是那条红色的切线，当我们娶到如图中的切点时，我们求导得到了正斜率，这个式子就变成了![](https://latex.codecogs.com/gif.latex?\theta&space;_&space;{1}&space;:=\theta&space;_&space;{1}-\alpha&space;\frac{\partial&space;}{\partial&space;\theta&space;_{1}}J(\theta&space;_{1}))
通过它，我们得到了一个新的![西塔1](https://latex.codecogs.com/gif.latex?\theta&space;_&space;{1})，这个![](https://latex.codecogs.com/gif.latex?\theta&space;_&space;{1})等于![](https://latex.codecogs.com/gif.latex?\theta&space;_&space;{1})减去一个正数的斜率乘以![阿尔法](https://latex.codecogs.com/gif.latex?\alpha)

![](http://www.ai-start.com/ml2014/images/ee916631a9f386e43ef47efafeb65b0f.png)

这里涉及到了两个问题：
- ![阿尔法](https://latex.codecogs.com/gif.latex?\alpha)太大或者![阿尔法](https://latex.codecogs.com/gif.latex?\alpha)太小会出现什么情况？
- 如果直接把![西塔1](https://latex.codecogs.com/gif.latex?\theta&space;_&space;{1})放在局部最低点，接下来梯度下降算法接下来该怎么做？

首先第一个问题，![阿尔法](https://latex.codecogs.com/gif.latex?\alpha)太大的话梯度下降法可能会直接越过最低点，甚至无法收敛
<img heigth=550 width=890 src="pics/αtoolarge.png">
![阿尔法](https://latex.codecogs.com/gif.latex?\alpha)太小的话，即我的学习速率太小，需要很长时间才能移动到最低点；

第二个问题![阿尔法](https://latex.codecogs.com/gif.latex?\alpha)已经到最低点的时候，对这个点求导为0，即是这条上面那条红色斜线的斜率为0；那么这个时候我们的梯度下降算法式子为

![\theta _ {j} :=\theta _ {j}-\alpha \ast 0](https://latex.codecogs.com/gif.latex?\theta&space;_&space;{j}&space;:=\theta&space;_&space;{j}-\alpha&space;\ast&space;0)
即![\theta _ {j} :=\theta _ {j}](https://latex.codecogs.com/gif.latex?\theta&space;_&space;{j}&space;:=\theta&space;_&space;{j})，那么，到这里，梯度下降算法其实什么都没做，他也不会改变参数的值。那么这也解释了，为什么学习速率![阿尔法](https://latex.codecogs.com/gif.latex?\alpha)保持不变的时候，梯度下降也会收敛到最低点。

那么，在梯度下降的过程中，式子是怎么变化的呢？

举一个例子，如图代价函数![J(θ)](https://latex.codecogs.com/gif.latex?J(\theta))，我们要找到它的最小值，首先初始化我们的梯度下降算法，可以看出导数项对应的斜率是蛮陡的，但是当迭代多次之后，我们接近局部最低时，导数值会自动变得越来越小，所以梯度下降将自动采取较小的幅度，这就是梯度下降的做法。所以实际上没有必要再另外减小α

![](pics/αtozero.png)

**这就是梯度下降算法，你可以用它来最小化任何代价函数**

### 2.2.2 梯度下降的线性回归
我们谈到关于梯度下降算法，梯度下降是很常用的算法，它不仅被用在线性回归上和线性回归模型、平方误差代价函数。这部分内容，我们要将梯度下降和代价函数结合。我们将用到此算法，并将其应用于具体的拟合直线的线性回归算法里。


梯度下降算法和线性回归算法比较如图：

![](http://www.ai-start.com/ml2014/images/5eb364cc5732428c695e2aa90138b01b.png)

对我们之前的线性回归问题运用梯度下降法，关键在于求出代价函数的导数，即：
![\frac {\partial }{\partial \theta_{j}}J(\theta_{0},\theta_{1})=\frac {\partial }{\partial \theta_{j}}  \frac {1}{2m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)})-y^{(i)})^{2}](https://latex.codecogs.com/gif.latex?\frac&space;{\partial&space;}{\partial&space;\theta_{j}}J(\theta_{0},\theta_{1})=\frac&space;{\partial&space;}{\partial&space;\theta_{j}}&space;\frac&space;{1}{2m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)})-y^{(i)})^{2})

![j=0](https://latex.codecogs.com/gif.latex?j=0)时：![\frac {\partial }{\partial \theta_{0}}J(\theta_{0},\theta_{1})=\frac {1}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)})-y^{(i)})](https://latex.codecogs.com/gif.latex?\frac&space;{\partial&space;}{\partial&space;\theta_{0}}J(\theta_{0},\theta_{1})=\frac&space;{1}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)})-y^{(i)}))

![j=1](https://latex.codecogs.com/gif.latex?j=1)时：![\frac {\partial }{\partial \theta_{1}}J(\theta_{0},\theta_{1})=\frac {1}{m}\sum_{i=1}^{m}((h_{\theta}(x^{(i)})-y^{(i)})\cdot x^{(i)})](https://latex.codecogs.com/gif.latex?\frac&space;{\partial&space;}{\partial&space;\theta_{1}}J(\theta_{0},\theta_{1})=\frac&space;{1}{m}\sum_{i=1}^{m}((h_{\theta}(x^{(i)})-y^{(i)})\cdot&space;x^{(i)}))

应用梯度下降算法把上式改写成这样：

Repeat {

![\theta _{0}:=\theta _{0}-\alpha \frac {1}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)})-y^{(i)})](https://latex.codecogs.com/gif.latex?\theta&space;_{0}:=\theta&space;_{0}-\alpha&space;\frac&space;{1}{m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)})-y^{(i)}))

![\theta _{0}:=\theta _{0}-\alpha \frac {1}{m}\sum_{i=1}^{m}((h_{\theta}(x^{(i)})-y^{(i)})\cdot x^{(i)})](https://latex.codecogs.com/gif.latex?\theta&space;_{0}:=\theta&space;_{0}-\alpha&space;\frac&space;{1}{m}\sum_{i=1}^{m}((h_{\theta}(x^{(i)})-y^{(i)})\cdot&space;x^{(i)}))

}

这个算法叫做批量梯度下降，意思是指，在梯度下降算法的过程中，用到了所有的训练样本，即在公式中，每一次求导都要对结果求和，求了m次。

但在线性代数中，有一种计算代价函数最小值的方法，它可以在不需要多步梯度下降的情况下，也能解出代价函数的最小值，这是另一种称为**正规方程**(normal equations)的方法。实际上在数据量较大的情况下，梯度下降法比正规方程要更适用一些。

# 3. 线性代数回顾（Linear Algebra）

- 矩阵和向量定义

略

- 加法和矩阵标量乘法

行列相等的可以加，其他略

- 矩阵向量乘法

矩阵乘法：

![m\timesn](https://latex.codecogs.com/gif.latex?m\times&space;n)矩阵乘以![n\timeso](https://latex.codecogs.com/gif.latex?n\times&space;o)矩阵，变成![m\timeso](https://latex.codecogs.com/gif.latex?m\times&space;o)矩阵。

比如：

![](http://www.ai-start.com/ml2014/images/1a9f98df1560724713f6580de27a0bde.jpg)
![](http://www.ai-start.com/ml2014/images/5ec35206e8ae22668d4b4a3c3ea7b292.jpg)

矩阵乘法的性质：

矩阵的乘法不满足交换律：![A\times B\neq B\times A](https://latex.codecogs.com/gif.latex?A\times&space;B\neq&space;B\times&space;A)

矩阵的乘法满足结合律。即：![A\times (B \times C)=(A\times B) \times C](https://latex.codecogs.com/gif.latex?A\times&space;(B&space;\times&space;C)=(A\times&space;B)&space;\times&space;C)

单位矩阵：在矩阵的乘法中，有一种矩阵起着特殊的作用，如同数的乘法中的1,我们称这种矩阵为单位矩阵．它是个方阵，一般用![I](https://latex.codecogs.com/gif.latex?I)或者![E](https://latex.codecogs.com/gif.latex?E)表示；单位矩阵从左上角到右下角的对角线（称为主对角线）上的元素均为1以外全都为0。如：![A{{A}^{-1}}={{A}^{-1}}A=I](https://latex.codecogs.com/gif.latex?A{{A}^{-1}}={{A}^{-1}}A=I)

对于单位矩阵有下式![](https://latex.codecogs.com/gif.latex?AI=IA=A)

- 逆、转置（Inverse and Transpose）

矩阵的逆：如矩阵![A](https://latex.codecogs.com/gif.latex?A)是一个![](https://latex.codecogs.com/gif.latex?m\times&space;n)的矩阵，对于它的逆矩阵有，![A{{A}^{-1}}={{A}^{-1}}A=I](https://latex.codecogs.com/gif.latex?A{{A}^{-1}}={{A}^{-1}}A=I)

矩阵的转置：设![A](https://latex.codecogs.com/gif.latex?A)为![](https://latex.codecogs.com/gif.latex?m\times&space;n)阶矩阵（即![m](https://latex.codecogs.com/gif.latex?m)行![n](https://latex.codecogs.com/gif.latex?n)列），第![i](https://latex.codecogs.com/gif.latex?i)行![j](https://latex.codecogs.com/gif.latex?j)列的元素是![a(i,j)](https://latex.codecogs.com/gif.latex?a(i,j))，即：![A=a(i,j)](https://latex.codecogs.com/gif.latex?A=a(i,j))

定义![A](https://latex.codecogs.com/gif.latex?A)的转置为这样一个![](https://latex.codecogs.com/gif.latex?n\times&space;m)阶矩阵![B](https://latex.codecogs.com/gif.latex?B)，满足![B=a(j,i)](https://latex.codecogs.com/gif.latex?B=a(j,i))，即![b (i,j)=a(j,i)](https://latex.codecogs.com/gif.latex?b&space;(i,j)=a(j,i)),记![{{A}^{T}}=B](https://latex.codecogs.com/gif.latex?{{A}^{T}}=B)。（有些书记为A'=B）

例：

![](https://latex.codecogs.com/gif.latex?%7B%7B%5Cleft%7C%20%5Cbegin%7Bmatrix%7D%20a%26%20b%20%5C%5C%20c%26%20d%20%5C%5C%20e%26%20f%20%5C%5C%5Cend%7Bmatrix%7D%20%5Cright%7C%7D%5E%7BT%7D%7D%3D%5Cleft%7C%5Cbegin%7Bmatrix%7D%20a%26%20c%20%26%20e%20%5C%5C%20b%26%20d%20%26%20f%20%5C%5C%5Cend%7Bmatrix%7D%20%5Cright%7C)

矩阵的转置基本性质：

![{{\left( A\pm B \right)}^{T}}={{A}^{T}}\pm {{B}^{T}}](https://latex.codecogs.com/gif.latex?{{\left(&space;A\pm&space;B&space;\right)}^{T}}={{A}^{T}}\pm&space;{{B}^{T}})

![{{\left( A\times B \right)}^{T}}={{B}^{T}}\times {{A}^{T}}](https://latex.codecogs.com/gif.latex?{{\left(&space;A\times&space;B&space;\right)}^{T}}={{B}^{T}}\times&space;{{A}^{T}})

![{{\left( {{A}^{T}} \right)}^{T}}=A](https://latex.codecogs.com/gif.latex?{{\left(&space;{{A}^{T}}&space;\right)}^{T}}=A)

![{{\left( KA \right)}^{T}}=K{{A}^{T}} ](https://latex.codecogs.com/gif.latex?{{\left(&space;KA&space;\right)}^{T}}=K{{A}^{T}})

