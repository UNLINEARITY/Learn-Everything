---
{"dg-publish":true,"dg-path":"工具/manim.md","permalink":"/工具/manim/","dgPassFrontmatter":true,"noteIcon":"","created":"2024-05-21T15:20:27.867+08:00","updated":"2024-08-02T18:32:21.561+08:00"}
---

An animation engine for precise programmatic animations.   
制作数学动画      [官方文档](https://docs.manim.community/en/stable/index.html#)
[社区](https://www.manim.community/)


主文件由  [[Python\|Python]]  编写
使用  [[PowerShell\|PowerShell]]  自动化配置
使用   [[FFmpeg\|FFmpeg]]   渲染视频
[[LaTex\|LaTex]]  书写数学公式  
[[Opengl\|Opengl]] 交互性渲染

-qp
```powershell
manim -pql scene.py CreateCircle
```

```python  
from manim import *

class CreateCircle(Scene):
    def construct(self):
    	circle = Circle()  # create a circle
    	circle.set_fill(PINK, opacity=0.5)  # set the color and transparency
    	self.play(Create(circle))  # show the circle on screen 
```


定义了一个名为 `CreateCircle` 的类。这个类继承自 `Scene`，表示它是一个Manim场景类。在Manim中，所有的动画场景都是从 `Scene` 类派生出来的。

类的一个方法定义，名为 `construct`。在Manim中，`construct` 方法是场景的主体，所有动画的构建和播放指令都写在这个函数中。`self` 参数是对当前对象实例的引用。


创建了一个 `Circle` 对象，并将其赋值给变量 `circle`。`Circle` 是Manim中用于创建圆形的类。

调用 `circle` 对象的 `set_fill` 方法来设置圆形的填充颜色和透明度

使用`self.play`方法来播放一个动画，这个动画是由`Create`函数生成的

### Output Settings 

```PowerShell
manim -flag file.py classname
```

- `manim`   命令行工具的名称，用于执行Manim动画的创建
- `-flag`   一组命令行选项的缩写
- `file.py`   包含Manim代码的Python脚本文件的名称
- `classname`   要渲染的Manim场景的类名
	Manim会查找这个类，并执行其中的`construct`方法来生成动画。


命令行选项
**command line flags**

`-p`  plays the animation once it is rendered
`-f`  open the file browser at the location of the animation instead of playing it

`-ql`   854x480 15FPS    low render quality
`-qm`   1280x720 30FPS    medium
`-qh`   1920x1080 60FPS    high
`-qp`   2560x1440 60FPS   2k
`-qk`   3840x2160 60FPS   4k

`--format gif`   更改文件输出格式为 [[gif\|gif]]

### Mobjects
Mobject 类是所有其他 mobject 的抽象基类
Mobjects are the basic building blocks for all manim animations.

Each class that derives from Mobject represents an object that can be displayed on the screen.

By default, mobjects are placed at the center of coordinates, or _origin_, when they are first created.
Further, the Shapes scene places the mobjects by using the shift () method 

```python
# 初始位置设置
circle=Circle()
circle.shift(ORIGN/UP/DOWN/LEFT/RIGHT)
#  UP/DOWN/LEFT/RIGHT 上、下、左、右单位向量
square=Square().shift(UP*2)
```

```python
# 初始位置设置
circle=Circle()
circle.shift(ORIGN/UP/DOWN/LEFT/RIGHT)
#  UP/DOWN/LEFT/RIGHT 上、下、左、右单位向量
square=Square().shift(UP*2)
```


```python
circle.set_stroke(color= COLOR, width= )  # 设置线条
circle.set_fill(COLOR, opacity= )   # 设置填充
```

### Animations 动画
At the heart of manim is animation. Generally, you can add an animation to your scene by calling the `play ()` method.

animations are procedures that interpolate between two mobjects

```python
self.play(FadeIn(square))
self.play(Rotate(square,PI/4))
self.play(FadeOut(square))
```

```python 
self.play(square.animate.shift(UP), run_time=3)
```


一个动画 animation 本质是函数/映射  
特殊的函数：alpha_function 动画函数
alpha 为动画的完成率，取值范围 0-1 
alpha% 


```C
def Alpha_F(mobject,t):
	x=f(t)
	mobject.method(g(x))

mob=mobject()
self.add(mob)
self.play(UpdateFromAlphaFunc(mob,Alpha_F,run_time=))
```

#### .animate  
mobj. method () 通常返回一个 mobject ，不能作为参数传递到 play () 中
可以使用 .animate  来传递，播放动画
```python 
self.play(mobj.animate.method())
```

但是注意. animate 实际上并不知道你需要什么动画，它只知道起始的状态和终止的状态，然后进行线性插值，不能实现点的实际运动

例子：
```python
VGroup(s1,s2).arrange(Right,buff=1)
self.add(s1,s2)
self.play(s1.animate.rotate(PI),Rotate(s2,PI),run_time=2)
```

![DifferentRotations_ManimCE_v0.18.0.post0.gif](/img/user/%E5%8A%9F%E8%83%BD%E6%80%A7%E6%96%87%E4%BB%B6%E5%A4%B9/%E8%BD%BD%E5%85%A5%E7%9A%84%E5%AA%92%E4%BD%93%E8%B5%84%E6%BA%90/DifferentRotations_ManimCE_v0.18.0.post0.gif)

#### 自定义动画
从 Animation 类中继承，重载函数
与库中已经实现的函数比较

```python 
begin()
interpolate_mobject(alpha)
interpolate_submobject(sub,sub_start,alpha)
finish()
clean_up_from_scene(scene)
```


### Update Function 

Mobject can be made dependent on other mobjects 
Mobject update   /  Scene update 




### LaTeX 渲染 

```python 
tex = MathTex(r"\string",font_size=)
tex = Tex(r"$\string$",font_size=)
```

`Tex`     渲染一般字符串
`MathTex`   默认渲染 `$ $`  公式符号


