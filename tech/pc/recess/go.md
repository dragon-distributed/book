
# 工程准备

```
# First, clone the repo via git:
git clone --depth=1 https://github.com/electron-react-boilerplate/electron-react-boilerplate.git recess

cd recess

# remove git info, in order to commit to your git hub
rm -rf .git

# git init
git init
git status
git add *
git commit -m "init"
git remote add origin https://github.com/dragon-distributed/recess.git
git push -u origin master


#安装nodejs, npm, yarn

1 进https://nodejs.org/en/，安装nodejs，已包含npm

检查:  
npm -v
node -v

2 yarn 
https://yarnpkg.com/zh-Hans/docs/install#mac-stable
MAC: brew install yarn 或 sudo port install yarn
Windows: 下载安装即可

```

# vs code 准备

```
https://code.visualstudio.com

安装插件

https://electron-react-boilerplate.js.org/docs/editor-configuration

code --install-extension dbaeumer.vscode-eslint
code --install-extension dzannotti.vscode-babel-coloring
code --install-extension EditorConfig.EditorConfig
code --install-extension flowtype.flow-for-vscode

不知道怎么做，就可以在
code->首选项->extensions，
搜索dbaeumer.vscode-eslint，dzannotti.vscode-babel-coloring等等

其它建议插件
css-in-js
Git supercharged


```


# 遮掩的窗口

## components

```
安装material-ui, 
1. 在package.json，在dependencies中，添加material-ui/core，提一下，这里的^是指大于这个版本都行。@不是什么特殊符号，只是包是这个命名。
"@material-ui/core": "^4.8.0",

yarn install
```

第一个 relax 的主页
```
创建index.js，然后写代码
先讲讲布局: flex
然后写style，写div布局。

然后写timer控件

所以主要知识点： 
1. flex
2. react
3. with style
4. constructor, did amount顺序等
5. PropTypes
6. rgba与opacity区别
```

第二个 timer 控件
```
编写控件

主要是这个控件需要实例倒数，以前可以用getElementById('id').innerText来修改，现在可以使用控件思想

说明一下可以用setValue的方式进行

所以主要知识点：
1. 控件思想
2. setTimeOut
3. 组件内的setState
4. 如何通知外部, 从index传递function过来
5. 为什么要用内部的state
```

第三个 button 控件

```
主要知识点
1. 如果在组件内enable button，并且不依耐全局state
2. 在外部调用组件内的enable function
3. 点击button关闭窗口，注意，这个方法应该是在container里面提供的，因为这是对外部的反应
4. botton 点击关闭主窗口
```

## containers

```
编写Relax.js

知识点:
1. connect
2. mapStateToProps
3. mapDispatchToProps
4. config.js
```

## 删除原有css

```
删除原有app.global.css里面的无关内容
```

## main windows

```
1. no frame, main.dev.js. main windows add: frame: false,
2. fullscreen, simpleFullScreen
3. opacity
4. alway on top关键点
```


# Tray(图标)

## tray放入
```
利用boilerplate工程中的resource

icon size: 
mac https://iconhandbook.co.uk/reference/chart/osx/

暂时用24*24, 

知识点：
1. 2x图标 
2. appTray回收的问题
```

## tray 菜单

```
1. tray_menu的编写
2. open windows, 
3. separator
4. full screen的坑，要在close事件中设回full screan=false,不然一点图标就会全屏
```

# setting

```
问题1. 工程中的app.html与index.js是定位在relax windows的，如何处理？复制一份还是？
-> 
1. share global variables, 
2. set title.
3. UI.
4. 保存,使用electron-store
5. 改写config类
6. 改写setting页面
7. 处理start at login
```

# 定时relax

```
1. 主进程的relax_timer编写
2. 打开窗口时stop，关闭时start
3. 每次都要重启relax
```



# 优化

## 自定义菜单

```
1. menubar
2. 编写菜单，先不管事件
   先讲功能，想做到什么
   讲讲如何设置，因为menu有倒数，main process也有倒数
   再讲讲如何避免slider的变动
1. ipc处理
2. Main process发送到manu web content的办法
3. config在两个process中，如果做内存缓存，会失效
4. 加速打开: preloadWindow: true
```

## notification

```
1. 添加notification
```

## 多屏幕

## 图标

## 动态 tray

```
1. 引入chartjs
2. 写chartjs脚本
3. 处理webPreferences中的backgroundThrottling，然后window.hide之后,canvas不刷新
```

## 喝水

```
1. material-ui, css: &:hover, 基css
2. 外部react体系
```


# 打包 

```
1. 修改package.json，修改名字,包括最开始，还有build属性，author属性等
2. mac下需要 CSC_IDENTITY_AUTO_DISCOVERY=false yarn package
3. 
```



# windows

```
1 window-all-closed 在windows下需要注释
添加
app.on('window-all-closed', e => e.preventDefault());



```








# book structure

1. 介绍自己，以及课程、工程等
2. js历史, v8引擎(js以前写前台，表单验证等)
3. electron介绍以及原理
4. 开发准备
5. 最简单的demo
6. 介绍主进程
7. 主进程demo
8. 介绍渲染线程
9. 渲染线程demo
10. 介绍react + matrial ui
11. 实践，实际例子
12. 