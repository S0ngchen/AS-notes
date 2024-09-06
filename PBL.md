# 大气边界层

## 什么是大气边界层
我们生活在大气中，大气的一切运动都和我们息息相关。虽然这么说，但其实相比千米高空发生的事情，我们更想知道我们所生活的范围有什么样的天气。我们生活的地方，最贴近地面的大气，被称为**大气边界层**，或者**行星边界层 (PBL)**。意思是大气的边界地带。在边界层中，由于大气与地表直接接触，会发生一系列有趣的事情：地面摩擦造成的大气动量的剧烈耗散、地面对大气的加热作用、植被湖泊向大气释放水汽……同时他也是我们直接生活的地方。这无不让我们关注这一特殊区域。

### 边界层高度与划分
我们现在知道边界层如此重要，需要我们研究。但是，边界层的范围是怎么规定的呢？我们先引入流体力学对于边界层的定义：

流体在边界上方流动过程中，边界表面的摩擦力使流体速度在垂直边界上发生切变，造成流体低能部分积累。这一流速减少的部分就是流体边界层。

听起来似乎有点绕，但实际上可以由这张图很明确的解释

![来源：https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Laminar_boundary_layer_scheme.svg/2560px-Laminar_boundary_layer_scheme.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Laminar_boundary_layer_scheme.svg/2560px-Laminar_boundary_layer_scheme.svg.png)

在图中流体速度在一定高度之内，会低于最上层的流体，因为上层的流体收到的边界摩擦作用弱，而下层强。这一速度低的区域就是边界层。

由此类推，在大气科学中，行星边界层就可以被简单定义为：大气受到下垫面摩擦影响的薄层。而更严谨的定义如下：
`大气边界层位于对流层底部，由于直接与地面相贴而受到分子粘性，湍流摩擦，辐射增热，水汽交换，物质扩散各种交换作用和地形的影响，致使湍流应力成为一个重要的因子而不可忽略，与之相联系形成大气边界层`

虽然说人类大部分时间生活在地表不超过100米的地方，这一地方称为边界层，但不代表边界层只有一百米高。根据气象观测，受到不同地区气象条件的差异，边界层的高度在几百米到几千米不等，可以简单的估计为1500m，也就是大约850hPa的高度。

结合大气科学对大气气层的划分，包含了边界层的大气由低到高可以被细致的划分为以下几层：

![来源：https://bkimg.cdn.bcebos.com/pic/0df431adcbef76093a8facc02ddda3cc7dd99eec?x-bce-process=image/format,f_auto/quality,Q_70/resize,m_lfit,limit_1,w_536](https://bkimg.cdn.bcebos.com/pic/0df431adcbef76093a8facc02ddda3cc7dd99eec?x-bce-process=image/format,f_auto/quality,Q_70/resize,m_lfit,limit_1,w_536)

1. 贴地层：这一层的厚度大约2m，是大气最低的一层。在这层中，分子粘性力主导运动，湍流粘性力小。
2. 近地面层：这一层的厚度大约100m。这层分子粘性力的影响随高度迅速减弱，湍流粘性力的影响相对增强。由于这层中的各个物理量（动量、水汽等）的垂直输送基本不随高度变化，又被称为**常值通量层**。
3. 上部摩擦层：再往上，湍流粘性力的影响被科氏力反超，呈现湍流粘性力、科氏力与气压梯度力三力平衡的形式。由于Ekman对本层的重要贡献，这层又称Ekman层。
4. 自由大气：这一层属于对流层除去行星边界层剩下的的部分。其中的湍流粘性力可以忽略，因此被称为自由大气。
5. 平流层
6. 热层
……

接下来，我们将对边界层中的几个分层展开介绍。但是，由于其中的解释需要涉及一些后续的知识，但为了保证信息的连续性，我把这些部分放在此处。如果你是一位初学者，更推荐先了解[湍流](#湍流)再回头看这一部分。
#### 贴地层

#### 近地面层

#### 上部摩擦层

### 湍流
为了描述边界层中大气的运动，我们需要知道一些用于解析边界层的物理概念与方法。

先看一组真实世界中的气温-时间序列：

![图是偷的（小声）](./fig4pbl/image.png)

如果不看红线，只会感觉密密麻麻的，似乎没什么特别。但是加上这条红线，就可以看出点端倪：我们测得的物理量都在这个红线附近波动，而红线本身又呈现波的形状。

也就是说，真实世界中，流体的流动形式有以下三种：
平均运动 $\bar A$，波动 $A'$和湍流运动$A''$ 。也就是说，任何一个变量都能写成 $A=\bar A+A'+A''$ ！换种方法说，流体运动是平均运动、波动和湍流三者的叠加。

这和[动力气象学中的波动]()类似，只不过动力气象学中研究的是自由大气，所以可以忽略湍流的作用。

但是，我们讲了半天，到底什么是**湍流 (turbulence)**呢？

#### 什么是湍流

一般提起流体，我们很容易想到水流，比如水喉流出的水。一般来说，如果流量很小的话，水流呈现出比较稳定的结构

![稳定的水流结构，来源https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTALwOdtEXqTT-W4S_QBdB1o31TJYDAN9EHMg&s](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTALwOdtEXqTT-W4S_QBdB1o31TJYDAN9EHMg&s)

在这些情况下，流体质点彼此互不混杂，质点运动轨迹呈平滑直线的流动。我们称这样的运动为**层流 (laminar)**。

但是，如果一下把出水量跳到最大，那么水流就不再是像图上这样流动了，而是喷涌而出。

![喷涌的水流结构，https://preview.qiantucdn.com/58pic/20240509/00358PICeMHIX58PIC58PICbW008c_PIC2018_PIC2018.jpg!qt_h320](https://preview.qiantucdn.com/58pic/20240509/00358PICeMHIX58PIC58PICbW008c_PIC2018_PIC2018.jpg!qt_h320)

这种喷涌而出的水流就被称为**湍流 (turbulence)**。

但是说来惭愧，目前湍流仍然没有一个准确的定义，只有以下几种主流的定性描述：
1. Von.Karman和I.G Taylor对湍流的定义：湍流是流体和气体中出现的一种无规则流动现象。
2. Hinze对湍流的定义为：只提不规则运动不全面，“湍流的各个量在时间和空间上表现出随机性。
3. 周培源：湍流为一种不规则的涡旋(eddy)运动。

为了规范，我们不妨采取Hinze与Taylor说法的叠加：湍流是流体和气体中出现的一种无规则流动现象，并且湍流的各个量在时间和空间上表现出随机性。也就是说，我们看到水枪喷射出来，飞溅的水、工厂排出乱飘的烟都是湍流。

![湍流，来源：https://upload.wikimedia.org/wikipedia/commons/b/b9/False_color_image_of_the_far_field_of_a_submerged_turbulent_jet.jpg](https://upload.wikimedia.org/wikipedia/commons/b/b9/False_color_image_of_the_far_field_of_a_submerged_turbulent_jet.jpg)

综上，湍流与层流的区别如图所示

![图源：https://bkimg.cdn.bcebos.com/pic/0d338744ebf81a4ca55b972edd2a6059242da6e8?x-bce-process=image/format,f_auto/watermark,image_d2F0ZXIvYmFpa2UyNzI,g_7,xp_5,yp_5,P_20/resize,m_lfit,limit_1,h_1080](https://bkimg.cdn.bcebos.com/pic/0d338744ebf81a4ca55b972edd2a6059242da6e8?x-bce-process=image/format,f_auto/watermark,image_d2F0ZXIvYmFpa2UyNzI,g_7,xp_5,yp_5,P_20/resize,m_lfit,limit_1,h_1080)

#### 湍流的产生机制
雷诺（Reynold）在1883年做了一个[实验](https://www.youtube.com/watch?v=y0WRJtXvpSo)（不能播放的话可以看看这个[比较长的版本](https://www.bilibili.com/video/BV14U4y1f7K7)）验证湍流的产生机制。

他发现流体呈现湍流还是层流运动主要取决于：
1. 流体流速
2. 管子直径
3. 液体性质

根据这个性质，他得出了雷诺数（Reynolds number）：

$$
\text{Re}=\frac{\rho U L}{\mu}=\frac{U L}{\nu}
$$

其中 $\nu=\frac{\mu}{\rho}$ ，表示运动粘度。
关于这个式子具体的介绍，我会放在[动力学基础]()中（如果我想得起来更的话XD）

通过计算雷诺数，我们可以得到湍流的运动类型式层流还是湍流。当雷诺数大于临界雷诺数 $Re_c$ 时，流体从层流转变。

不过，雷诺数只是一个用于鉴别流体运动类型的工具，不能反映湍流的产生机制。一般来说，在大气中，湍流主要有两个产生机制：对流热泡和速度梯度。

##### 对流热泡
根据之前对于湍流的示意图，湍流的组织形式可以看作一个个小的涡旋 (专业称呼为湍涡，eddy)。你可以利用湍涡对湍流加深理解：**湍流可以看成叠加上许多湍涡的平流运动流体**。

当地面受到太阳辐射加热后，某些受到辐射量比较大的地面温度就会高于周围。热量传导到大气中，就产生了局地的高温热泡。如图所示

![如图所示红色就是热泡，来源http://pic3.zhimg.com/70/418ab4820aadaeb58d6cdbe71a700382_b.jpg](http://pic3.zhimg.com/70/418ab4820aadaeb58d6cdbe71a700382_b.jpg)

当热泡上升脱离地面后（详细的描述可以参考[这篇文章的 “2、成因” 部分](https://daily.zhihu.com/story/8113698)），会因为失去能量源而破碎。破碎的热泡就像浴缸中的泡泡一样变成更小的泡泡，这些小泡泡就是湍涡。

#### 剪切作用
第二种情况是风的剪切作用。当风吹过地表，受到地表的阻曳作用，靠近地表的风速会小于远离地表的风速。

![来源：https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Laminar_boundary_layer_scheme.svg/2560px-Laminar_boundary_layer_scheme.svg.png](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0e/Laminar_boundary_layer_scheme.svg/2560px-Laminar_boundary_layer_scheme.svg.png)

这种风的垂直切变会让气团旋转，产生涡旋。比如图中右边这个风速切变就会产生顺时针的涡旋。这些涡旋也会破碎产生小的湍涡。

#### 湍流的研究方法
现在我们知道了湍流的产生机制，接下来就要开始正式研究湍流了。

##### 泰勒假设
首先，我们应该获取湍流的资料。但是，由于流体在无时无刻的运动，湍涡也在不停的生消发展，我们该怎么测量一个无时无刻在变化的量呢？在1938年，泰勒（I.G Tylor）提出：**在特定条件下，湍流平移经过传感器时，可以将它看成凝固的。** 即，如果 $\frac{d\xi}{dt} = 0$ ，则有

$$
\frac{d\xi}{dt} = \frac{\partial \xi}{\partial t} + U \frac{\partial \xi}{\partial x} + V \frac{\partial \xi}{\partial y} + W \frac{\partial \xi}{\partial z}
$$

也就是

$$
\frac{\partial \xi}{\partial t} = - U \frac{\partial \xi}{\partial x} - V \frac{\partial \xi}{\partial y} - W \frac{\partial \xi}{\partial z}
$$

这样，区域内物理量随时间的变化就可以通过泰勒假设间接地通过排除时间变量求得。而根据 $\frac{d\xi}{dt} = 0$ ，可知其适用于湍强不太大、风速不太小、均匀湍流、平稳湍流的地区。也就是说，这个方法只能用于获取稳态流动中的湍流信息。

##### 雷诺平均
现在我们算是解决了资料的问题了。接下来，我们需要做另一件事：解方程。

我们知道，大气科学，乃至流体力学，都在试图解决一个核心的问题：Navier-Stokes方程（NS方程）

$$
\rho \left( \frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u} \cdot \nabla)\mathbf{u} \right) = -\nabla p + \mu \nabla^2 \mathbf{u} + \mathbf{f}
$$ 

或者写成大气科学领域更为熟悉的方式

$$
\frac{d\vec{V}_h}{dt} = -f \vec{k} \times \vec{V} - \frac{1}{\rho} \nabla P
$$

但是，众所周知，这是一个极其难以求解的，高度非线性的方程，我们必须使用一些技巧来辅助我们求解。在计算流体力学（Computational Fluid Dynamics, CFD）中有两个常用的方法：雷诺平均方法（Reynolds-Averaged Navier-Stokes, RANS）和大涡模拟方法（Large Eddy Simulation, LES）。我们先介绍更为常见RANS方法，如果后续有需要的话，我再更新[LES方法]()。

虽然湍流运动是随机且复杂的，但对于雷诺平均方法，我们可以采用统计的思想从计算瞬时态的流场转为计算均态的流场来曲线救国。像分析波动一样，雷诺平均的思想是将流体中的物理量表示为代表流体变化趋势的**均值**与代表湍流脉动的**扰动**，即对于任意物理量，均有 $A=\bar A+A'$。其中 $\bar A=\frac{1}{T}\int_0^T Adt$。如果我们取一个合适的时间，比如大于脉动周期，而小于流体的特征时间尺度。这样，由于时间大于脉动周期，可以去除随机性产生的影响；小于特征尺度可以防止流体的主要信息被一并消去。

然后，我们再对平均化做出如下规则约束：
1. $\overline{\bar A}=\bar A$， $\overline{A'}=0$,  $\overline{A'B'}\neq0$
2. $\overline{\bar A+A'}=\bar A+0=\bar A$
3. $\overline{(\bar A+A')\cdot(\bar B+B')}=\overline{\bar AB'+\bar A\bar B+A'\bar B+A'B'}=\overline{\bar A\bar B}+\overline{A'}=0$

同时，为了表达式简洁，我们再引入该死的[张量标识法]()（会填的），则可以得到雷诺平均后的方程，即（雷诺平均NS方程，Reynolds-Averaged Navier-Stokes, RANS）


#### 湍流的发展

#### 湍流的性质

### 边界层的特点
有了前面对边界层分层的划分，现在
#### 1. 日变化
