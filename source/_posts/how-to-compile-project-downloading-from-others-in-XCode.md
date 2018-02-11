---
title: 在XCode中编译下载的项目
date: 2018-02-10 23:59:14
tags:
- Swift
- Complie
- Mac
categories: Code
---
## Foreword
  Sometimes, we need to compile others' program, but to the people who didn't know Swift or Objective-C at all, compiling other people's program is so difficult to do. So this passage will tell you how to compile existed project in XCode.

<!--more-->

## Contents
  > - [Prepare](#Prepare)
  >   - [Carthage](#Carthage)
  >   - [CocoaPods](#CocoaPods)
  > - [Compile](#Compile)
  >   - [Clone Project](#Clone-Project)

## Prepare
  There are two ways to install project's dependency, so judge it from project files.

  You may saw some projects tree like this: ![1]
  Look at the last two files, they start by `Cartfile`. You need to process these project in the step [Carthage](#Carthage).

  Or you saw others are like this: ![2]
  You can see `Podfile` in this project, to complie this kind of projects, see step [CocoaPods](#CocoaPods).



[1]: http://7xju1y.com1.z0.glb.clouddn.com/20180211174925_tGxhbb_WX20180211-174714.jpeg
[2]: http://7xju1y.com1.z0.glb.clouddn.com/20180211174925_HuybqP_WX20180211-174907.jpeg
