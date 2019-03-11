# 数据类型

### 1. 内建数据类型

#### 1. logic类型

{% hint style="info" %}
SV对reg数据类型进行改进，使其除了作为变量以外，还可以被连续赋值、门单元和模块驱动；

使用线网的地方均可以使用logic，但要求logic只能有一个驱动，若多个驱动需要使用wire类型
{% endhint %}

#### 2. 双状态数据类型

* bit b  ： 双状态，单bit
* bit \[31:0\] b32  :  双状态，32比特无符号整数
* int unsigned ui ： 双状态，32比特无符号整数
* int i：双状态，32bit有符号整数
* byte b8：双状态，8bit有符号整数
* shortint s：双状态，16bit有符号整数
* longint l：双状态，64bit有符号整数
* integer i14：四状态，32bit有符号整数
* time t：四状态，64bit无符号整数
* real r：双状态，双精度浮点数

