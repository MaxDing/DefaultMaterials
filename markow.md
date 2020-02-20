

## Markov Logic Network

####  Markov property

- 无记忆性，下一状态的概率分布今取决于当前状态（未来只和现在相关，和过去无关），即

$$
p(x_{n+1}=s_{n+1}|x_{n}=s_{n},x_{n-1}=s_{n-1},...,x_1=s_1) = p(x_{n+1}=s_{n+1}|x_{n}=s_{n})
$$

​    

- 明天的天气，下一时刻车站人数
- 不严谨，但计算高效



#### Markov Chain

- 定义

  - 一组随机变量 $X = \{X_1,X_2,...X_n\}$，每个随机变量的取值都在可数集内$X_i=s_i，s_i \in S$,如果随机变量的条件概率满足马尔可夫性质
    $$
    p(x_{n+1}=s_{n+1}|x_{n}=s_{n},x_{n-1}=s_{n-1},...,x_1=s_1) = p(x_{n+1}=s_{n+1}|x_{n}=s_{n})
    $$
    则$ X$成为马尔可夫链，可数集$S$称为状态空间。	

#### Markov Network

- 定义

  - 马尔可夫网是用来刻画一组随机变量 $X = \{X_1,X_2,...X_n\}$联合分布的模型，它由一个无向图$G$和一组势函数组成。
    - 每个随机变量对应$G$上的一个节点
    - $G$上的每个团都有一个势函数，势函数是从团的状态集到正实数集的映射

- 联合概率分布
  $$
  P(X=x) = \frac{1}{Z}\prod_k \phi_k(x_{\{k\}})
  $$
  其中$\phi_k$就是势函数，$x_{\{k\}}$表示第k个团的状态（就是团中每个节点（随机变量）的取值），Z是归一化常数，$Z=\sum_{x}\prod_k\phi_k(x_{\{k\}})$,表示所有状态的下的团势能乘积和

  - 对数形式
    $$
    P(X=x) = \frac{1}{Z}exp(\sum_j\omega_if_i(x))
    $$
    其中 $\omega_i为第i个团的权重，f_i是团特征函数$

- 马尔可夫性质

  - 从联合概率分布公式可以看出，某个点的概率分布只和它的相邻节点相关，即只和包含它的团的状态相关。因为这个点相邻节点的取值会影响到包含它的团的特征函数的取值。

#### Markov Logic Network

- 一阶逻辑

![1578024543544](C:\Users\DRJ\AppData\Roaming\Typora\typora-user-images\1578024543544.png)

![1578024561994](C:\Users\DRJ\AppData\Roaming\Typora\typora-user-images\1578024561994.png)

ground term:闭项，基本项，不包含变量的项   $f(t_1,t_2)$

ground atom:闭原子，谓词参数是闭项的原子  $R(f_1(t_1),f_2(t_1,t_2))$

ground formula:闭公式，原子是闭原子的公式 $R_1(f_1(t_1),f_2(t_1,t_2)) \land R_2(f_1(t_1),f_2(t_1,t_2))$



- 马尔可夫逻辑网

  ![1578025855246](C:\Users\DRJ\AppData\Roaming\Typora\typora-user-images\1578025855246.png)

  - 这里规则的权重$w$表示满足规则世界和不满足规则世界的差异性，$\omega$越大，差异越大。

    - 比如 $A \rightarrow B$, 满足该规则的世界有{(T,T),(F,T),(F,F)}, 不满足的世界有{(T,F)}, $\omega$越大，表示取到满足世界的可能性越大，不满足的可能性越小（但不代表不可能）。
      - 当然，如果$\omega \rightarrow \infty$,则不满足世界的可能性为0，表示不可能发生。和强逻辑是等价的

  - **马尔可夫逻辑网其实就是生成马尔可夫网的模板**

  - 马尔可夫逻辑网结合常量集合C生产的马尔可夫网结构：

    - 任意闭原子对应一个节点
    - 当两个节点表示的闭原子出现在同一规则中，则他们之间有条边
      - 因此出现在同一闭规则的闭原子节点构成一个团，团的权重就是规则的权重

  - 举例

    ![1578026732404](C:\Users\DRJ\AppData\Roaming\Typora\typora-user-images\1578026732404.png)

    给定常量集合C={A,B}，则马尔可夫网$M_{L,C}$。可以看出，网络大小和参数最多谓词的参数数量，常量集大小呈指数相关，会非常大。

    ![1578026999048](C:\Users\DRJ\AppData\Roaming\Typora\typora-user-images\1578026999048.png)

  - 联合概率分布

    ![1578027190012](C:\Users\DRJ\AppData\Roaming\Typora\typora-user-images\1578027190012.png)

    其中$\omega_i $表示规则(公式)$F_i$的权重，$n_i(x)$表示公式$F_i$在状态$x$下，为真的闭公式的个数

**举例说明和一阶逻辑的关系**

L = {($\forall x R(x) \rightarrow S(x)$,$\omega$ )}, C={A}.







#### 权重学习

类似于线性回归中的梯度下降算法（$y = wx + b$学习$(w,b)$）



x为试验样本

![1578030168318](C:\Users\DRJ\AppData\Roaming\Typora\typora-user-images\1578030168318.png) 



#### 推理

- 最大可能性问题

  ![1578030257961](C:\Users\DRJ\AppData\Roaming\Typora\typora-user-images\1578030257961.png)

- 条件概率

![1578030292746](C:\Users\DRJ\AppData\Roaming\Typora\typora-user-images\1578030292746.png)

