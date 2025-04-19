# PID 控制

**PID** 即比例 (Proportional)、积分 (Integral)、微分 (Differential) 的缩写。PID控制是一种闭环控制算法，它动态改变施加到被控制对象身上的控制输出值(Out)，使得被控制对象某一物理量的实际值(Actual)，能够快速、准确、稳定地跟踪到指定的目标值(Target)。PID控制是一种基于误差(Error)的调控算法，其中规定：误差 = 目标值 - 实际值，算法的目的是使得误差始终为0。

PID对被控对象的要求低，无需建模，即便是被控对象内部运作的规律不明确，PID也能控制。

## PID公式和介绍

$$
\begin{equation}\begin{split} 
误差： &error(t) = target(t) - actual(t) \\
输出值： &out(t) = K_p(error(t) + \frac{1}{T_i}\int_0^t error(t)dt + T_d\frac{derror(t)}{dt}) \\
输出值(简化)： &out(t) = K_p error(t) + K_i \int_0^t error(t)dt + K_d \frac{derror(t)}{dt}
\end{split}\end{equation}
$$

### 1、比例项 (P)

只含有**比例项**的PID输出值：
$$
\begin{equation}
out(t) = K_p error(t)
\end{equation}
$$
比例项的输出值仅取决于当前时刻的误差，与历史时刻无关，因此存在稳态误差。稳态误差是指系统进入稳定状态时，实际值和目标值存在一个稳定的差值。

### 2、积分项 (I)

含有比例项和**积分项**的PID输出值：
$$
\begin{equation}
out(t) = K_p error(t) + K_i \int_0^t error(t)dt
\end{equation}
$$
积分项的输出值取决于0到t所有时刻误差的积分，与历史时刻有关。积分项的可以消除纯比例项产生的稳态误差。

### 3、微分项 (D)

含有比例项、积分项和**微分项**的PID输出值：
$$
\begin{equation}
out(t) = K_p error(t) + K_i \int_0^t error(t)dt + K_d \frac{derror(t)}{dt}
\end{equation}
$$
微分项的输出取决于当前时刻误差的变化率，与当前时刻误差的变化趋势有关。微分项可以阻碍误差的急剧变化，增加系统阻尼。

## 离散PID公式

连续形式：
$$
\begin{equation}
out(t) = K_p error(t) + K_i \int_0^t error(t)dt + K_d \frac{derror(t)}{dt}
\end{equation}
$$
离散形式：
$$
\begin{equation}
out(t) = K_p error(t) + K_i T \sum_{j=0}^t error(j) + K_d \frac{error(t) - error(t - 1)}{T}
\end{equation}
$$
离散形式简化：
$$
\begin{equation}
out(t) = K_p error(t) + K_i \sum_{j=0}^t error(j) + K_d (error(t) - error(t - 1))
\end{equation}
$$
