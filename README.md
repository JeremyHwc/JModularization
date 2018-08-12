# JModularization
组件化开发学习记录库

## 内容概要
    （1）网络请求组件开发
    （2）App首页开发
    （3）异步图片加载模块开发
    （4）zxing二维码模块开发
    （5）视频播放SDK开发（重难点）
    （6）浏览大图功能开发
    （7）分享模块开发
    （8）搜索功能开发
    （9）推送模块开发
    （10）适配到新权限模式
    
    规划：
        每个章节开始前都会预览本章要完成的目标
        对一些难点会跟大家一起讨论一下思路
        思路理清以后进入我们真正的开发步骤
        开发完成后我们会总结本章我们必须要学会的那些东西
        
    收获：
        本次实战课程带领大家开发android原生应用
        同时带领大家完成一个sdk开发，工资及或者第三方使用
        组件化的开发思想，让你的效率高人一等
        实际开发中常用到的设计模式
        开发过程中经常用到的一些工具软件
        在实战过程中讲解我个人的开发经验，技巧，规范
        
## 第一章 首页框架的搭建
    疑问：
        （1）fragment的切换有多少种方式，有区别吗？
        （2）只要我们创建了一个activity一定要在manifest中声明吗？
        （3）activity有几种启动模式，你能熟练的知道他们各自的使用场景吗？
        （4）实际开发中，对各种文件的命名有没有什么规范？
    
        
## 第三章 App之公共模块之网络请求组件
    网络请求组件开发：
        （1）get/post请求发送及响应
        （2）支持https加密请求
        （3）封装方便使用的api，简化调用方式
        （4）后期实现文件上传/下载功能
    开发步骤：
        先利用okhttp提供的api去发送最基本的请求
    封装思路讲解：
        request(请求参数，url)，创建好请求对象
        okhttp核心（发送get/post请求，https支持，请求相关参数设置）
        callback（处理回调函数，异常处理，转发消息到我们的ui线程，将json转换对应的实体）
    基于okhttp封装我们的网络请求框架：
        cookie,exception,https,listener,request,response
    测试我们的请求组件是否好用：
    
    Charles简介：
        一款全平台的网络请求调试工具
        简单，易学，功能强大
        自动将json/xml格式化，非常适合移动端程序员
    Charles常用功能：
        http/https请求拦截，查看请求相关信息
        请求地址映射（Map）,主要用于接口调试
        请求相关参数设置，模拟慢网，超时等情况
        
## 第4章 App公共模块之图片加载组件
    本章实现功能：
        网络图片加载组件：
        （1）实现异步图片加载；
        （2）封装一个好用的图片加载组件。
        universeimageloader
        picasso/fresco/glide
        
        universeimageloader:
        （1）配置简单，使用方便
        （2）高度的可定制性
        （3）强大的图片缓存机制
        
        加载异步图片步骤：(三级缓存)
         
         Bitmap在内存缓存中--------------------------------------------------------------->
         
         图片缓存在磁盘中------------------------->
                                            Cache   Decode      Pre-process     cache       post-process    display
                                            Image   image       bitmap          bitmap      bitmap          bitmap
                                Download    On      into                        in
         图片无缓存------------>image       Disk    Bitmap                      memory
         
## 第5章 首页列表开发与测试    
    思路点拨：
        如何在ListView中使用一个二维的数据结构？
        如何让ViewPager实现无线的循环滑动？
    首页列表功能开发：
        请求我们的首页列表数据
        利用数据初始化Adapter，及各种类型item
        添加其他功能
    开发步骤：
        使用我们封装好的网络请求组件请求数据
        初始化我们的首页ListView
        
## 第6章 APP公共模块之二维码扫描组件
    二维码功能开发
    （1）添加扫码功能
    （2）自定义扫码界面
    （3）闪光灯控制
    思路点拨
        如何实现扫码功能？
        如何自定义扫码界面？
        扫码功能是否可以封装为一个组件？
    zing优势
        google的开源项目，高可定制库
        可以识别多种码，而不仅是二维码
        不依赖其他第三方库，使用起来简单
    开发步骤
        集成步骤
            导入zxing.jar包
            复制扫码所有资源到工程中
            复制扫码必须类到工程中
    必知必会
        掌握zxing中几个关键类的作用
        
## 第7章 视频播放sdk模块开发
    几个问题
        如何自定义视频播放器？
        什么是sdk，为什么要将其封装为一个sdk？
        如何统计我们的视频播放次数？
        还有很多，我们后面慢慢分析
    开发流程
        封装视频播放器
        封装业务逻辑
        对外提供API，供外界调用
    思路点拨
        如何定义一个视频播放器
        了解视频播放器声明周期吗
        自定义视频播放器有哪些坑
    三种实现方式
        （1）VideoView  简单，但丑陋，几乎没有可定制型
        （2）MediaPlayer + SufaceView 需要自己处理生命周期，复杂，可定制度高
        （3）MediaPlayer + TextureView 同第二种，还可添加动画，在ListView等复杂控件中使用
    常见的坑
        （1）非常容易加载失败
        （2）非常容易被回收
        （3）会有偶尔的黑屏现象
    核心知识串讲
        MediaPlayer视频播放核心类
        TextureView显示帧数据核心类（三种状态监听：available，change，destroy）
        众多事件接口概述（主要监听mediaplayer当前处于哪些状态）
            （1）MediaPlayer.onPreparedListener
            （2）MediaPlayer.OnErrorListener（异常捕获）
            （3）MediaPlayer.OnCompletionListener（播放完成）
            （4）MediaPlayer.OnBufferingUpdateListener（缓冲过程中调用 ）
    开发步骤
        创建我们的播放器核心类CustomVideoView
        完成我们的视频播放的生命周期方法和回调等
        处理视频的其他逻辑（返回桌面，锁屏等）
        
    实现步骤
        
        load() --加载失败处理（三次重试）--> stop();
        load() --加载成功-->onPrepared() --> pause
                                         --> resume --> onComplete --> playback()
                                                    --> onError 
    哪些业务
        根据露出屏幕百分比决定是否播放
        小屏到全屏的切换播放
        监听播放器产生的各种事件
        统计我们视频播放次数
    思路点拨
        如何计算播放器在屏幕中出现的百分比
        小屏播放到全屏播放能复用一个播放器吗
        如何监听到播放器产生的各种事件  
    开发步骤
        监听播放器产生的各种事件并实现逻辑
        完成画出屏幕暂停，划入屏幕自动播放功能
    接口回调三部曲
        （1）在B类中创建事件接口interface
        （2）在A类中implements此接口
        （3）在A类中创建B类实例时，同时为B类setListener
        
    全屏方案分析：
        （1）启动一个新的activity
            缺点：无法复用同一个播放器，所以必须加载2次
                  资源消耗较大
        （2）创建一个全屏显示的dialog
            优点：可以解决播放器复用问题且资源消耗更小
    
    核心适应点串讲
    
        （1）Dialog生命周期相关函数：onCreate(),onWindowFoucusChanged(),dismiss()
        （2）接口回调 --> 三部曲
        
    哪些接口
        必要参数的构造方法
        必要的对外功能API
    思路点拨
        创建VideoAdContext类对外提供功能
    
    视频播放SDK模块开发
        （1）MediaPlayer及其众多接口，TextureView的实践
        （2）MediaPlayer的声明周期（状态模式），外观模式，接口回调
        （3）我们的一个思维流程
            
    
         
         
         
         
         
         
         
         
         
         
         
         
