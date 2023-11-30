
[[Video Editing]]

DaVinci Resolve -> Free
DaVinci Resolve Studio -> Paid

### Tutorial

影视飓风： [https://space.bilibili.com/946974/channel/collectiondetail?sid=284](https://space.bilibili.com/946974/channel/collectiondetail?sid=284)

DJI Mavic 2 Pro LUT：[https://www.dji.com/cn/downloads/products/mavic-2](https://www.dji.com/cn/downloads/products/mavic-2)

Rec. 709 created in 1990
Recommend to use AECS

### Tips

Shortcut| 
---|---
J|前进 / 快进
K|暂停
L|后退 / 快退
I|in 入点
O|out 出点
F9|选择素材 将素材放到时间轴
shift v|选择当前时间轴上的素材
shift \[ / ]|修建素材到当前帧
shift delete|

<br/>

预览| 
---|---
ctrl f|视频全屏
p|视频全屏
alt f|影院模式

change clip color
![[clip-color.gif|500]]

↑ / ↓ move to clip start / end
← / → move 1 frame
shift ← / → move 5 frames
![[clip-start-end.gif]]



### Color Grading

Shortcut| 
---|---
ctrl d|关闭单个节点
shift d|关闭调色
shift h|突出显示 显示mask区域
shift +|复制前倒数第一个的素材调色
shift -|复制前倒数第二个的素材调色
rmb > cleanup Node Graph 清理节点图|


Grab Still 截图
![[grab-still.gif|500]]

Scopes 示波器
![[davinci-resolve-scopes.png|500]]

- Lum Mix 亮度混合
    - 颜色通道影响其他颜色：例如调整R时，G B也会变化
    - Lum Mix为0时，调整颜色通道时不影响其他颜色通道

波形图
上下亮度
1. 亮度
2. 白色校准, 白平衡
	![[davinci-resolve-waveform-whitebalance.png]]

Vectorscope 矢量图
看到颜色偏移（倾向）
![[davinci-resolve-vectorscope.png|300]]

- white balance
![[davinci-resolve-whitebalance.png|300]]

##### qualifier 限定器
	- → mask?
	- shift h - isolate mask area
	- Pre-filter 降噪 （减少色块）
	- 与蒙版，跟踪配合使用
	- 魔法蒙版

disconnect node|add serial node 添加串行节点 Alt S
---|---
![[davinci-resolve-disconnect-node.gif]]|![[davinci-resolve-add-serial-node.gif]]

##### 节点类型
- 串行节点 Alt S
- 并行节点 Alt P
- 图层节点 Alt L （可与并行节点转换）
		- 混合模式
		- 图层顺序：下面图层盖住上面图层
- 外部节点
	- 蒙版 / 抠像 反向节点
- RGB分离节点

绿点 → 颜色
蓝点 → 通过 mask → alpha

##### HDR Grade HDR色轮
- 更多调整选项

##### Color Warper 颜色扭曲器
- 调整色相，饱和度


###### copy nodes

mmb on target clip|+ copy previous clip
---|---
![[davinci-resolve-copy-node-mmb.gif]]|![[davinci-resolve-copy-node-+.gif]]

Clips Group
![[davinci-resolve-clips-group.gif]]

##### 节点
- 色彩空间转换
> [!note] 在Group Pre-Clip中不同相机先色彩空间转换



Lightbox 光箱 → 选择素材

调整片段 Color Grading在Editing中

##### Denoise
![[davinci-resolve-denoise.png]]

时域降噪
	- 多帧分析 → 拖影
空域降噪
	- 单帧 → 闪烁 跳跃

亮度 黑白噪点
色度 彩色噪点

Effects > 
	- deflicker 去闪烁
	- 物体移除
	- 面部修饰 > 磨皮

### Editing
- Hold MMB move / Ctrl Scroll
- B Blade / Ctrl \\ cut

Keyframe & Curve
![[davinci-resolve-keyframe&curve.gif|500]]

Ctrl C & Alt V Copy Attributes, Keyframes
![[davinci-resolve-copyAttributes.gif|500]]

##### Caption
![[davinci-resolve-caption.gif]]

通过第三方软件生成.srt字幕文件导入达芬奇
File > Import > Subtitle

Dynamic Zoom → iMovie缩放


### Preparation / organization

Project Settings > Color Management > Color Settings > Rec. 709

For Mac
Preferences  Command ,
✅ use Mac display color profiles for viewers


### Fairlight
音频

响度单位
- LUFS 绝对响度
- LU 相对响度
- dB Decibel 分贝 (对音量)


互联网节目
Target loudness level → -16
BS.1770-4

绝对比例
人声 → mono 单声道
1.0 单声道
2.0 立体声

效果器

### Fusion
合成软件