# 目录
- [目录](#目录)
- [雷诺平均](#雷诺平均)
  - [动量方程](#动量方程)
  - [水汽方程](#水汽方程)
  - [状态方程](#状态方程)
  - [连续方程](#连续方程)
  - [热流量方程](#热流量方程)
  - [动量脉动方程的简化](#动量脉动方程的简化)
  - [湍流动能方程](#湍流动能方程)
    - [不可压湍流动能方程的简化](#不可压湍流动能方程的简化)
      - [耗散项的简化](#耗散项的简化)
      - [气压扰动项的简化](#气压扰动项的简化)
      - [科氏力项的简化](#科氏力项的简化)
      - [湍流动能输送项的简化](#湍流动能输送项的简化)
    - [简化后的湍流方差方程](#简化后的湍流方差方程)
    - [湍流动能方程的物理意义](#湍流动能方程的物理意义)
      - [湍流动能随时间变化项](#湍流动能随时间变化项)
      - [平流项](#平流项)
      - [浮力项](#浮力项)
      - [切变项](#切变项)
      - [湍流输送项](#湍流输送项)
      - [气压脉动项](#气压脉动项)
      - [耗散项](#耗散项)

# 雷诺平均
虽然湍流运动是随机且复杂的，但我们可以采用统计的思想从计算瞬时态的流场转为计算均态的流场来曲线救国。雷诺平均（reynolds averaging）就是一种利用对物理量求时间平均来简化方程的方法。雷诺平均的特殊之处在于其并非直接对物理量进行平均，而是先进行了一个步骤：雷诺分解（reynolds decomposition）。像分析波动一样，雷诺分解的思想是将流体中的物理量表示为代表流体变化趋势空间分布的**均值**与代表湍流脉动时间分布的**扰动**，即对于任意物理量，均有 $A(x, t)=\bar A(x)+A'(x, t)$。其中 $\bar A=\frac{1}{T}\int_0^T A(x, t)dt$。

在这个分解中，物理量分解出来的平均量代表着在某个小的瞬间，这个系统的运行情况。比如使用高速摄像机对流场进行拍摄，通过这个手段获得的流体速度就是 $\bar u$ 。同时，在拍摄过程中，相机获取的是快门曝光时间的流体总的运动情况，也就相当于时间平均了。也就是说，平均流并不能完全反映实际的流场。比如说如果扰动的变化时间要小于高速摄像机的快门速度，那我们就完全无法捕捉扰动的变化。这就是扰动项的作用，它相当于补齐了是某个瞬间的变化量，帮助我们更好的还原流体实际的运行。

因此，我们对于雷诺平均时的时间步的选取就十分重要了。一般我们选取大于脉动周期，而小于流体的特征时间尺度。这样，由于时间大于扰动脉动周期，可以去除湍流随机性产生的影响；小于特征尺度则可以防止流体的主要变化信息被一并消去。

然后，我们再对平均化做出如下规则约束：
1. $\overline{\bar A}=\bar A$， $\overline{A'}=0$,  $\overline{A'B'}\neq0$
2. $\overline{\bar AB}=\bar A\bar B$ 但 $\overline{AB}\neq\bar A\bar B$
3. $\overline{\bar A+A'}=\bar A+0=\bar A$
4. $\overline{(\bar A+A')\cdot(\bar B+B')}=\overline{\bar AB'+\bar A\bar B+A'\bar B+A'B'}=\overline{\bar A\bar B}+\overline{A'B'}=0$
5. $\overline{(\frac{\partial A}{\partial B})}=\frac{\partial\bar A}{\partial B}$


整个过程可以总结为：只保留纯的平均量或者扰动的二次项（因为扰动的平均是0，而扰动乘上扰动的平均却不一定为0，比如 $\lim_{x\rightarrow0}x\sin(\frac{1}{x})$ ）。

同时，为了表达式简洁，我们再引入该死的[张量标识法](./basis.markdown#张量表示法)。

首先，在用张量表示的各个控制方程如下：

1. 动量方程： $\frac{\partial u_i}{\partial t}+u_j\frac{\partial u_i}{\partial x_j}=-\frac1\rho\frac{\partial p}{\partial x_i}+\epsilon_{i3}g+f\epsilon_{ij3}u_j+\nu\frac{\partial^2 u_i}{{\partial x_j}^2}$
2. 水汽方程： $\frac{\partial q}{\partial t} + u_j \frac{\partial q}{\partial x_i} = \nu_q \frac{\partial^2 q}{\partial x_i^2} + \frac{S_q}{\rho} + \frac{E}{\rho}$
3. 状态方程： $p=\rho RT$
4. 热流量方程： $\frac{\partial\theta}{\partial t}+u_j\frac{\partial\theta}{\partial x_j}=\nu_\theta\frac{\partial^2\theta}{{\partial x_j}^2}-\frac{1}{\rho C_p} \frac{\partial Q_j^*}{\partial x_j} - \frac{L_v E}{\rho C_p}$
5. 不可压近似下的连续方程： $\frac{u_j}{x_j}=0$

每项的物理意义与推导详见[大气运动的基本方程](./equations.md)。接下来，我们将对每个基本方程计算雷诺平均。

## 动量方程
对于

$$
\frac{\partial u_i}{\partial t}+u_j\frac{\partial u_i}{\partial x_j}=-\frac1\rho\frac{\partial p}{\partial x_i}+\epsilon_{i3}g+f\epsilon_{ij3}u_j+\nu\frac{\partial^2 u_i}{{\partial x_j}^2}
$$

将速度和压力进行雷诺分解： $u_i = \overline{u_i} + u_i', \quad p = \overline{p} + p'$ 。（由于密度的扰动相对自身不大，所以这里不分解密度项。），然后代入原方程，得到：

$$
\frac{\partial (\overline{u_i} + u_i')}{\partial t} + (\overline{u_j} + u_j') \frac{\partial (\overline{u_i} + u_i')}{\partial x_j} = -\frac{1}{\rho} \frac{\partial (\overline{p} + p')}{\partial x_i} + \epsilon_{i3} g + f \epsilon_{ij3} (\overline{u_j} + u_j') + \nu \frac{\partial^2 (\overline{u_i} + u_i')}{\partial x_j^2}
$$

求时间平均，得到

$$
\frac{\partial \overline{u_i}}{\partial t} + \overline{u_j} \frac{\partial \overline{u_i}}{\partial x_j} = -\frac{1}{\rho} \frac{\partial \overline{p}}{\partial x_i} + \epsilon_{i3} g + f \epsilon_{ij3} \overline{u_j} + \nu \frac{\partial^2 \overline{u_i}}{\partial x_j^2} - \frac{\partial \overline{u_i' u_j'}}{\partial x_j}
$$

上式便是RANS的动量方程。可以发现，这个方程与最初的方程有很大的相似之处：在把原方程所有的速度和气压取了平均然后多出了一项 

使用还没求平均的动量方程与RANS动量方程相减，可以得到扰动方程 $\frac{\partial \overline{u_i' u_j'}}{\partial x_j}$ 。这种形如 $\overline{u'_1u_2'}$ 的表达称为**雷诺应力**， $\frac{\partial \overline{u_i' u_j'}}{\partial x_j}$ 项也被称为雷诺应力项，表示由于速度扰动引起的动量传输，也就是**湍流粘性应力**。我们可以说雷诺应力 $\frac{\partial \overline{u_i' u_j'}}{\partial x_j}$ （其中i, j是确切的量）是通过 $u_i$ 方向的面向 $u_j$ 方向传输的脉动动量。接下来我将向你证明为什么可以这么说。首先借用一下别人的图来演示，所以请忽视图上的文字。

![图源：https://www.srmcad.com/wp-content/uploads/2021/07/10.2.png](https://www.srmcad.com/wp-content/uploads/2021/07/10.2.png)

对于一个雷诺应力分量，比如说上表面的x方向 

$$
\frac{\partial \overline{u_3' u_1'}}{\partial x_1}=\frac{\partial \overline{w' u'}}{\partial x}
$$ 

如果将将单位质量（也就是密度）还给它，就会变成这样

$$
\overline{\bar\rho w' u'}
$$

对于这个分量，是不是很像动量 $Ft=MV$ ？如果你没看明白，那我再对它动点手脚：

$$
Ft=MV \Rightarrow F=\frac{MV}{t}=\frac{ML^3V}{L^3t}=\frac{\rho LVS}{t}={\rho V_1V_2S}
$$

如果是单位面积 （ $S=1$ ），那就和上面的雷诺应力完全一致了！（虽然实际上这样的证明是很不严谨的）这样看来，雷诺应力是一个作用于流体微团表面的力。我们可以把流体微团看成一个微小的立方体。对于这个立方体，有上下，左右，前后三个轴向的面，每个方向的面也能受到x, y, z三个方向的力。也就是说，湍流粘性力，雷诺应力，实质上是湍流对流体微团表面动量的输送。

继续，我们可以用 $\tau_{31}=\overline{\bar\rho w' u'}$ 表示上下表面在x轴上的湍流粘性力。对于流体微团，下表面的湍流粘性应力为 $\tau_{31}|_z$ ，上表面为 $\tau_{31}+|_{z+dz}$ 两个面产生的合力即为 $\frac{(\tau_{31}|_{z}-\tau_{31}|_{z+dz})dxdy}{dxdydz}=\frac{\partial \overline{\bar\rho w' u'}}{\partial x}$ 。

因为我们雷诺分解的依据是 $A=\bar A+A'$ ，也就是说用源方程减去平均的情况可以得到脉动的作用。如果用雷诺展开方程减去雷诺时均方程，就可以得到

$$
\frac{\partial u_i'}{\partial t} + \overline{u_j} \frac{\partial u_i'}{\partial x_j} + u_j' \frac{\partial \overline{u_i}}{\partial x_j} + u_j' \frac{\partial u_i'}{\partial x_j} + \overline{u_j} \frac{\partial u_i'}{\partial x_j} = \frac{1}{\rho} \rho' \frac{\partial (\overline{p} + p')}{\partial x_i} + f \epsilon_{ij3} u_j' - \frac{1}{\rho} \frac{\partial p'}{\partial x_i} + \nu \frac{\partial^2 u_i'}{\partial x_j^2} + \frac{\partial \overline{u_i' u_j'}}{\partial x_j}
$$

这条充满了脉动的方程，我们称之为**脉动方程**。这条方程表征的是湍流脉动的变化。

## 水汽方程
根据我们对于动量方程的处理，我们可以总结导出雷诺时均方程操作流程：
1. 将物理量雷诺展开成平均量与扰动量
2. 对展开后的方程求时间平均
3. 得到平均方程
4. 平均方程减去原方程的平均
5. 得到脉动方程

应用这套流程

由水汽方程

$$
\frac{\partial q}{\partial t} + u_j \frac{\partial q}{\partial x_i} = \nu_q \frac{\partial^2 q}{\partial x_i^2} + \frac{S_q}{\rho} + \frac{E}{\rho}
$$

对水汽含量、速度进行雷诺分解

$$
q = \overline{q} + q', \quad u_j = \overline{u_j} + u_j'
$$

代入原方程并求平均， 最终得到水汽的平均方程

$$
\frac{\partial \overline{q}}{\partial t} + \overline{u_j} \frac{\partial \overline{q}}{\partial x_i} = \nu_q \frac{\partial^2 \overline{q}}{\partial x_i^2} + \frac{\overline{S_q}}{\overline{\rho}} + \frac{\overline{E}}{\overline{\rho}} - \frac{\partial \overline{u_j' q'}}{\partial x_i}
$$

与脉动方程

$$
\frac{\partial q'}{\partial t} + \overline{u_j} \frac{\partial q'}{\partial x_j} + u_j' \frac{\partial \overline{q}}{\partial x_j} + u_j' \frac{\partial q'}{\partial x_j} + \overline{u_j} \frac{\partial q'}{\partial x_j} = \nu_q \frac{\partial^2 q'}{\partial x_j^2} + \frac{\partial \overline{u_j' q'}}{\partial x_j}
$$

其中 $\frac{\partial \overline{u_j' q'}}{\partial x_i}$ 项与雷诺应力项类似，也是湍流作用项，但这项作用的不再是对动量而是水汽的输送作用。

## 状态方程
对于状态方程

$$
p = \rho R T
$$

对压力、密度和温度进行雷诺分解

$$
p = \overline{p} + p', \quad \rho = \overline{\rho} + \rho', \quad T = \overline{T} + T'
$$

代入状态方程

$$
\overline{p} + p' = (\overline{\rho} + \rho')R(\overline{T} + T')
$$

并求平均得到平均方程

$$
\overline{p} = R(\overline{\bar\rho\bar T}+\overline{\rho'T'})
$$

考虑了水汽，此处的状态方程应当写作[湿空气的状态方程](./humidity.md#湿空气的状态方程)

$$
\overline{p} = R_d(\overline{\bar\rho\bar T_v}+\overline{\rho'T_v'})
$$

其中 $R_d$ 为干空气的气体常数， $T_v$ 为虚温。实验说明，在这个方程中， $\overline{\rho'T_v'}$ 是可略去的小量。因此状态方程的平均量形式写作

$$
\overline{p} = R_d\overline{\bar\rho\bar T_v}
$$

与原方程相减，得到

$$
p'=R_d\bar\rho T_v'+R_d\rho'\bar T_v
$$

除以平均量方程，得到

$$
\frac{p'}{\bar p}=\frac{\rho'}{\bar\rho}+\frac{T'_v}{\bar T_v}
$$

由于湍流一般只出现在行星边界层中，且边界层的厚度相对整个大气很薄，所以边界层中的对流系统可以看成浅对流系统。对于浅对流系统， $\frac{\rho'}{\bar\rho}$ 的数量级( $\frac{0.05hPa}{1000hPa}$ )远小于 $\frac{T'_v}{\bar T_v}$ 的数量级 ( $\frac{0.6K}{300K}$ )。消去小量，得到如下表达

$$
\frac{\rho'}{\bar\rho}\approx-\frac{T'_v}{\bar T_v}\approx\frac{\theta'_v}{\bar\theta_v}
$$

其中 $\theta$ 是虚位温。即满足浅对流近似条件下，湍流微团相互之间的密度差异 \( \rho' \) 只决定于其相互之间的虚位温 \( \theta_v' \) 的高低。



## 连续方程
由于连续方程实在是太简单了（在0级近似的情况下），这里就不推导了，直接给出连续方程的平均方程

$$
\frac{\bar u_j}{x_j}=0
$$

与扰动方程

$$
\frac{u'_j}{x_j}=0
$$

这导出了一个极其重要的性质：我们的流体是不可压的。当然，这只是我们的一个基于0级近似的假设，但是它将对我们后续的简化过程起到极大的作用。

## 热流量方程
对热流量方程

$$
\frac{\partial \theta}{\partial t} + u_j \frac{\partial \theta}{\partial x_j} = \nu_\theta \frac{\partial^2 \theta}{\partial x_j^2} - \frac{1}{\rho C_p} \frac{\partial Q_j^*}{\partial x_j} - \frac{L_v E}{\rho C_p}
$$

的温度、速度等进行雷诺分解

$$
\theta = \overline{\theta} + \theta', \quad u_j = \overline{u_j} + u_j', \quad Q_j^* = \overline{Q_j^*} + {Q'_j}^*
$$

代入原方程并求平均并得到最终的平均热流方程

$$
\frac{\partial \overline{\theta}}{\partial t} + \overline{u_j} \frac{\partial \overline{\theta}}{\partial x_j} = \nu_\theta \frac{\partial^2 \overline{\theta}}{\partial x_j^2} - \frac{1}{\overline{\rho} C_p} \frac{\partial \overline{Q_j^*}}{\partial x_j} - \frac{L_v \overline{E}}{\overline{\rho} C_p} - \frac{\partial \overline{u_j' \theta'}}{\partial x_j}
$$

与扰动方程

$$
\frac{\partial \theta'}{\partial t} + \overline{u_j} \frac{\partial \theta'}{\partial x_j} + u'_j \frac{\partial \overline{\theta}}{\partial x_j} + u'_j \frac{\partial \theta'}{\partial x_j} + \overline{u_j} \frac{\partial \theta'}{\partial x_j} = \nu_\theta \frac{\partial^2 \theta'}{\partial x_j^2} + \frac{\partial \overline{u_j' \theta'}}{\partial x_j} - \frac{1}{\rho C_p} \frac{\partial Q_j^*}{\partial x_j}
$$

相似的， $\frac{\partial \overline{u_j' \theta'}}{\partial x_j}$ 项也表示湍流对于热流量的输送作用。

## 动量脉动方程的简化
对于动量脉动方程

$$
\frac{\partial u_i'}{\partial t} + \overline{u_j} \frac{\partial u_i'}{\partial x_j} + u_j' \frac{\partial \overline{u_i}}{\partial x_j} + u_j' \frac{\partial u_i'}{\partial x_j} + \overline{u_j} \frac{\partial u_i'}{\partial x_j} = \frac{1}{\rho} \rho' \frac{\partial (\overline{p} + p')}{\partial x_i} + f \epsilon_{ij3} u_j' - \frac{1}{\rho} \frac{\partial p'}{\partial x_i} + \nu \frac{\partial^2 u_i'}{\partial x_j^2} + \frac{\partial \overline{u_i' u_j'}}{\partial x_j}
$$

考虑浅对流情况，可以使用

$$
\frac{\rho'}{\bar\rho}\approx\frac{\theta'_v}{\bar\theta_v}
$$

结合静力平衡关系 $\partial\bar p=g\bar\rho \partial z$ ，可以推出

$$
-\frac{\rho'}{\rho} \cdot \frac{1}{\rho} \frac{\partial \overline{p}}{\partial z} = - \frac{\theta_v'}{\overline{\theta_v}} g
$$

这样就可以用浮力来替换这一坨 $\frac{1}{\rho} \rho' \frac{\partial (\overline{p} + p')}{\partial x_i}$ ，得到简化后的动量脉动方程

$$
\frac{\partial u_i'}{\partial t} + \overline{u_j} \frac{\partial u_i'}{\partial x_j} + u_j' \frac{\partial \overline{u_i}}{\partial x_j} + u_j' \frac{\partial u_i'}{\partial x_j} + \overline{u_j} \frac{\partial u_i'}{\partial x_j} = \delta_{i3} g \frac{\theta_v'}{\overline{\theta_v}} + f \epsilon_{ij3} u_j' - \frac{1}{\rho} \frac{\partial p'}{\partial x_i} + \nu \frac{\partial^2 u_i'}{\partial x_j^2} + \frac{\partial \overline{u_i' u_j'}}{\partial x_j}
$$

## 湍流动能方程
为了得到湍流发展过程中的能量传递过程，我们需要引入湍流动能。首先，在[大气能量学](./energy.md)中，我们认识到了流体的动能 $E_k=\frac{\vec V^2}{2}$ 。又由于雷诺分解后，速度可以表达成 $V=\bar V + V'$，那么对于速度推出的能量也有 $E_{total} =\frac{\vec V^2}{2}=E_{MKE}+E_{TKE}$ 。在这个式子中， $E_{MKE}$ 表示**平均动能**（mean kinetic energy），即湍流运动中有序运动那部分流场的动能； $E_{TKE}$ 表示**湍流动能**（turbulence kinetic energy），即流场中做无序运动的那部分动能。由于湍流动能是无序的运动，这意味着它可能出现在各个方向上。为此，为了精确描述他们的分布， $E_{TKE}$ 需要写成 $E_{TKE}=\frac{\bar {u'^{2}}+\bar {v'^{2}}+\bar {w'^{2}}}{2}$ ，即将它们在各个方向上的分量相加。

这样，搜寻之前的知识，需要预报湍流动能与时间的关系，需要用到动量方程的脉动形式

$$
\frac{\partial u_i'}{\partial t} + \overline{u_j} \frac{\partial u_i'}{\partial x_j} + u_j' \frac{\partial \overline{u_i}}{\partial x_j} + u_j' \frac{\partial u_i'}{\partial x_j} = \delta_{i3} g \frac{\theta_v'}{\overline{\theta_v}} + f \epsilon_{ij3} u_j' - \frac{1}{\rho} \frac{\partial p'}{\partial x_i} + \nu \frac{\partial^2 u_i'}{\partial x_j^2} + \frac{\partial \overline{u_i' u_j'}}{\partial x_j}
$$

所有项乘上 $2u_i'$ ，得到

$$
2u_i'\frac{\partial u_i'}{\partial t} + 2u_i'\overline{u_j} \frac{\partial u_i'}{\partial x_j} + 2u_j' u_i'\frac{\partial \overline{u_i}}{\partial x_j} = 2u_i'\delta_{i3} g \frac{\theta_v'}{\overline{\theta_v}} + 2u_i'f \epsilon_{ij3} u_j' - 2u_i'\frac{1}{\rho} \frac{\partial p'}{\partial x_i} + 2u_i'\nu \frac{\partial^2 u_i'}{\partial x_j^2} + 2u_i'\frac{\partial \overline{u_i' u_j'}}{\partial x_j}
$$

稍微整理下，得到

$$
\frac{\partial u_i'^2}{\partial t} + \overline{u_j} \frac{\partial {u_i'}^2}{\partial x_j} + u_i' u_j'\frac{\partial \overline{u_i}}{\partial x_j} + u_i'u_j' \frac{\partial u'_j}{\partial x_i} = \delta_{i3} g u_i' \frac{\theta_v'}{\overline{\theta_v}} + \epsilon_{ij3} u_j' u_i'f - u_i'\frac{1}{\rho} \frac{\partial p'}{\partial x_i} + u_i'\nu \frac{\partial {u'_i}^2}{\partial x_j^2} + u_i'\frac{\partial \overline{u_i' u_j'}}{\partial x_j}
$$

求时均，得**湍流方差预报方程**。（为什么叫湍流方差预报方程，是由于这个方程是基于速度平方对时间的平均，而平方的平均就是方差，所以也称为方差预报方程）

$$
\frac{\partial \overline{u_i'^{2}}}{\partial t} + \overline{u_j} \frac{\partial \overline{u_i'^{2}}}{\partial x_j} + 2 \overline{u_i' u_j'} \frac{\partial \overline{u_i}}{\partial x_j} + 2 \overline{u_i' u_j' \frac{\partial u'_i}{\partial x_j}} = -2 \delta_{i3} g \frac{\overline{u_i' \theta_v'}}{\overline{\theta_v}} + 2 f \epsilon_{ij3} \overline{u_i' u_j'} - \frac{2}{\rho} \overline{u_i' \frac{\partial p'}{\partial x_i}} + 2 \nu \overline{u_i' \frac{\partial^2 u_i'}{\partial x_j^2}} + 2 \overline{u_i'} \frac{\partial \overline{u_i' u_j'}}{\partial x_j}
$$

### 不可压湍流动能方程的简化

这个方法无论怎么看都无比复杂，如果实际操作这样的方程将造成计算量的大提升。为此，我们需要一些合适的方法简化这个方程。考虑到不可压假设带来的 $\frac{\partial u_j}{\partial x_j}=0$ ，我么可以通过链式法则来实现这一目标。

对于最后一项， $2 \overline{u_i'} \frac{\partial \overline{u_i' u_j'}}{\partial x_j}$ ，尽管 $\frac{\partial \overline{u_i' u_j'}}{\partial x_j}$ 并不是0（因为其是扰动的乘积），但再乘上一个微小的扰动的平均（ $\bar u'_i=0$ ），因此我们在此约去。

后面的章节原本是不想用每项的物理意义作为标题的，因为这有剧透的嫌疑。但是发现使用项的位置进行命题在查看的时候不太方便，于是还是选用了物理意义作为标题。


#### 耗散项的简化

对于倒数第二项耗散项 $2 \nu \overline{u_i' \frac{\partial^2 u_i'}{\partial x_j^2}}$ ，可以写成

$$
2\nu\overline{u'_i\frac{\partial^2 u'_i}{\partial x_j^2}}=\nu\overline{\frac{\partial^2 u'_i}{\partial x_j^2}}-2\nu\overline{\frac{\partial u'_i}{\partial x_j}\frac{\partial u'_i}{\partial x_j}}
$$

至于为什么，我想倒过来解释会更加方便。 对于 $\overline{\frac{\partial^2 u'_i}{\partial x_j^2}}$ ，应用链式法则

$$
\overline{\frac{\partial^2 u'_i}{\partial x_j^2}}=\overline{\frac{\partial }{\partial x_j}(\frac{\partial {u'_i}^2}{\partial x_j}})=\overline{\frac{\partial }{\partial x_j}(\frac{2u'_i\partial {u'_i}}{\partial x_j}})=2\overline{\frac{\partial u'_i}{\partial x_j}\frac{\partial u'_i}{\partial x_j}}+2\overline{u'_i\frac{\partial^2u'_i}{\partial x_j^2}}
$$

整理后乘上 $\nu$ ，即得上式。

$$
2\nu\overline{u'_i\frac{\partial^2 u'_i}{\partial x_j^2}}=\nu\overline{\frac{\partial^2 u'_i}{\partial x_j^2}}-2\nu\overline{\frac{\partial u'_i}{\partial x_j}\frac{\partial u'_i}{\partial x_j}}
$$

对于右边的第一项 

$$
\nu\overline{\frac{\partial^2 u'_i}{\partial x_j^2}}
$$

写成好看点的形式 $\nu\nabla^2\vec V$ ，表示为湍流耗散的空间分布，是湍流脉动速度的扩散项。在大气科学中， $ \frac{\partial^2 \overline{u_i'^2}}{\partial x_j^2} $ 的量级为 $ 10^{-6} s^{-2} $ 到 $ 10^{-2} s^{-2} $，$\nu$ 量级为 $ 10^{-5} m^2 s^{-1} $ 。得该项量级 $ 10^{-11} m^2 s^{-3} $（混合层）到 $ 10^{-7} m^2 s^{-3} $（近地层）。

对于右边的第二项 

$$
2\nu\overline{\frac{\partial u'_i}{\partial x_j}\frac{\partial u'_i}{\partial x_j}}
$$

表示为为分子黏性耗散项。其中 $ \left( \frac{\partial u_i'}{\partial x_j} \right)^2 $ 的量级为 $ 10^2 s^{-2} $，$\nu$ 量级为 $ 10^{-5} m^2 s^{-1} $，则该项量级 $ 10^{-4} m^2 s^{-3} $（混合层）到 $ 10^{-2} m^2 s^{-3} $（近地层）。

相比之下，第一项是量级远小于第二项的小量，可以忽略。

令

$$
\overline{\frac{\partial^2 u'_i}{\partial x_j^2}}=\varepsilon
$$

此项最终写成

$$
-2\nu\overline{\frac{\partial^2 u'_i}{\partial x_j^2}}=-2\varepsilon
$$

#### 气压扰动项的简化
对于倒数第三项

$$
-\frac{2}{\rho} \overline{u_i' \frac{\partial p'}{\partial x_i}}
$$

引入链式法则，可以写成

$$
-\frac{2}{\rho} \overline{u_i' \frac{\partial p'}{\partial x_i}}=-\frac{2}{\rho}\frac{\partial p'u'_i}{\partial x_i}+\frac{2p'}{\rho}\frac{\partial u'_i}{\partial x_i}
$$

对于 $\frac{2p'}{\rho}\frac{\partial u'_i}{\partial x_i}$ 其起到的作用是气压扰动引起的速度梯度再分配。但是在我们的简化条件中，速度梯度是0，因此这项可以略去。

略去这项的气压梯度变成

$$
-\frac{2}{\rho}\frac{\partial p'u'_i}{\partial x_i}
$$

#### 科氏力项的简化
对于倒数第四项

$$
2 f \epsilon_{ij3} \overline{u_i' u_j'}
$$

可以展开为

$$
2 f \epsilon_{ij3} \overline{u_i' u_j'}=2 f \epsilon_{123} \overline{u_i' u_j'}+2 f \epsilon_{213} \overline{u_i' u_j'}=2 f\overline{u_i' u_j'}-2 f\overline{u_i' u_j'}=0
$$

于是科氏力项就被我们消没了。也很符合我们的直觉，因为科氏力的方向永远垂直速度方向，这就注定它无法做功对动能产生影响。

#### 湍流动能输送项的简化
对于湍流动能方程中的这项

$$
-2 \overline{u_i' u_j' \frac{\partial u'_i}{\partial x_j}}
$$

由于 $\frac{\partial u'_j}{\partial x_j}=0$ ，为它补一个 $\overline{{u'_i}^2\frac{\partial u'_j}{\partial x_j}}$

得到

$$
-2 \overline{u_i' u_j' \frac{\partial u'_i}{\partial x_j}} = -2 \overline{u_i' u_j' \frac{\partial u'_i}{\partial x_j}} - \overline{{u'_i}^2\frac{\partial u'_j}{\partial x_j}}=-\overline{u_j' \frac{\partial {u'_i}^2}{\partial x_j}} - \overline{{u'_i}^2\frac{\partial u'_j}{\partial x_j}}=-\overline{\frac{\partial {u'_i}^2u'_j}{\partial x_j}}
$$

这项表示i方向的湍流动能在j方向的传播。它不起到产生动能的作用，但是起到传播能量的作用。

### 简化后的湍流方差方程
综上，简化后的湍流方差方程如下

$$
\frac{\partial \overline{u_i'^2}}{\partial t} + \overline{u_j} \frac{\partial \overline{u_i'^2}}{\partial x_j} = 2 \delta_{i3} g \frac{\overline{u_i' \theta_v'}}{\overline{\theta_v}} - 2 \overline{u_i' u_j'} \frac{\partial \overline{u_i}}{\partial x_j} - \frac{\partial \overline{u_i'^2 u_j'}}{\partial x_j} - \frac{2}{\rho} \overline{u_i' \frac{\partial p'}{\partial x_i}} - 2 \varepsilon
$$

换成 $E_{TKE}=\frac{\bar {u'^{2}}+\bar {v'^{2}}+\bar {w'^{2}}}{2}$ 得到湍流动能方程

$$
\frac{\partial \overline{E_{TKE}}}{\partial t} + \overline{u_j} \frac{\partial \overline{E_{TKE}}}{\partial x_j} = \delta_{i3} g \frac{\overline{u_i' \theta_v'}}{\overline{\theta_v}} - \overline{u_i' u_j'} \frac{\partial \overline{u_i}}{\partial x_j} - \frac{\partial \overline{E_{TKE} u_j'}}{\partial x_j} - \frac{1}{\rho} \overline{u_i' \frac{\partial p'}{\partial x_i}} - \varepsilon
$$

我们现在来分析每项的物理意义

### 湍流动能方程的物理意义
#### 湍流动能随时间变化项
对于第一项 $\frac{\partial \overline{E_{TKE}}}{\partial t}$ ，相信大家都知道是做什么的了，就不多赘述了。

#### 平流项
对于第二项 $\overline{u_j} \frac{\partial \overline{E_{TKE}}}{\partial x_j}$ ，也不难看出，这是平流项，表示随风从远方输送过来的湍流能量。

#### 浮力项
对于 $\delta_{i3} g \frac{\overline{u_i' \theta_v'}}{\overline{\theta_v}}$ ，当 $i=3$ 时，根据[静力不稳定](./instability.md#静力不稳定)章节对于位温的讨论，这项的物理意义是浮力作用。

在白天太阳直射地面，大地受到辐射作用升温并加热近地面大气。这样局地的高温产生了浮力作用。因此在白天，混合层以下的浮力项作用为正，产生湍流动能；在晚上或者太阳不能直射的地区，浮力项作用为负，抑制湍流动能产生。

#### 切变项
对于 $\overline{u_i' u_j'} \frac{\partial \overline{u_i}}{\partial x_j}$ ，写成向量形式为 $-\overline{u' w'} \frac{\partial \overline{u}}{\partial z} - \overline{v' w'} \frac{\partial \overline{v}}{\partial z}$ 。不难看出这是风切变对湍流动能的贡献。

由于地球的摩擦作用，在地表的风速一定是0。也就是说无论如何，边界层中一定有风切变。而风切变的大小只取决于风速的大小。这幅图展示了地表风切变随高度的变化。

![风切变](./fig4pbl/wind%20sheer.png)

关于湍流动能中的切变项与浮力项更进一步的讨论放在了[湍流的产生机制](./turbulence1.md#湍流的产生机制)中论述。

同时在混合层的顶部，由于存在湍流对于自由大气的[夹卷作用]()，会将自由大气中动能更大的风裹挟至混合层，在此处产生风切变的  次大值

#### 湍流输送项
对于 $\frac{\partial \overline{E_{TKE} u_j'}}{\partial x_j}$ ，这项表示湍流动能的脉动输送。与平流项类似，他们都只对湍流动能起到传输的作用，而没有生成与耗散的作用。但是湍流输送项是由湍流的脉动本身主动传输，相当于你把能量递给我，我再把能量递给别人；而平流项是大尺度的平均场的作用，相当于一团湍流被一阵风吹去别处，自然湍流携带的动能也被带到了别处。

#### 气压脉动项
$\frac{1}{\rho} \overline{u_i' \frac{\partial p'}{\partial x_i}}$ 项表示气压梯度脉动产生湍流动能的作用。可惜的是，在边界层中，气压脉动相当小，导致实际大气中该项通常被忽略或作为湍流动能方程的余项予以考虑。

#### 耗散项
对于耗散项 $\varepsilon$ ，表征分子粘性应力对湍流动能的耗散作用，它将湍流动能转化为热能。