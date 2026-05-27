# Machine Learning

## What is Machine Learning

- **Supervised learning** — used most
- **Unsupervised learning**

### Supervised Learning

Learn to map input (x) to output (y).

Learn from being given the "right answers".

- **Regression (回归)**: predict a number
  - Infinitely many possible outputs
- **Classification (分类)**: predict categories
  - Small number of possible outputs
  - Inputs can be more than one variable

### Unsupervised Learning

Data only comes with inputs x, but not output labels y.

- x is also called **feature**
  - 字面意思理解，可以理解为某个东西的特征，比如预测房价，x可以是size of house，也可以多维预测，加上the number of bedroom等
- y is also called **target**
- $\hat{y}$ means the predicted value (estimate of y)

The algorithm has to find structure in the data.

![Unsupervised learning clustering example](machine-learning.assets/image-20260428125917066.png)

- **Clustering (聚类)**

## Linear Regression Model

## Cost Function

![Cost function diagram](machine-learning.assets/image-20260428161732083.png)

- **Parameters**: variables you can adjust to improve the model
- Also called **coefficients** or **weights (权重)**

![Cost function formula](machine-learning.assets/image-20260428162302425.png)

- Divided by $2m$ to make derivative computation cleaner later on
- So it's important to find $w, b$ to minimize the cost function $J$

## Gradient Descent (梯度下降)

- Used widely — **very important**

Given some function $J(w, b)$, we want:

$$\min_{w, b} J(w, b)$$

![Gradient descent surface](machine-learning.assets/image-20260428165553135.png)

- Choose a starting point on the surface by choosing starting values for $w, b$
- Choose the direction that takes you downhill most quickly
- Different starting points may lead to different local minima (局部最小值)

### Gradient Descent Algorithm

$$w = w - \alpha \frac{\partial}{\partial w} J(w, b)$$

$$b = b - \alpha \frac{\partial}{\partial b} J(w, b)$$

- **$w$**: The **Weight/Parameter (参数/权重)** that the model is trying to learn
- **$\alpha$**: The **Learning Rate (学习率)**
  - Determines the **step size** during each iteration
- **$\frac{\partial}{\partial w} J(w, b)$**: The **Derivative** or **Gradient (导数/梯度)**
  - It represents the slope of the cost function at the current point (代表当前位置代价函数的斜率)
  - It tells the algorithm which direction to move in to reach the lowest point (它告诉算法为了到达最低点应该朝哪个方向移动)

![Gradient descent steps](machine-learning.assets/image-20260428171433306.png)

- Simultaneously update $w$ and $b$ on each iteration

### Learning Rate

![Learning rate too small](machine-learning.assets/image-20260428172637104.png)

![Learning rate too large](machine-learning.assets/image-20260428172919831.png)

- Note that if we use a convex function (凸函数), it will always converge to the global minimum (the only one minimum)

## "Batch" Gradient Descent

- **Batch**: Each step of gradient descent **uses all the training examples**
  - In this case, we use the cost function which uses all the training examples to compute error

![Batch gradient descent](machine-learning.assets/image-20260428175327787.png)

## Feature Scaling

![Feature scaling illustration](machine-learning.assets/image-20260429230146949.png)

![Contour comparison](machine-learning.assets/image-20260429230551268.png)

- Sometimes the range of one feature may be very large, so a small change of $w_1$ can make a big difference
- The contours (等高线) can be very tall and skinny, making gradient descent bounce back and forth
- If different features take on very different ranges of values, it can cause gradient descent to run slowly

### Mean Normalization

![Mean normalization formula](machine-learning.assets/image-20260429231730923.png)

Normalize feature values to a common range (typically around $-1$ to $1$ or $0$ to $1$):

![Mean normalization calculation](machine-learning.assets/image-20260429232130930.png)

- 如果不归一化，有些参数就会更快地收敛到最佳值，有些收敛非常慢，从表达式也看的出来，因为他们共用一个学习率但是梯度相差非常大
- 归一化之后训练速度会变得非常非常快！

  ![Scaling speeds up gradient descent](machine-learning.assets/image-20260502161309259.png)

## Cost Function Curve

To verify gradient descent is working, plot the cost $J$ vs. iterations:

![Cost function decreasing](machine-learning.assets/image-20260429234526107.png)

![Cost function increasing — bad](machine-learning.assets/image-20260429234845846.png)

- If cost sometimes increases, it usually means the learning rate is too large, or there's a bug in the code
- Can choose a very, very small $\alpha$ to see if the cost still decreases (used as a debugging strategy)

![Choosing learning rate](machine-learning.assets/image-20260429235231793.png)

## Feature Engineering

> Using intuition to design new features, by transforming or combining original features.

For $f = w_1x_1 + w_2x_2 + b$:

We can set $x_3 = x_1 x_2$

Then we get $f = w_1x_1 + w_2x_2 + w_3x_3 + b$

This may produce a better model than using the original features alone.

## Polynomial Regression (多项式回归)

- Feature scaling becomes **very important** here

![Polynomial regression examples](machine-learning.assets/image-20260502162645810.png)

# Classification

- Class = category
- **Binary classification**: y can only be one of two values

![Binary classification example](machine-learning.assets/image-20260502213900955.png)

## Logistic Regression

![Why not linear regression for classification](machine-learning.assets/image-20260504144757188.png)

The logistic regression model uses the **sigmoid function** to output a value between 0 and 1:

![Logistic regression model](machine-learning.assets/image-20260504144952803.png)

- The output represents the **probability** that y = 1 given input x
- If we set a threshold of 0.5, we get:

  ![Decision boundary at 0.5](machine-learning.assets/image-20260504145749808.png)

## Decision Boundary

## Cost Function for Logistic Regression

![Why squared error doesn't work](machine-learning.assets/image-20260504152633333.png)

- If we use the squared error cost for logistic regression, the cost function becomes non-convex, which means gradient descent can easily get stuck in a local minimum instead of the global minimum

![Non-convex vs convex](machine-learning.assets/image-20260504153139922.png)

The logistic loss function (also called **Binary Cross-Entropy**):

![Logistic loss function](machine-learning.assets/image-20260504153233456.png)

![Simplified logistic cost](machine-learning.assets/image-20260504153347484.png)

- A simpler way to write this formula as a single expression
- 这个模型是通过最大似然估计（Maximum Likelihood Estimation）推导的，基本所有分类任务都在用这个

# Overfitting (过拟合)

- **Bias (偏差)**
- **Underfit (欠拟合)**: also called **high bias** — does not fit the training set well
  - 可以这样理解，偏差就是"偏"，意思是没命中靶心，就是模型没有精确命中 training set 上的点
- **Generalization (泛化)**: make good predictions on new examples that the model has never seen before
- **Overfitting**: also called **high variance (高方差)** — fits the training set extremely well but cannot generalize well
  - 因为可能同一个训练集训练出来的函数很不一样，所以叫高方差
  - 方差反应波动程度，高方差意思是模型弯弯绕绕的，所以过拟合
  - 成本函数可能接近0但是效果很差

![Underfitting, good fit, overfitting](machine-learning.assets/image-20260505214639624.png)

So the aim of machine learning is to find a model which is neither underfitting nor overfitting.

## Addressing Overfitting

- Collect more training examples
- Use fewer features
  - All features + insufficient data → overfitting
  - A subset of these features may be just right
  - **Regularization (正则化)**: keep all features but reduce the magnitude of parameters
- Note that we can set a parameter to 0 to eliminate a feature entirely; if the parameter is made small enough, it can also work well without fully removing the feature

## Cost Function with Regularization

![Regularized cost function](machine-learning.assets/image-20260505231254900.png)

- $\lambda$ is a hyperparameter we must choose (like the learning rate $\alpha$)
  - If $\lambda$ is too small, the regularization term has little effect → the model will **overfit**
    - 因为后面的正则项几乎不会起作用
  - If $\lambda$ is enormous, all parameters are driven close to 0 → the model will **underfit**
    - 后面正则项非常大，导致各个参数接近于0，最后得到一个 $y = b$ 的直线
- This model will try to keep $w_j$ small
- 这个方法常常可以带来一个比较平滑、波动不大的拟合

![Gradient descent with regularization](machine-learning.assets/image-20260506001104853.png)

This derivation shows that:

What regularization is doing on every single iteration of gradient descent is multiplying $w$ by a number slightly less than 1, and that has the effect of shrinking the value of $w_j$ just a little bit.

## Regularized Logistic Regression

和线性回归的思路完全一样。The gradient descent update with regularization term looks identical to the linear regression case.

# Deep Learning

![Neural network overview](machine-learning.assets/image-20260506220047924.png)

- A **layer** is a grouping of neurons which take as input the same or similar features and that in turn output a few numbers together (a layer can have one or more neurons)
- **Input Layer**: The first layer of the network that receives raw data / features
- **Hidden Layer**: The layers between the input and output
  - They are called "hidden" because their values aren't seen in the final output
  - We don't need to manually decide what the features should be (such as affordability, awareness, etc.) — the network can figure out all the features it needs in the hidden layers on its own
  - Each neuron in a given layer has access to every feature from the previous layer (though it may ignore some features by setting the corresponding weights near zero)
- **Activations**: The output values of a layer. For example, the vector $\vec{a}$ (3 numbers) from the hidden layer is passed to the next layer as input.
- **Output Layer**: The final layer that produces the prediction or classification result
- A neural network can have many hidden layers (multilayer perceptron / deep network):

![Multilayer perceptron](machine-learning.assets/image-20260506222534399.png)

### Forward Propagation in a Single Layer

![Forward propagation](machine-learning.assets/image-20260510184821869.png)

想象左边有 3 个输入神经元 ($x_1, x_2, x_3$)，右边有 2 个输出神经元 ($y_1, y_2$)：

- $y_1$ 的值取决于：$x_1w_{11} + x_2w_{12} + x_3w_{13} + b_1$
- $y_2$ 的值取决于：$x_1w_{21} + x_2w_{22} + x_3w_{23} + b_2$

PyTorch 的权重矩阵形状是 `(out_features, in_features)`。这意味着：**矩阵的每一行对应一个输出神经元**。

$$W = \begin{bmatrix} w_{11} & w_{12} & w_{13} \\ w_{21} & w_{22} & w_{23} \end{bmatrix} \begin{aligned} &\leftarrow \text{这一行决定了 } y_1 \\ &\leftarrow \text{这一行决定了 } y_2 \end{aligned}$$

- 如果你访问 `model.layer.weight[0]`，你得到的是所有连接到第一个输出神经元的权重
- **计算公式**：$y = xW^T + b$ （对 $W$ 进行了转置，以便进行矩阵乘法）

So $W = [w_1 \quad w_2]^T$, and each $w$ is a vector whose length is the same as the input features' dimension.

### Training of a Neural Network

![Training overview](machine-learning.assets/image-20260510183455039.png)

![Training steps](machine-learning.assets/image-20260510184333974.png)

**1. Create the model**

```python
model = nn.Sequential(
    nn.Linear(input_dim, 25),  # First layer: 25 neurons
    nn.Sigmoid(),              # Activation function for this layer
    nn.Linear(25, 15),         # Second layer: 15 neurons
    nn.Sigmoid(),
    nn.Linear(15, 1),          # Output layer: 1 neuron
    nn.Sigmoid()
)
```

**2. Define loss and cost functions**

```python
# 2. Define loss function and optimizer (corresponds to ② in the diagram)
criterion = nn.BCELoss()      # Binary Cross Entropy
optimizer = optim.Adam(model.parameters(), lr=0.01)  # Commonly used Adam optimizer
```

- **Binary Cross Entropy** is the loss function used for logistic loss:

  $$L = - [y \log(\hat{y}) + (1 - y) \log(1 - \hat{y})]$$

- Usually used for binary classification problems

**3. Gradient descent (training loop)**

```python
# 3. Train the model (corresponds to ③ model.fit in the diagram)
# Assume X and Y are already torch.Tensor
epochs = 100
for epoch in range(epochs):
    # A. Forward propagation
    outputs = model(X)
    loss = criterion(outputs, Y)

    # B. Backpropagation and optimization
    optimizer.zero_grad()  # Clear previous gradients
    loss.backward()        # Compute gradients (Backpropagation)
    optimizer.step()       # Update parameters (Gradient Descent)

    if (epoch + 1) % 10 == 0:
        print(f'Epoch [{epoch+1}/{epochs}], Loss: {loss.item():.4f}')
```

Compute derivatives for gradient descent using **backpropagation**.

## Activation Functions

- **ReLU**: $g(z) = \max(0, z)$
- **Linear activation function**: $g(z) = z$ — 也可以说成没有用激活函数
- **Sigmoid**: $\sigma(x) = \frac{1}{1 + e^{-x}}$ — 常用于二分类

### Choosing an Activation Function

For the **output layer**, it depends on $y$:

![How to choose output activation](machine-learning.assets/image-20260510193714386.png)

For **hidden layers**: the most common choice is **ReLU**

- Faster to compute
- Flat only in the left half (z < 0)
  - Sigmoid/Tanh are flat in a lot of places, which causes slow gradient descent (the gradient is near zero, so learning stalls)

![ReLU vs Sigmoid comparison](machine-learning.assets/image-20260510193813186.png)

### Why We Need Activation Functions

Stacking multiple layers with linear activation functions always collapses into a single linear regression model.

简单来说，**线性变换的复合仍然是线性变换**。如果你不加非线性激活函数，无论你堆叠多少层，模型最终都能被简化为一个单层的线性变换。

If all hidden layers use a linear activation function and the output layer uses a sigmoid function, the entire network becomes equivalent to a logistic regression model.

## Multiclass Classification

- **Multiclass classification** problem:
  The target $y$ can take on more than two possible values (but not any arbitrary number — it's one of a fixed set of categories)

![Multiclass classification](machine-learning.assets/image-20260511213710792.png)

## Softmax

![Softmax from scratch](machine-learning.assets/image-20260512123856795.png)

![Softmax as output layer](machine-learning.assets/image-20260512124229972.png)

- 计算代价时只会计算 y 实际等于的那一项的 cost，而不是每一项都计算

![Softmax neural network](machine-learning.assets/image-20260515220744517.png)

- Note that each of these activation values $a_j$ depends on all of the values of $z$ (i.e., $z_1, z_2, \ldots, z_n$), which is unique to the softmax activation function
- 其他激活函数（如 sigmoid、ReLU）的输出都是只依赖于各自的 $z$ 值，与其他 $z$ 无关

## Multi-label Classification

![Multi-label vs multi-class](machine-learning.assets/image-20260516163410686.png)

- $y$ is a vector (each element indicates the presence or absence of a label)

![Multi-label approaches](machine-learning.assets/image-20260516163606117.png)

We can use three separate neural networks (one per label), or we can use a single neural network with multiple output neurons (each with a sigmoid activation).

- **Multi-class**: A sample belongs to **exactly one** category. The choices are mutually exclusive (互斥的).
  - 就是结果是从多个类里面选一个类出来
- **Multi-label**: A sample can belong to **multiple** categories at the same time (or none at all).
  - 结果是多个标签，输出是拥有每个标签的概率

## Advanced Optimization

Review: gradient descent

![Gradient descent review](machine-learning.assets/image-20260516164339644.png)

### Adam Algorithm Intuition

Adam: **Adaptive Moment Estimation**

![Adam intuition](machine-learning.assets/image-20260516164547545.png)

- Adam can adapt the learning rate automatically — if a parameter needs a larger step, the effective learning rate increases; if it needs a smaller step, the effective learning rate decreases
- Like gradient descent but each parameter gets its own custom learning rate

## Additional Layer Types

- **Dense layer** (全连接层): each neuron receives input from every neuron in the previous layer

  ![Dense layer](machine-learning.assets/image-20260516165022321.png)

- **Convolutional layer** (卷积层): each neuron only looks at a small region of the input

  ![Convolutional layer](machine-learning.assets/image-20260516165300036.png)

![Convolutional layer detail](machine-learning.assets/image-20260516170140621.png)

- A neuron in a convolutional layer only looks at a local patch of the input $x$ — not the entire input

## Model Selection

![Model selection problem](machine-learning.assets/image-20260521233652609.png)

### 1. 数据的"双重间接训练"

在幻灯片展示的流程中，每个模型（从 $d=1$ 到 $d=10$）首先在**训练集**上训练，得到了各自的最佳参数（如 $w^{\langle 10 \rangle}, b^{\langle 10 \rangle}$）。

接着，流程做了一件致命的事：**用同一个测试集去评估这 10 个模型，并根据测试集上的错误率 $J_{\text{test}}$，挑选出了表现最好的那一个（比如图中选了 $d=5$）。**

这就意味着，虽然测试集没有直接参与修改 $w$ 和 $b$ 的梯度计算，但**你用它来做决策，挑选了超参数 $d$**。超级参数 $d=5$ 能够胜出，正是因为它"讨好"了这组特定的测试集数据。

### 2. 为什么说是"乐观的估计"？

因为这个被选出来的 $d=5$ 的模型，极有可能**刚好拟合了测试集中的特定噪声或随机特征**。

- **真实泛化误差**：模型在面对完全未知的全新数据（比如未来的真实流量、全新的样本）时的错误率。
- **现在的测试集误差 $J_{\text{test}}(w^{\langle 5 \rangle}, b^{\langle 5 \rangle})$**：因为 $d=5$ 是从 10 个候选人里专门挑出来的"最适应这个测试集"的冠军，它在这个测试集上的表现通常会**显著优于**它在其他全新未知数据上的表现。

### Solution: Validation Set

![Train/validation/test split](machine-learning.assets/image-20260521234440311.png)

- The validation set can help you choose the degree $d$, so every hyperparameter is guided by the data instead of your personal decision
- Make decisions only looking at the training set and validation set
- Do not use the test set at all to make decisions about your model
- Only once you've made all those decisions, then finally take the model you have designed and evaluate it on your test set

## Diagnosing Bias and Variance

![Bias and variance](machine-learning.assets/image-20260525190648362.png)

![High bias, high variance, both](machine-learning.assets/image-20260525191219958.png)

- Sometimes we may have high bias and high variance at the same time — 部分区域欠拟合，部分区域过拟合

### With Regularization

![Effect of lambda on decision boundary](machine-learning.assets/image-20260525193516626.png)

![J_train vs J_cv across lambda values](machine-learning.assets/image-20260525193742681.png)

![Choosing lambda](machine-learning.assets/image-20260525194042713.png)

![Bias/variance vs lambda summary](machine-learning.assets/image-20260525195317415.png)

## Learning Curves

![High bias learning curve](machine-learning.assets/image-20260525195832747.png)

- Note that it becomes harder to fit the data perfectly when you have more training examples (J_train rises)
- **Flatten (平坦)**: The curves plateau

![High bias — more data doesn't help](machine-learning.assets/image-20260525200156144.png)

- If your model has high bias, adding more training data will **not** significantly improve performance — J_cv and J_train will both flatten out at a high error level

![High variance learning curve](machine-learning.assets/image-20260525200700079.png)

- Increasing the amount of training data **can** help handle high variance (overfitting)
- Because of overfitting, $J_{train}$ may start lower than the baseline, but it will increase as training data grows — while $J_{cv}$ decreases

### Neural Networks and Bias/Variance

![Large vs small networks](machine-learning.assets/image-20260525203946738.png)

- A larger network can reduce bias (it's a more powerful function approximator), but it also slows down training and inference
- 只要适当正则化，使用一个更大的神经网络几乎不会有什么坏处，可能显著提高性能
- A large neural network is usually a **low bias machine**, which can fit very complicated functions very well

## Iterative Loop of Machine Learning Development

![The ML development loop](machine-learning.assets/image-20260525211416215.png)

### 1. Choose Architecture (model, data, etc.)

This is the **starting point** of each iteration. In this step, you make foundational decisions regarding your machine learning system:

- **Model Selection:** Deciding which algorithm or neural network architecture to use (e.g., choosing a linear model, a deep convolutional network, or a transformer).
- **Data Preparation:** Choosing how to collect, clean, structure, and feature-engineer your dataset.
- **Hyperparameters:** Setting initial configurations like learning rates, number of layers, or regularization terms.

### 2. Train Model

Once the architecture and data are ready, you execute the **training phase**:

- The model feeds on the training dataset and adjusts its internal weights using an optimization algorithm (like Gradient Descent or Adam).
- The goal here is to let the model learn the patterns and minimize the training loss.

### 3. Diagnostics (Bias, Variance, and Error Analysis)

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

### Example: Spam Email Classifier

![Spam classifier development](machine-learning.assets/image-20260525211618111.png)

**How to try to reduce your spam classifier's error?**

- Collect more data — e.g., "Honeypot" project.
- Develop sophisticated features based on email routing (from email header).
- Define sophisticated (复杂的) features from the email body — e.g., should "discounting" and "discount" be treated as the same word?
- Design algorithms to detect misspellings — e.g., w4tches, med1cine, m0rtgage.

### Error Analysis

![Error analysis](machine-learning.assets/image-20260527232615776.png)

- Pay attention to those errors which have the biggest impact
- Collect more data or design new features to help your model become better at recognizing specific types of mistakes (e.g., pharma spam 制药垃圾邮件)

![Iterating based on error analysis](machine-learning.assets/image-20260527233111731.png)
