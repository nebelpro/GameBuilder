# [GameBuilder]()

GameBuilder 是移动端轻量HTML5游戏快速开发框架，主要应用于活动推广。

## 开始之前

### 1.游戏形式活动推广页的生命周期

加载资源 --> 活动介绍 --> 游戏主体 --> 结果提示 --> 引导分享

分享进入 --> 参与结果 --> 引导参与 --> 进入游戏

### 2.

## 快速开始

**如果已经安装了 [generator-lego](https://github.com/duowan/generator-lego) ，可以直接使用 `yo lego` 命令来构建**

**或者直接 clone 到本地使用**

### 1.引入样式文件

```html
<link rel="stylesheet" href="http://assets.dwstatic.com/gamebuilder/css/gamebuilder.css">
```

### 2.引入脚本文件

```html
<body>
    ...
    <script src="http://assets.dwstatic.com/gamebuilder/js/gamebuilder.js"></script>
</body>
```

### 3.最佳实践

```html
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=0, minimum-scale=1.0, maximum-scale=1.0">
    <meta name="description" content="">
    <meta name="keywords" content="">
    <meta name="format-detection" content="telephone=no,address=no,email=no">
    <meta name="apple-mobile-web-app-capable" content="yes" />
    <meta name="screen-orientation" content="portrait">
    <meta name="x5-orientation" content="portrait">
    <meta name="full-screen" content="yes">
    <meta name="x5-fullscreen" content="true">
    <meta http-equiv="expires" content="0">
    <meta http-equiv="cache-control" content="no-cache">
    <link rel="stylesheet" href="http://assets.dwstatic.com/gamebuilder/css/gamebuilder.css">
    <title> title </title>
</head>
<body>
    <div id="preloadPage">
        <img id="loadingImg" src="http://lol.duowan.com/s/lolFaceGame/img/icon.png">
        <div id="loadingText">
            <i></i>
            <span>光速加载中...</span>
            <span id="loadingProcess">0</span>%
            </div>
    </div>
    <div class="body-page">
        <div class="game-page is-right" data-index="1" id="listPage">
            ...
        </div>
        <div class="tool-page" data-type="share" id="sharePage">
            ...
        </div>
        <div class="tool-page" data-type="wait" id="waitingPage" >
            <div class="mod-waiting">
                <div class="mod-waiting__bd">
                    <div class="mod-waiting__inner"></div>
                    <div class="mod-waiting__outer"></div>
                </div>
            </div>
        </div>    
    </div>
    <script src="http://assets.dwstatic.com/gamebuilder/js/gamebuilder.js"></script>
</body>
</html>
```

## 说明

### 推荐文件结构(游戏模板)

```
yourProj/
│
├── config.json                // 模板配置文件,必须编写,用于开发调试和上传模板时后台生成给用户编辑的选项
│
├── css/                       // 样式文件
│
├── img/                       // 图片资源
│
├── js/                        // 脚本文件
│
├── res/                       // 素材资源
│
└── index.html                 // 游戏入口
```

### 开发规范

1.界面分三种类型，资源加载界面（load-page）、主体内容界面（body-page）和消息提示界面（tool-page），主体内容分页（game-page）从`data-index="1"`开始，资源加载界面为`0`，消息提示界面不属于分页内容。

2.消息提示界面（tool-page）也有三种类型，分享页、等待页、弹出页（如结果提示，消息提示，文案提示）。

3.使用img标签加载图片资源时，`data-id`代表图片文件名，`data-type`代表图片文件格式。

4.如果是设定为可以配置内容的项，需要提供`data-set-xxx`的钩子

### gamebuilder.js使用说明

**utils工具库**

isBadAndroid - 是否低端安卓机

getTime - 返回当前时间戳

hasTransform - 是否支持transform

hasTransition - 是否支持transition

hasTouch - 是否支持触摸事件

extend(target,obj) - 用obj对象扩展target对象

each(arrays,callback) - 像$.each一样的用法

ease - 一些常用的贝塞尔曲线

**$工具库**

$()

html()

attr()

each()

show()

hide()

addClass()

hasClass()

removeClass()

siblings()

append()

on()

**配置项**

scanImg - 默认为 `true`，是否扫描img标签作为资源加载

**回调函数**

loadFinish() - 资源加载完成的处理

startEvent() - 游戏开始的处理

pauseEvent() - 游戏暂停的处理

endEvent() - 游戏结束的处理

devicemotionEvent() - 摇一摇事件触发的回调

**静态方法**

prevPage() - 主体内容分页，上一页

nextPage() - 主体内容分页，下一页

gotoPage(index) - 主体内容分页，指定`index`页

showToolPage(opts) - 打开消息提示界面

hideToolPage(opts) - 关闭消息提示界面

start() - 游戏开始

pause() - 游戏暂停

end() - 游戏结束

devicemotion() - 监听摇一摇事件

## 更新说明

* 1.0 基础版本。
* 1.1 新增gameStatus，0-游戏就绪 1-游戏开始 2-游戏暂停 3-游戏结束
* 1.2 新增start,pause,end静态方法和startEvent,pauseEvent,endEvent回调函数
* 1.3 新增devicemotion静态方法，和devicemotionEvent回调函数，用于监听摇一摇事件
* 1.4 新增popupTool配置，是否使用弹出层工具，showToolPage静态方法新增popup用法
