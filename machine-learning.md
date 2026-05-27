# machine learning

# what is machine learning

* supervised learning ==used most==
* Unsupervised learning

## supervised learning

learn to map input(x) to output(y)

learn from being given `right answers`

* regression （回归）: predict a number
  * infinitely many possible outputs

* classification(分类)：predict categories
  * small number of possible outputs
  * inputs can be more than one 

## unsupervised learning

Data only comes with inputs x,but not output labels y.

* x also called feature
  * 字面意思理解，可以理解为某个东西的特征，比如预测房价，x可以是size of house,也可以多维预测，加上the number of bedroom等
* y also called target
* $\hat{y}$ means the predicted value

Algorithm has to find structure in the data.

![image-20260428125917066](machine-learning.assets/image-20260428125917066.png)

* clustering(聚类)

## linear regression model



## cost function

![image-20260428161732083](machine-learning.assets/image-20260428161732083.png)

* parameters: variables you can adjust to improve the model
* also called coefficients or weights(权重)

![image-20260428162302425](machine-learning.assets/image-20260428162302425.png)

* divided by 2m can help us compute easily later

* so it's important to find $w,b$ to minimize the cost function $J$.

## Gradient descent（梯度下降）

* used widely ==very important==

Have some function  $$J(w,b)$$

Want $$\min_{w, b} J(w, b)$$

![image-20260428165553135](machine-learning.assets/image-20260428165553135.png)

* choose a starting point at the surface by choosing starting value for $w,b $ 
* choose the direction that take you downhill quickly
* different starting point may lead you to different local minima(局部最小值)

## Gradient descent algorithm

$$w = w - \alpha \frac{\partial}{\partial w} J(w, b)$$

$$b = b - \alpha \frac{\partial}{\partial b} J(w, b)$$

- **$w$**: The **Weight/Parameter** (参数/权重) that the model is trying to learn.
- **$\alpha$ **: The **Learning Rate** (学习率).
  - determines the **step size** during each iteration 
- **$\frac{\partial}{\partial w} J(w, b)$**: The **Derivative** or **Gradient** (导数或梯度).
  - It represents the slope of the cost function at the current point (代表当前位置代价函数的斜率).
  - It tells the algorithm which direction to move to reach the lowest point (它告诉算法为了到达最低点应该朝哪个方向移动).

![image-20260428171433306](machine-learning.assets/image-20260428171433306.png)

* Simultaneously update $w$ and $b$

## Learning rate

![image-20260428172637104](machine-learning.assets/image-20260428172637104.png)

![image-20260428172919831](machine-learning.assets/image-20260428172919831.png)

* notice that if we use convex function(凸函数),it will always converge to the global minimum(the only one minima)

## "batch" gredient descent

* batch: Each step of gradient descent ==uses all the training examples== 
  * in this case, we use the cost function which uses all the training examples to compute error.

![image-20260428175327787](machine-learning.assets/image-20260428175327787.png)



## Feature scaling

![image-20260429230146949](machine-learning.assets/image-20260429230146949.png)

![image-20260429230551268](machine-learning.assets/image-20260429230551268.png)

* sometimes the range of one feature may be very big so a little change of $w_1$ can make a big difference.
* the contours(等高线) are so tall and skinny
* 

* if different features take on very different ranges of values, it can cause gradient descent to run slowly.

* 

## Mean normalization

![image-20260429231730923](machine-learning.assets/image-20260429231730923.png)

* feature's value

![image-20260429232130930](machine-learning.assets/image-20260429232130930.png)



* 如果不归一化，有些参数就会更快地收敛到最佳值，有些收敛非常慢，从表达式也看的出来，因为他们共用一个学习率但是梯度相差非常大

* 归一化之后训练速度会变得非常非常快！

  ![image-20260502161309259](machine-learning.assets/image-20260502161309259.png)

## Cost fuction curve

![image-20260429234526107](machine-learning.assets/image-20260429234526107.png)

![image-20260429234845846](machine-learning.assets/image-20260429234845846.png)

* if cost increases sometimes, it means a too big learning rate, or some mistakes in code.
* can choose a very very small $\alpha$ to see if the cost decreases(as debug)

![image-20260429235231793](machine-learning.assets/image-20260429235231793.png)

## Feature engineering

> Using intuition to design new features, by transforming or combining original features

for $f=w_1x_1+w_2x_2+b$ 

we can set $x_3=x_1x_2$

then we get $f=w_1x_1+w_2x_2+w_3x_3+b$ 

it may be better than the original model

## Polynomial regression(多项式回归)

* feature scaling is very important

![image-20260502162645810](machine-learning.assets/image-20260502162645810.png)

# Classification

* class=category
* binary classification: y can only be one of two values

![image-20260502213900955](machine-learning.assets/image-20260502213900955.png)

## logistic regression

![image-20260504144757188](machine-learning.assets/image-20260504144757188.png)

logistic regression model

![image-20260504144952803](machine-learning.assets/image-20260504144952803.png)

* output represent the probabilit



* if we set a threshold of 0.5, we can get:![image-20260504145749808](machine-learning.assets/image-20260504145749808.png)

## Decision boundary

## Cost function

![image-20260504152633333](machine-learning.assets/image-20260504152633333.png)

* if we use squared error cost, the cost function is a non-convex function, which means we usually get the local minima instead of global minimum by gradient descent

![image-20260504153139922](machine-learning.assets/image-20260504153139922.png)

![image-20260504153233456](machine-learning.assets/image-20260504153233456.png)

![image-20260504153347484](machine-learning.assets/image-20260504153347484.png)

* a more simple way to write this formula
* 这个模型是通过最大似然估计推导的，基本所有都在用这个

# overfitting（过拟合）

* bias：偏差
* underfit（欠拟合）:also called high bias, Does not fit the training set well
  * 可以这样理解，偏差就是偏，意思是没命中把心，就是模型没有精确命中train set上的点

* generalization(泛化): make good predictions on new examples that it has never seen before
* overfitting : also called high variance(高方差),fits the training set extremely well but cannot generalize well.
  * 因为可能同一个训练集训练出来的函数很不一样，所有叫高方差
  * 方差反应波动程度，高方差意思是模型弯弯绕绕的，所以过拟合
  * 成本函数可能接近0但是效果很差

![image-20260505214639624](machine-learning.assets/image-20260505214639624.png)

so the aim of machine learning is to find a model which is neither underfitting nor overfitting

## Addressing Overfitting

* collect more training examples
* use fewer features 
  * all features + insufficient data -> overfitting
  * subset of these features may be just right
  * regularization(正则化)
* note that we can set a parameter as 0 to eliminate  a feature, and if parameter is small enough, it can also work well

## Cost Function with Regularization

![image-20260505231254900](machine-learning.assets/image-20260505231254900.png)

* $\lambda$ is also a value we should choose(like learning rate $\alpha $)
  * if $\lambda $ is too small,this model will ==overfit==
    * 因为后面的正则项几乎不会起作用
  * if $\lambda $ is enormous, this model will ==underfit==
    * 后面正则项非常大，导致各个参数接近于0，最后得到一个$y=b$ 的直线
* This model will try to keep $w_j$ small
* 这个方法常常可以带来一个比较平滑，波动不大的拟合

![image-20260506001104853](machine-learning.assets/image-20260506001104853.png)

this derivation shows that:

what regularization is doing on every single iteration of gradient descent is you're multiplying $w$ by a number slightly less than 1 and that has the effect of shrinking the value of $w_j$ just a little bit

## Regularized Logistic Regression

和回归思路一样的

# Deep Learning

ne

![image-20260506220047924](machine-learning.assets/image-20260506220047924.png)

* a layer is a grouping of neurons which take as input the same or similar features and that in turn output a few numbers together(can have one or more neurons)

* Input layer: The first layer of the network that receives raw data or "features"
* Hidden Layer: The layers between the input and output. 
  * They are called "hidden" because their values aren't seen in the final output;
  * we don't need to decide what are the features(such as affordability,awareness and so on), it can figure out all features it wants to use in this hidden layer
  * each neuron in a certain layer will have access to every feature from the previous layer(maybe it'll ignore some features through setting the parameters)
* activations: The output values of a layer. In this case, the vector $\vec{a}$ (3 numbers) from the hidden layer is passed to the next layer.

* Output Layer: The final layer that produces the prediction or classification result.

* a neural network can have many hidden layers(multilayer perception) :

* ![image-20260506222534399](machine-learning.assets/image-20260506222534399.png)


## Forward prop in a single layer

![image-20260510184821869](machine-learning.assets/image-20260510184821869.png)



想象左边有 3 个输入神经元 ($x_1, x_2, x_3$)，右边有 2 个输出神经元 ($y_1, y_2$)：

- $y_1$ 的值取决于：$x_1w_{11} + x_2w_{12} + x_3w_{13} + b_1$
- $y_2$ 的值取决于：$x_1w_{21} + x_2w_{22} + x_3w_{23} + b_2$

PyTorch 的权重矩阵形状是 `(out_features, in_features)`。这意味着：**矩阵的每一行对应一个输出神经元**。

$$W = \begin{bmatrix} w_{11} & w_{12} & w_{13} \\ w_{21} & w_{22} & w_{23} \end{bmatrix} \leftarrow \text{这一行决定了 } y_1 \\ \leftarrow \text{这一行决定了 } y_2$$

- 如果你访问 `model.layer.weight[0]`，你得到的是所有连接到第一个输出神经元的权重。
- **计算公式**：$y = xW^T + b$ （对 $W$ 进行了转置，以便进行矩阵乘法）。

so $ W=[w_1  w_2]^T $,and $ w $ is vector whose number is the same as input features' dimension

## Training of neural network

![image-20260510183455039](machine-learning.assets/image-20260510183455039.png)

![image-20260510184333974](machine-learning.assets/image-20260510184333974.png)

1. create the model

   ```python
   model = nn.Sequential(
       nn.Linear(input_dim, 25), # 第一层：25个神经元
       nn.Sigmoid(),             #这一层的激活函数
       nn.Linear(25, 15),        # 第二层：15个神经元
       nn.Sigmoid(),
       nn.Linear(15, 1),         # 输出层：1个神经元
       nn.Sigmoid()
   )
   ```

2. loss and cost functions

   ```python
   # 2. 定义损失函数和优化器 (对应图片中的 ②)
   criterion = nn.BCELoss()      # Binary Cross Entropy
   optimizer = optim.Adam(model.parameters(), lr=0.01) # 常用 Adam 优化器
   ```

   * binary cross entropy is the loss function we use in logistic loss        $$L = - [y \log(\hat{y}) + (1 - y) \log(1 - \hat{y})]$$
   * usually used in binary classification data 
   * regression model 

3. gradient descent

   ```python
   # 3. 训练模型 (对应图片中的 ③ model.fit)
   # 假设 X 和 Y 已经是 torch.Tensor 格式
   epochs = 100
   for epoch in range(epochs):
       # A. 前向传播
       outputs = model(X)
       loss = criterion(outputs, Y)
       
       # B. 反向传播与优化
       optimizer.zero_grad() # 清空之前的梯度
       loss.backward()       # 计算梯度 (Backpropagation)
       optimizer.step()      # 更新参数 (Gradient Descent)
       
       if (epoch + 1) % 10 == 0:
           print(f'Epoch [{epoch+1}/{epochs}], Loss: {loss.item():.4f}')
   ```

compute derivatives for gradient descent using "back propagation"

## activation functions

* ReLU: $g(z)=max(0,z)$
* Linear activation function: $g(z)=z$  ==也可以说成没有用激活函数==
* Sigmoid: $\sigma(x) = \frac{1}{1 + e^{-x}}$ ==常用于二分类==

### choose activation function

for output layer, it depends on  $y $

![image-20260510193714386](machine-learning.assets/image-20260510193714386.png)

for hidden layer: most common choice is  ReLU

* higher computing speed
* flat just in the left
  * flat in a lot of places cause slow gradient descent

![image-20260510193813186](machine-learning.assets/image-20260510193813186.png)

### Why we need activation functions

Stacking multiple layers with linear activation functions always collapses into a single Linear Regression model.

简单来说，**线性变换的复合仍然是线性变换**。如果你不加非线性激活函数，无论你堆叠多少层，模型最终都能被简化为一个单层的线性变换。

if all hidden layer use linear activation function and output layer use sigmoid function, it becomes logistic regression model.

## Multiclass Classification

* multiclass classification problem:
  target $y$ can take on more than two possible values but not any number

![image-20260511213710792](machine-learning.assets/image-20260511213710792.png)

## softmax

![image-20260512123856795](machine-learning.assets/image-20260512123856795.png)

![image-20260512124229972](machine-learning.assets/image-20260512124229972.png) 

* 计算代价时只会计算y实际等于的那一项的cost，而不是每一项都计算 

![](machine-learning.assets/image-20260515220744517.png)

* note that each of these activation values depend on all of the values of $Z $ ,which is unique to the softmax activation function
* 其他激活函数都是不依赖于其他的 $z $ 的
* 

 

## Multi-label Classification 

![image-20260516163410686](machine-learning.assets/image-20260516163410686.png)

* $y$ is a vector



![image-20260516163606117](machine-learning.assets/image-20260516163606117.png)

we can use three neural networks

we can also use one neural networks with a 

* **Multi-class:** A sample belongs to **exactly one** category. The choices are mutually exclusive(互斥的).
  * 就是结果是从多个类里面选一个类出来
* **Multi-label:** A sample can belong to **multiple** categories at the same time (or none at all).
  * 结果是多个标签，输出是拥有每个标签的概率

## Advanced Optimization

REVIEW: gradient descent

![image-20260516164339644](machine-learning.assets/image-20260516164339644.png)

## Adam Algorithm Intuition

Adam: Adaptive Moment estimation

![image-20260516164547545](machine-learning.assets/image-20260516164547545.png)

* Adam can adapt the learning rate a bit automatically

## Additional layer types 

* dense layer:
* ![image-20260516165022321](machine-learning.assets/image-20260516165022321.png)

* convolutional layer:

  ![image-20260516165300036](machine-learning.assets/image-20260516165300036.png)

![image-20260516170140621](machine-learning.assets/image-20260516170140621.png)

* a neuron just look at part of $x$

## Model selection

![image-20260521233652609](machine-learning.assets/image-20260521233652609.png)

### 1. 数据的“双重间接训练”

在幻灯片展示的流程中，每个模型（从 $d=1$ 到 $d=10$）首先在**训练集**上训练，得到了各自的最佳参数（如 $w^{\langle 10 \rangle}, b^{\langle 10 \rangle}$）。

接着，流程做了一件致命的事：**用同一个测试集去评估这 10 个模型，并根据测试集上的错误率 $J_{\text{test}}$，挑选出了表现最好的那一个（比如图中选了 $d=5$）。**

这就意味着，虽然测试集没有直接参与修改 $w$ 和 $b$ 的梯度计算，但**你用它来做决策，挑选了超参数 $d$**。超级参数 $d=5$ 能够胜出，正是因为它“讨好”了这组特定的测试集数据。

### 2. 为什么说是“乐观的估计”？

因为这个被选出来的 $d=5$ 的模型，极有可能**刚好拟合了测试集中的特定噪声或随机特征**。

- **真实泛化误差**：模型在面对完全未知的全新数据（比如未来的真实流量、全新的样本）时的错误率。
- **现在的测试集误差 $J_{\text{test}}(w^{\langle 5 \rangle}, b^{\langle 5 \rangle})$**：因为 $d=5$ 是从 10 个候选人里专门挑出来的“最适应这个测试集”的冠军，它在这个测试集上的表现通常会**显著优于**它在其他全新未知数据上的表现。

### solution: validation set

![image-20260521234440311](machine-learning.assets/image-20260521234440311.png)

* validation can help you choose the degree $ d $,so every parameter is given by the data instead of your decision

* make decisions only looking at the training set and validation set
* do not use the test set at all to make decisions about your model
* only you've made all those decisions, then finally take the model you have designed and evaluated on your test set

##  Diagnosing bias and variance

![image-20260525190648362](machine-learning.assets/image-20260525190648362.png)

![image-20260525191219958](machine-learning.assets/image-20260525191219958.png)

* sometimes we may have high bias and high variance at the same time  部分过拟合部分欠拟合 

* with regularration

![image-20260525193516626](machine-learning.assets/image-20260525193516626.png)

![image-20260525193742681](machine-learning.assets/image-20260525193742681.png)

![image-20260525194042713](machine-learning.assets/image-20260525194042713.png)

![image-20260525195317415](machine-learning.assets/image-20260525195317415.png)

## learning curve

![image-20260525195832747](machine-learning.assets/image-20260525195832747.png)

* note that it becomes harder to fit the data when getting more train data

* flatten:平坦

![image-20260525200156144](machine-learning.assets/image-20260525200156144.png)

* it shows that increasing train data is not helpful for your model if your model have high bias

![image-20260525200700079](machine-learning.assets/image-20260525200700079.png)

* increasing data can help handle high variance
* because pf overfitting, $J_{train}$ may be lower than baseline, but it will get higher with the increasing of the train data

### Neural networks and bias variance

![image-20260525203946738](machine-learning.assets/image-20260525203946738.png)

* 更大的网络可以降低 bias，但会 slow down the training and inference process
* 只要适当正则化，使用一个更大的神经网络几乎不会有什么坏处，可能显著提高性能
* a large neutral network usually is a low bias machine, which fits very complicated functions very well.

## Iterative loop of Machine-learning development

![image-20260525211416215](machine-learning.assets/image-20260525211416215.png)

 1. Choose architecture (model, data, etc.)

This is the **starting point** or the next iteration phase. In this step, you make foundational decisions regarding your machine learning system:

- **Model Selection:** Deciding which algorithm or neural network architecture to use (e.g., choosing a linear model, a deep convolutional network, or a transformer).
- **Data Preparation:** Choosing how to collect, clean, structure, and feature-engineer your dataset.
- **Hyperparameters:** Setting initial configurations like learning rates, number of layers, or regularization terms.

### 2. Train model

Once the architecture and data are ready, you execute the **training phase**:

- The model feeds on the training dataset and adjusts its internal weights using an optimization algorithm (like Gradient Descent or Adam).
- The goal here is to let the model learn the patterns and minimize the training loss.

### 3. Diagnostics (bias, variance and error analysis)

After training, you evaluate how the model actually performed. This is the **diagnostic phase** where you perform a "medical checkup" on your model:

- **Bias Analysis:** Checking if the training error is too high (indicating the model is underfitting).
- **Variance Analysis:** Checking the gap between the training error and cross-validation error (indicating if the model is overfitting).
- **Error Analysis:** Manually inspecting the specific examples the model got wrong to understand *why* it made those mistakes.

### Why is it a Loop?

The output of the **Diagnostics** phase directly guides your next choice in the **Architecture** phase.

- If diagnostics show **High Bias**, you loop back to *Choose architecture* and make the model larger or add features.
- If diagnostics show **High Variance**, you loop back to *Choose architecture* to add regularization or collect more data.
- If error analysis shows the model struggles with a specific category of data, you loop back to modify the data pipeline.

By continuously running through this loop, the model's performance improves incrementally with each cycle.

### an example: rubbish email ckassifier

![image-20260525211618111](machine-learning.assets/image-20260525211618111.png)

**How to try to reduce your spam classifier's error?**

- Collect more data. E.g., "Honeypot" project.
- Develop sophisticated features based on email routing (from email header).
- Define sophisticated(复杂) features from email body. E.g., should "discounting" and "discount" be treated as the same word.
- Design algorithms to detect misspellings. E.g., w4tches, med1cine, m0rtgage.

### Error analysis

![image-20260527232615776](machine-learning.assets/image-20260527232615776.png)

* pay attention to those errors which have big impact

* collect more data or new features to help your model become better at recognizing this type of pharma spam（制药垃圾邮件）

![image-20260527233111731](machine-learning.assets/image-20260527233111731.png)
