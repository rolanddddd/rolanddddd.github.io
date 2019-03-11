# 数据类型



### logic类型

{% hint style="info" %}
SV对reg数据类型进行改进，使其除了作为变量以外，还可以被连续赋值、门单元和模块驱动；

使用线网的地方均可以使用logic，但要求logic只能有一个驱动，若多个驱动需要使用wire类型
{% endhint %}

```javascript
wire[7:0] byte = data[select +: 8] (data[select+7 ： select])
wire[7:0] byte = data[select -: 8] (data[select ： select-7])
```

### 2.双状态数据类型

* bit b  ： 双状态，单bite
* bit \[31:0\] b32  :  双状态，32比特无符号整数
* int unsigned ui ： 双状态，32比特无符号整数

