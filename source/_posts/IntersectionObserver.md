---
title: IntersectionObserver
date: 2023-06-26 10:55:36
tags:
cover: https://gxt-buckets.oss-cn-shanghai.aliyuncs.com/blog/filename_H128PIC%20(2).jpg
---
# 一、IntersectionObserver介绍
- ## 1.1 起源

  在现代网页开发中，动态加载和按需展示内容已成为提升用户体验和网页性能的重要手段。传统的方法通常依赖于滚动事件或定时器来监测元素与视窗的交叉状态，但这些方法效率低下且容易导致性能问题。为了解决这个问题，`W3C` 于 2016 年引入了 `IntersectionObserver API`。

  ## 1.2 IntersectionObserver 是什么？

  `IntersectionObserver`是一种浏览器提供的 `JavaScript API`，用于监测元素与视窗的交叉状态。它可以告诉开发者一个元素是否进入或离开视窗，以及两者的交叉区域的大小和位置。
   它提供了一种高效的方法来观察元素是否进入或离开视窗，而无需依赖滚动事件或定时器。它可以通过回调函数及设定的阈值来实时地通知开发者目标元素与视窗的交叉状态，并根据需要采取相应的操作。

  ## 1.3 IntersectionObserver 的特性

  - **异步执行**：`IntersectionObserver` 是异步执行的，它使用浏览器的内部优化机制，不会阻塞主线程，从而避免了性能问题。
  - **节省资源**：相比于传统的滚动事件或定时器，`IntersectionObserver` 可以精确地观察元素与视窗的交叉状态，避免了不必要的计算和回调触发，从而节省了资源的消耗。
  - **多目标观察**：`IntersectionObserver` 可以同时观察多个目标元素，通过回调函数逐个通知开发者它们的交叉状态，方便进行批量操作。
  - **自定义阈值**：开发者可以设定一个或多个阈值，用来定义元素与视窗的交叉比例。当交叉比例超过或低于阈值时，会触发相应的回调函数。

  通过使用 `IntersectionObserver`，开发者可以实现一些常见的功能，如图片懒加载、无限滚动加载、广告展示控制等，以提升网页的性能和用户体验。

  ## 1.4  IntersectionObserver的作用

  - 图片懒加载
  - 无限滚动加载
  - 广告展示控制
  - 有效曝光埋点
  - 用户兴趣埋点
  - 可视区域内外动画/视频暂停（腾讯视频列表效果）
  - 视差效果与动画
  - 标题和导航联动
  - 虚拟列表优化
  - 消息已读状态标记（各聊天软件）

  