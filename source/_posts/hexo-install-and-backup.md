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
## Foreword
  About three years ago around 2015, I found I need to record something important by writting blog. But I hadn't money to buy VPS or Hosting, and it is too hard to do it in free hostings. So I found github(gitcafe) and Hexo.
  - What is Hexo?
  It is an fantastic program which can help people creat their static blog page easily.

  - How Hexo works?
  It relys on Node.js, and can generate static html pages in your local device.

  - Why is Hexo?
  Fast, beautiful themes, easy to use, etc.

  This is the home page from my blog, in which you can see how beautiful it is.
  <!--more-->
  ![IndexPic][2]
  Then, if you want to know more about Hexo, you can check details in its wiki page, see [Hexo Wiki Page][1].

## Prepare
  > - A Linux or Mac computer.(Though Windows is ok, but I don't suggest you use it, if you still go on working on it, you will have a bad enough experience.)
  > - A github account.
  > - Be familiar with Markdown.
  > - Maybe a good VPN.

  Now, let's see how to install and use Hexo.

## Install Node.js
  Download Node.js from its official website [Node.js][3], and follow its guide to install it. Now you get npm installed. To test whether the npm successfully installed, you can input
  ```bash
  $ npm -v && echo $?
  ```
  Then you will see a number 0, if not, check your Node.js installation.

## Install Git
  In macOS, you just need to input command such as `gcc` or `git` in terminal, then macOS will ask you if you need to download developer command line tools, just choose `Yes`.
  In Linux, you can use package control system like `apt` or `yum`.
  To check if git works, input
  ```bash
  $ git -v && echo $?
  ```
  Like last step of installing Node.js, you should see a number 0 now, too. If not, check [github][4] for more information.

## Install Hexo
  Just input
  ```bash
  $ npm install -g hexo-cli
  ```
  to install hexo on your system. Input
  ```bash
  $ hexo -v && echo $?
  ```
  to check if it installed successfully. For more infomation, you can go to [Hexo Wiki Page][1].

  From now on, you finished hexo installation, let's see how to use it.

## Simple Usage
  Emmm, you should creat a workspace for you blog at first.
  ```bash
  $ mkdir blog
  $ cd blog
  ```
  Unless special mention, we will use this directory by default.
  Then, initialize your blog by inputing
  ```bash
  $ hexo init
  ```
  After a while, you can get a default blog. But you need to modify `_config.yml` to customlize your blog.

  | Argument    | Description              |
  |    :-:      |            :-:           |
  | title       | Website title            |
  | subtitle    | Website subtitle         |
  | description | Use for SEO              |
  | author      | Blog author, your name   |
  | language    | Your website language    |
  | timezone    | Don't mind it            |
  | url         | Your blog url            |
  | theme       | Which theme you use      |

  > Notice: Every argument follow the syntax like this:
  ```bash
  theme: landspace
  ```
  > There is the only `SPACE` between the symbol `:` and `landspace`.

　　
  > ### Install git deployer in you blog
  > You need to install a git deployer to push your blog into github, Input
  ```bash
  $ npm install hexo-deployer-git --save
  ```
  > > Notice: You should reinstall it whenever you have a new blog.

  > Then, modify your `_config.yml` to make it avaliable. Add these content at the end of the file.
  ```bash
  deploy:
    type: git
    repo: <repository url>
    branch: [branch]
    message: [message]
  ```
  > > Notice: This file is in your blog directory.

  > | Argument    | Description                         |
  > | :-:         | :-:                                 |
  > | type        | The type of deployer, here is git   |
  > | repo        | Your git repository url, ssh or http|
  > | branch      | Repository branch, like `master`    |
  > | message     | Commit message, usually don't mind  |

  Now, you can creat you first passage by
  ```bash
  $ hexo new [layout] <title>
  ```




  [1]: http://hexo.io/
  [2]: http://7xju1y.com1.z0.glb.clouddn.com/20180206233011_0CbdUI_FireShot%20Capture%203%20-%20CWind%20-%20https___i.r6up.win_.jpeg
  [3]: http://nodejs.org/
  [4]: https://github.com
  [5]: http://
