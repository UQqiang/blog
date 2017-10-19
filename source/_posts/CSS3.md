---
title: 2D 3D 动画
date: 2016-09-27 22:21:08
---

发现对css3一些知识不怎么熟练了。。。。。巩固一下

## 2D
1. 旋转
```
  rotate(deg)  
  deg  度数（旋转的是坐标系）正值为顺时针，负值为逆时针; 
```
2. 倾斜
```
  skew(deg) 水平方向
  skew(deg, deg)  (水平,垂直)
  skewX()、skewY()
```
3. 缩放
```
  scale(x)  水平和垂直方向缩放该倍率
  scale(x, y) （水平垂直）x、y的取值可为小数，不可为负值；
  scaleX()、scaleY()
```
4. 位移函数

```
  translate()
  translate(x, y) 可以改变元素的位置，x、y可为负值；
  默认以元素的中心点为基点，向x，y轴方向移动
  一个参数时:表示向水平方向移动
  两个参数时:向x，y夹角方向移动
  translateX()、translateY()

```


## 3D

1. 建立3D空间
```
  transform-style: preserve-3d; 
```
2. 视角基点（从哪个点进行观看）表示相对左上角原点的距离
```
  perspective-origin: -200% 200%;
  两个参数除了可以设置为具体的像素值，
  第一个参数可以指定为left、center、right，
  第二个参数可以指定为top、center、bottom
```

3. 景深
```
  perspective:0px; 
```
4. 属性定义当元素不面向屏幕时是否可见
```
  backface-visibility:hidden;  
```

## 动画 
### 动画描述
    @keyframes change{ from{ } 30%{ }  to{ } }
    @keyframes change{ 0%{ } 100%{ } }

### 动画调用
1. 动画名称
```
  animation-name: change;
```
2. 动画持续时间
```
  animation-duration: 5s; 
```
3. 动画运动方式
```
  animation-timing-function: ease;  
    linear:匀速;
    ease:缓冲;
    ease-in-out:慢-快-慢;
    cubic-bezier(number,number, number, number):贝塞尔曲线,4个数[0, 1]
```
4. 动画延迟（只是第一次）
```
  animation-delay: 1s;
```
5. 重复次数
```
  animation-iteration-count: infinite;
    参数n
    infinite(一直) 
```
6. 
```
  animation-direction: alternate;
    alternate:从上次停止的位置开始;
    normal:动画第二次直接跳到0%的状态开始 
```
7. 播放状态
```
  animation-play-state: running;
    running(播放);
    paused(暂停) 
```
8. 规定对象动画时间之外的状态
```
  animation-fill-mode: both;
    none：不改变默认行为
    forwards：动画执行完毕保持最后一个属性值
    backwards：动画执行之前 保持开始状态
    both：forwords和backwords都保持
```
9. 简写
```
  animation: change 5s ease 1s infinite alternate;
```

## 渐变

   