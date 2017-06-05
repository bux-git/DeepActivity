# 重识Activity,深入Activity 系列整理
## 目录
* [**Activity生命周期**](#Activity生命周期)
* [**Android任务栈**](#Android任务栈)
* [**activity启动模式**](#activity启动模式)
* [**scheme跳转协议**](#scheme跳转协议)

#### Activity是一个负责与用户交互的组件，提供一个屏幕，用户可以用来交互为了完成某项任务	
##### Activity生命周期
  
###### 1.activity的四种状态    
	1. running 活动状态 可以与用户进行交互 处于栈顶
		
	2. paused activity失去焦点且可见 被非全屏activity覆盖 或者 透明Activity覆盖 只是失去
	   和用户交互的能力 其他成员变量等都还是存在的  只是在系统内存需要时 才有可能被销毁
		
	3. stopped activity完全被其他activity覆盖 不可见时处于stopped状态 在内存不紧张下 成员变量
	   都有可能存在，容易被系统销毁 回收
		
	4. killed 被销毁 成员变量等都已经被回收
		
###### 2.activity生命周期分析   
	Activity启动-->onCreated()(生命周期中第一个调用的方法)
		-->onStart()(可见 不可交互)
		-->onResume()（可见可交互）
					
	点击Home回到主界面(Activity不可见) -->onPause()-->onStop()
		
	再次回到Activity-->onRestart()(不可见变为可见)-->onStart()-->onResume()
		
	退出当前Activity时-->:onPause()-->onSart()-->onDestory()销毁资源等等
###### 3.android进程优先级 
    前台：处于与用户进行交互的Activity或者与前台Activity绑定的Service
    
    可见: 处于前台但是不能用户用交互的Activity
    
    服务：服务进程
    
    后台: Activity由前台转为后台 就由前台进程变味后台进程
    
    空：优先级别最低 不属于前面四种的进程 系统可以随时杀掉这个进行


    
#### Android任务栈
       先进后出
#### activity启动模式
	1.standard 标准模式 每次都重新创建Activity
	
	2.singletop 栈顶复用模式  当Activity处于栈顶时 复用此activity 其他情况则和标准模式一样
	
	3.singletask 复用模式 activity存在与任务栈中 则复用此activity 同时将此activity以上的
	  activity全部弹出栈
	  
	4.singleinstance activity独享一个任务栈
	
#### scheme跳转协议
	是一种页面跳转协议，通过定义自己的scheme协议，可以非常方便的跳转app中的各个页面;
	通过scheme协议,服务器可以定制化告诉App跳转到哪个页面
	通过通知栏消息定制化跳转页面
	通过H5页面跳转页面