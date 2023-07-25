---
title: 一次认识NVM、Node.js、NPM、NPX
tags:
  - JavaScript
  - Development Tools
  - 扫盲
categories:
  - 前端开发
mathjax: true
abbrlink: 8c45a1bb
date: 2023-07-24 13:33:15
description: Node.js的简单说明，用于快速扫盲
---

## 介绍
在我学习前端开发的过程中，参考的教程中几乎都会提到Node.js环境安装，但我一直没有深入了解过背后的原理，只知道它们是`JavaScript`生态系统中重要的组成部分。但随着我逐渐深入软件开发，我意识了到`Node.js`模型是背后一个相当精妙的设计，只知道怎么用是远远不够的，还需要对其基本原理有一定程度的了解。

## Javascript
在正式介绍`Node.js`之前，我们先来简单回顾一下`JavaScript`的基本原理，`JavaScript`之所以能够实现与网页的交互，主要依赖于浏览器的`Document Object Model（DOM）`和`JavaScript`的事件机制。

先来说下`DOM`，`DOM`是浏览器提供的一种编程接口，当浏览器加载网页时，会将网页的`HTML`文档解析成一个`DOM`树。`DOM`树是由多个节点构成的，每个节点代表网页上的一个元素（如标签、文本等）。这样，开发者就可以使用JavaScript来获取`DOM`节点，读取或修改节点的内容、属性和样式，从而实现对网页的动态操作和交互效果。

### 代码示例
```html
<!DOCTYPE html>
<html>
<head>
  <title>JavaScript `DOM`示例</title>
</head>
<body>
  <p id="myParagraph">这是一个段落</p>

  <script>
    // 获取段落元素
    const paragraph = document.getElementById('myParagraph');

    // 修改段落内容
    paragraph.textContent = '这是修改后的内容';
  </script>
</body>
</html>
```

`JavaScript`的事件机制的则是基于浏览器的`Event Loop（事件循环）`和事件监听器。当用户触发一个事件，浏览器会将该事件添加到事件队列中。然后，`JavaScript`引擎会不断检查事件队列，一旦发现事件队列中有事件，就会将该事件取出，并执行对应的事件监听器。这样，就实现了对用户交互行为的实时响应。
### 代码示例
```html
<!DOCTYPE html>
<html>
<head>
  <title>JavaScript事件示例</title>
</head>
<body>
  <button id="myButton">点击我</button>

  <script>
    // 获取按钮元素
    const button = document.getElementById('myButton');

    // 添加事件监听器
    button.addEventListener('click', function() {
      alert('按钮被点击了！');
    });
  </script>
</body>
</html>
```

## Node.js：JavaScript的后端奇迹
看到这里，不难发现`JavaScript`本质上就是浏览器内核的附庸，没有浏览器作为解释器，`JavaScript`啥也不是。

而这一情况直到`Node.js`的出现才得以转变，`Node.js`是一个基于`Chrome V8`引擎的`JavaScript`运行时环境，通过`V8`引擎，可以将`JavaScript`代码解释和执行为机器代码，这使得`JavaScript`在服务端也能够进行文件的读写等操作，这使得`JavaScript`在服务端也能够进行文件的读写，此外`Node.js`还支持数据库连接、并发处理请求、模块化开发以及项目打包和构建等高级功能。这里就不再赘述了。

当然，即使不使用`Node.js`，我们依然可以考虑使用其他服务器端脚本语言来实现相同的功能，例如`PHP`，只是这样会涉及到不同语言的切换和学习成本，并且需要额外的配置和处理。不过这也不意味着`Node.js`就是十全十美，`Node.js`自身也存在回调地狱和缺乏一致性的问题，选择使用哪种后端技术还需要综合项目的需求、团队的技术栈和开发者的偏好来考虑。

## npm：JavaScript包管理利器
程序开发中我们常常需要依赖别人提供的框架，写js也不例外。这些可以重复的框架代码被称作`包(package)`或者`模块(module)`，一个包可以是一个文件夹里放着几个文件，同时有一个叫做 `package.json`的文件。

一个网站里通常有几十甚至上百个`package`，分散在各处，通常会将这些包按照各自的功能进行划分（类似安卓开发中的划分子模块)，但是如果重复造一些轮子，不如上传到一个公共平台，让更多的人一起使用、参与这个特定功能的模块。而`npm`的作用就是让我们发布、下载一些JS轮子更加方便。

## nvm：多版本Node.js管理利器
在开发中，有时候对`node`的版本有要求，有时候需要切换到指定的`node`版本来重现问题等。遇到这种需求的时候，我们需要能够灵活的切换`node`版本，`nvm`就是为解决这个问题而产生的，他可以方便的在同一台设备上进行多个`node`版本之间切换。

## npx：临时运行依赖包命令
随着`npm`的发展，很多第三方包提供了一些非常有用的命令行工具。传统上，我们需要全局安装这些包，然后才能使用这些命令行工具。然而，全局安装有时会带来一些问题，比如版本冲突、权限问题等。

`npm` v5.2.0引入了`npx`命令，它为解决这个问题而产生。`npx`命令可以帮助我们执行依赖包内的二进制文件，无需全局安装。它会在执行前检查依赖包是否存在，如果不存在会临时下载依赖包，并执行其中的命令行工具。

通过`npx`命令，我们可以把原来需要全局安装的包放到项目目录下安装，解决了全局安装带来的问题，同时提升了使用包内命令行工具的体验。