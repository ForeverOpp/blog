---
title: 安装与备份Hexo
date: 2018-02-05 20:53:29
tags:
- Hexo
- Install
- Backup
- Software
- Mac
categories: Code
---
## Forward
  About three years ago around 2015, I found I need to record something important by writting bßlog. But I hadn't money to buy VPS or Hosting, and it is too hard to do it in free hostings. So I found github(gitcafe) and Hexo.
  - What is Hexo?
  It is an fantastic program which can help people creat their static blog page easily.

  - How it works?
  It depends on Node.js, so you need to install it with nodejs, or you won't get it.

  - Why is Hexo?
  Fast, beautiful themes, easy to use, etc.

  This is a blog index page from my blog, in which you can see how beautiful it is.
  <!--more-->
  ![IndexPic][2]
  Then, if you want to know more about Hexo, you can check details in its wiki page, see [Hexo Wiki Page][1].

## Preparetion
  > - A Linux or Mac computer.(Though Windows is ok, but I don't suggest you use it, if you still go on working on it, you will have a "good" enough experience.)
  > - A github account.
  > - Be familiar with Markdown.

  Now, let's see how to install and use Hexo.

## Install Node.js
  Download Node.js from its official website [Node.js][3], and follow its guide to install it. Now you get npm installed. To test whether the npm successfully installed, you can input
  ```bash
  $ npm -v && echo $?
  ```
  Then you will see a number 0, if not, check your Node.js installation.

## Install Git
  In macOS, you just need to input command like `gcc` or `git` in terminal, then macOS will ask you if you need to download developer command tool, just choose `Yes`.
  In Linux, you can use package control system like `apt` or `yum`.
  To check if git works, input
  ```bash
  $ git -v && echo $?
  ```
  



  ---
  [1]: http://hexo.io/
  [2]: http://7xju1y.com1.z0.glb.clouddn.com/20180206001737_Me2aHU_FireShot%20Capture%201%20-%20CWind%20-%20https___i.r6up.win_.jpeg
