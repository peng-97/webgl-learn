## 关于attribute  只能在顶点着色器中 用来表示顶点信息

uniform  用在顶点着色器和片元着色器中 只读，如果在顶点着色器和片元着色中有相同变量名，则数据会共享（顶点-片元）   变换矩阵会所有顶点都会使用就是使用uniform

varying 从顶点着色器想片元着色器传输数据，变量名要一样---就是光栅化的歌城

pro中  3文件有关于顶点着色器和片元着色器的描述和说明、
4 纹理
vertexAttribPointer函数  p135  开始于b7
六个参数 location 位置参数
//方法说明
locationg  位置 、
size  每个位置需要的顶点（1-4)(这是2 ，原本需要的 z,w,会默认补全) 、
type   数据类型格式（数据是什么类型）
normlize  是否将浮点归一化
stride  相邻像个定点的字节数（默认是0）
offst 缓冲区对象中的偏移量（从那个位置开始用用顶点）
纹理的填充方法pro4 4中   gl.TEXTURE_MIN_FILTER  gl.TEXTURE_MAG_FILTER  纹理放大缩小（minamap
gl.TEXTURE_Warp_S  TEXTURE_Warp_S gl.TEXTURE_MAG_FILTER（水平 垂直）
gl.TEXTURE_MIN_FILTER  gl.TEXTURE_MAG_FILTER      gl.nearset 中心最近  gl.LINer（四像素建群平均）
gl.TEXTURE_MIN_FILTER  gl.TEXTURE_MAG_FILTER    （gl.repaet平铺重复 gl。mirroredPrepeat  进行对称重复 gl.clamp_to_edge 纹理边缘值   ）处理纹理

## 视图 分三个 视点  目标点   上方向

```
对于视角  视掉和目标点都是一个点，能控制一个直线方向，在通过一个上方向就能控制一个视野方向
```

## 投影  正射投影和投射投影

## 深度检测  多边形消除  webgl已经提供

## 绘制立方体  -三维视角   使用  drawArray  可以通过drawElement来通过索引来绘制

## 光照 有三种  点光源  平行光  环境光

有光就有反射  分为 漫反射 和环境反射  其中环境光可以理解为多次反射后的  漫反射  只有 点光源和平行光的漫反射

其中最终颜色=漫反射光+环境反射光组合

### 漫反射：光照射到物体表面，最终四面八方的角度反射出去-单设光颜色 和入射光颜色 物体颜色 入射角（入射光与法线的夹角）  在任何角度看上去颜色都一样

### 平行光的漫反射 计算 =入射光颜色*物体颜色*cos  入射角的计算  法线和光线的点积可以计算   cos=光线*法线方向   法线与绘制面的顺序有关  遵循 右手准则

### 环境光的漫反射项   =环境光颜色*物体颜色

### 计算运动物体的法向量  用没有运动之前的法向量乘以 模型矩阵的逆转置矩阵就是变换之后的法向量  模型矩阵-平移缩放旋转矩阵

## 层次模型  一个物体发生有模型变化的时候，与其相关联的物体也应该随之发生变化

## initShaer  代码中的创建顶点着色器  和片元着色器

1. gl.createShader() 创建着色器对象-分为顶点着色器和片元着色器
2. 想着色器对象填充着色器源代码  shaderSource()就是字符串那些东西
3. 编译着色器   gl.complieShader()
4. 创建程序对象 gl.creageProgram()\
5. 为程序对象分配着色器程序 gl.attachShader()
6. 连接程序对象 gl.linkProgram()
7. 使用程序对象 gl.useProgram()

## 片元着色器的内置变量

1. gl_FragColor  当前片元的颜色  Vec4
2. gl_FragCoord 片元的窗口坐标  VEC4
3. gl- PointCoord 片元在绘制的点内的坐标
   
   discard 取消绘制
   
   ## 渲染到纹理

* webgl把渲染出来的结果，当做一个纹理，再把这个纹理铁道另外的图形上去
* 流程
* 1、创建帧缓冲区对象  gl.createFramebuffer()
* 2、创建纹理对象并设置 其尺寸参数 gl.ccreateTexture() gl.bindTexture() gl.textImage2D() gl.Parameteri()
* 3 创建渲染缓存区对象 gl.createRenderbuffer()
* 4、绑定渲染缓冲区对象并设置其尺寸  gl.bindRenderBuffer() gl.renderbufferStore()
* 5、将帧缓冲区的颜色关联对象指定为一个纹理 gl.frambufferTexture2D()
* 6、将帧换从区的深度关联对象指定为一个渲染缓冲区对象 gl.frmaebufferRendererbuffer()
* 7、检查帧缓冲区是否配置正确 gl.checkFrmaebufferStatus()
* 8、在帧缓冲区中进行绘制gl.bindFramebuffer()

