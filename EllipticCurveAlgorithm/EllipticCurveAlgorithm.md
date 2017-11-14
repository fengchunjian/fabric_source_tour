# Fabric 1.0源码之旅(3)-椭圆曲线算法
BCCSP模块中，涉及椭圆曲线算法，本文专门讲解。
椭圆曲线算法go标准库即支持，如下均为标准库代码。
## 1、椭圆曲线算法概论
### 1.1、无穷远点、无穷远直线、射影平面
* 平行线相交于无穷远点；
* 直线上有且只有一个无穷远点；
* 一组相互平行的直线有公共的无穷远点；
* 平面上任何相交的两直线，有不同的无穷远点；
* 全部无穷远点沟通一条无穷远直线；
* 平面上全部无穷远点和全部普通点构成射影平面。
### 1.2、射影平面点定义
对于普通平面上点(x, y)，令x=X/Z，y=Y/Z，Z≠0，则投影为射影平面上的点为(X : Y : Z)。
如点(1，2)在射影平面的坐标为：(Z : 2Z : Z) Z≠0，即(1 : 2 : 1)或(2 : 4 : 2)均为(1, 2)在射影平面上的点。
Z=0时，(X : Y : 0)即为无穷远点，Z=0即为无穷远直线。
### 1.3、椭圆曲线方程
椭圆曲线的定义：
一条椭圆曲线是在射影平面上满足方程Y²Z+a1XYZ+a3YZ²=X³+a2X²Z+a4XZ²+a6Z³的所有点的集合，且曲线上的每个点都是非奇异（或光滑）的。
该方程为维尔斯特拉斯方程，是一个齐次方程。
所谓“非奇异”或“光滑”的，即满足方程的任意一点都存在切线。

椭圆曲线存在无穷远点(0, Y, 0)，可以在平面坐标系中用椭圆曲线、加一个无穷远点来表示。
令x=X/Z，y=Y/Z，代入椭圆曲线方程，即椭圆曲线普通方程：y²+a1xy+a3y = x³+a2x²+a4x+a6。