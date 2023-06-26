---
title: IntersectionObserver
date: 2023-06-26 10:55:36
tags:
cover: https://gxt-buckets.oss-cn-shanghai.aliyuncs.com/blog/filename_H128PIC%20(2).jpg
---
# 一、IntersectionObserver介绍
## 1.1 起源

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

# 二、工作原理

`IntersectionObserver` 的工作原理涉及到观察目标元素、目标元素与视窗的交叉区域、回调函数和阈值等方面。`MDN` 官方介绍请[移步](https://link.juejin.cn?target=https%3A%2F%2Fdeveloper.mozilla.org%2Fzh-CN%2Fdocs%2FWeb%2FAPI%2FIntersection_Observer_API)

## 2.1 观察目标元素

`IntersectionObserver` 首先需要指定要观察的目标元素。这可以通过创建一个 `IntersectionObserver` 实例，并传入一个回调函数来实现。回调函数会在目标元素的交叉状态发生变化时被调用。

## 2.2 目标元素与视窗的交叉区域

`IntersectionObserver` 会根据目标元素与视窗的交叉区域来确定它们的交叉状态。交叉区域可以分为以下几种情况：

- **进入视窗**：当目标元素的一部分进入视窗时，被称为进入视窗。
- **完全进入视窗**：当目标元素完全进入视窗时，被称为完全进入视窗。
- **离开视窗**：当目标元素完全离开视窗时，被称为离开视窗。
- **部分离开视窗**：当目标元素的一部分离开视窗时，被称为部分离开视窗。

`IntersectionObserver` 可以精确地计算目标元素与视窗的交叉区域，并根据交叉区域的变化来确定它们的交叉状态。

## 2.3 回调函数和阈值

当目标元素的交叉状态发生变化时，注册的回调函数将被触发。开发者可以在回调函数中定义相应的操作，如加载或显示元素。

此外，`IntersectionObserver` 还支持自定义阈值。阈值是一个介于 `0.0` 和 `1.0` 之间的值，用来定义目标元素与视窗的交叉比例。当交叉比例超过或低于设定的阈值时，会触发回调函数。

## 2.4 IntersectionObserver 的运行机制

`IntersectionObserver` 在内部采用了一些高效的运行机制来实现元素交叉状态的观察和回调触发。下面更详细地介绍下 `IntersectionObserver` 的运行机制。

1. **惰性计算**
    为了避免性能问题和不必要的计算，`IntersectionObserver` 采用了惰性计算的策略。它并不实时地计算目标元素与视窗的交叉状态，而是在特定时机进行计算。
    当一个目标元素进入或离开视窗的边界区域时，浏览器会通知 `IntersectionObserver` 进行交叉状态的计算。这样可以避免对所有元素进行持续的计算，从而节省了资源并提高了性能。
2. **队列处理**
    为了保证运行的平滑性，`IntersectionObserver` 使用了队列处理的机制。当目标元素的交叉状态发生变化时，会将变化的目标元素放入一个队列中。
    `IntersectionObserver` 会在下一个动画帧或微任务中处理队列中的元素。这种延迟处理的方式可以避免在一帧内频繁触发大量回调函数，从而提供更流畅的用户体验。
3. **优化算法**
    为了提高性能和减少回调触发的次数，`IntersectionObserver` 使用了一些优化算法。它会将目标元素进行分组，并按照它们在文档中的顺序进行观察。
    当观察到交叉状态变化时，`IntersectionObserver` 会将变化的目标元素放入队列中，并按照它们在文档中的顺序进行处理。这样可以确保回调函数的触发顺序与元素在文档中的顺序一致，避免出现混乱或错误的情况。

通过采用惰性计算、队列处理和优化算法，`IntersectionObserver` 实现了高效而平滑的元素交叉状态观察和回调触发，为开发者提供了一种优雅且性能优化的解决方案。

# 三、应用场景

## 3.1 图片懒加载

图片懒加载是 `IntersectionObserver` 在网页开发中常见的应用场景之一。传统情况下，网页加载时所有的图片都会同时加载，无论它们是否在视窗中可见。这会导致不必要的网络请求和资源浪费。
 通过使用 `IntersectionObserver`，可以延迟加载图片，只在它们进入视窗时才开始加载。这样可以减少初始页面加载时间，并节省带宽和资源。
 实现图片懒加载的步骤如下：

1. 创建 `IntersectionObserver` 实例，并指定观察的目标元素。
2. 在回调函数中，判断目标元素是否进入视窗。
3. 若目标元素进入视窗，将其真实的图片地址赋给元素的 `src` 属性，触发图片加载。

示例代码如下：

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      const img = entry.target;
      img.src = img.dataset.src; // 将真实的图片地址赋给 src 属性
      observer.unobserve(img); // 停止观察该图片
    }
  });
});

const lazyImages = document.querySelectorAll('.lazy-image');
lazyImages.forEach((img) => {
  observer.observe(img); // 开始观察每个图片元素
});
```

通过使用 `IntersectionObserver` 实现图片懒加载，可以显著提升页面加载性能，尤其在包含大量图片的页面中效果更为明显。

## 3.2 无限滚动加载

无限滚动加载是 `IntersectionObserver` 另一个常见的应用场景，特别适用于需要展示大量数据的页面，如社交媒体流、新闻列表等。
 传统的无限滚动加载通常基于滚动事件来触发数据加载，但这种方式在性能和用户体验上存在一些问题。而使用 `IntersectionObserver` 可以更高效地实现无限滚动加载。
 实现无限滚动加载的步骤如下：

1. 创建 `IntersectionObserver` 实例，并指定观察的目标元素，通常是页面底部的加载指示器或占位符元素。
2. 在回调函数中，判断目标元素是否进入视窗。
3. 若目标元素进入视窗，触发数据加载的操作，并更新页面内容。

示例代码如下：

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      loadMoreData(); // 触发数据加载操作
    }
  });
});

const loader = document.querySelector('.loader');
observer.observe(loader); // 开始观察加载指示器元素
```

通过使用 `IntersectionObserver` 实现无限滚动加载，可以提供更平滑和快速的加载体验。它避免了频繁的滚动事件触发，只在需要加载更多数据时才进行相应操作，减少了无效的请求和资源消耗。

vue 组件代码示例：

```js
<template>
  <div
    class="load-more-sentinel"
    v-show="sentinelEnabled"
    ref="loadMoreSentinel"
  >
    <div v-show="showLoading" class="load-more">
      <slot>
        <span v-for="i in 5" :style="`--order:${i}`" :key="`circle${i}`"></span>
      </slot>
    </div>
  </div>
</template>
<script>
import debounce from 'lodash/debounce';

export default {
  name: 'load-more',
  props: {
    sentinelEnabled: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      showLoading: false,
    };
  },
  watch: {
    sentinelEnabled: {
      handler() {
        // 因为浏览器渲染机制会在微任务执行之后执行渲染线程，之后执行宏任务，所以 setTimeout 可以保证dom已经更新
        if (!this.observer && this.$refs.loadMoreSentinel) {
          this.timer = setTimeout(() => {
            const node = this.$refs.loadMoreSentinel;
            if (node) {
              const options = {
                threshold: [0],
              };
              this.observer = new IntersectionObserver(
                debounce(this.insideViewportCb, 50),
                options
              );
              this.observer.observe(node);
            }
          }, 20);
        }
      },
      immediate: true,
    },
  },
  created() {
    this.observer = null;
    this.timer = null;
  },
  destroyed() {
    if (this.observer) this.observer.disconnect();
    if (this.timer) = clearTimeout(this.timer);
  },
  methods: {
    insideViewportCb([entry]) {
      if (this.sentinelEnabled && entry && entry.isIntersecting) {
        this.showLoading = true;
        this.$emit('load-more');
      }
    },
    finish() {
      this.showLoading = false;
    },
  },
};
</script>
<style lang="scss" scoped>
.load-more-sentinel {
  width: 100%;
  height: 15px;
  .load-more {
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    margin: 0 auto;
    margin: 8px 0;
    span {
      display: inline-block;
      width: 8px;
      height: 8px;
      margin-right: 5px;
      border-radius: 50%;
      background: $Gray8_a080;
      animation: load 1.04s ease infinite;
      animation-delay: calc(var(--order) * 0.13s);
      &:last-child {
        margin-right: 0px;
      }
    }
  }
}
@keyframes load {
  from {
    opacity: 1;
    transform: scale(1.3);
  }
  to {
    opacity: 0.2;
    transform: scale(0.3);
  }
}
</style>
```

## 3.3 广告展示控制

`IntersectionObserver` 在广告展示控制方面也有应用。传统的做法是通过滚动事件或定时器来检测广告元素是否在视窗中，并根据条件来显示或隐藏广告。
 使用 `IntersectionObserver` 可以更精确地控制广告的展示。通过观察广告元素与视窗的交叉状态，可以实现以下功能：

1. 延迟加载广告：只有当广告元素进入视窗时才开始加载广告内容，从而减少不必要的请求和资源消耗。
2. 动态展示广告：可以根据广告元素与视窗的交叉比例来决定广告的展示方式。例如，可以在广告元素完全进入视窗后才显示广告，或者在广告元素的一部分进入视窗时展示部分广告内容。
3. 预加载广告：可以在广告元素进入视窗之前提前加载广告内容，以减少展示广告的延迟时间。

示例代码如下：

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      showAd(entry.target); // 显示广告
      observer.unobserve(entry.target); // 停止观察该广告元素
    } else {
      hideAd(entry.target); // 隐藏广告
    }
  });
});

const ads = document.querySelectorAll('.ad');
ads.forEach((ad) => {
  observer.observe(ad); // 开始观察每个广告元素
});
```

通过使用 `IntersectionObserver` 来控制广告的展示，可以提高广告的可视性和用户体验。只有在广告元素真正进入视窗时才展示广告，避免了不必要的展示和资源浪费。

## 3.4 有效曝光埋点

有效曝光埋点是 `IntersectionObserver` 的另一个重要应用场景。在网页或应用中，我们常常需要追踪用户对某些元素的曝光情况，以便进行数据分析、广告计费和用户行为研究等，但如何识别曝光为**有效**的，也就是真实的出现在视口范围内，是一个难点。
 `IntersectionObserver` 提供了一个可靠且高效的方式来实现有效曝光埋点。通过观察目标元素与视窗的交叉状态，可以确定元素是否在视窗中完全或部分可见，从而进行曝光统计。

实现有效曝光埋点的步骤如下：

1. 创建 `IntersectionObserver` 实例，并指定观察的目标元素。
2. 在回调函数中，根据目标元素的交叉状态判断是否曝光。
3. 根据业务需求，记录曝光数据或触发相应的操作。

示例代码如下：

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      trackExposure(entry.target); // 记录曝光数据或触发相应操作
      observer.unobserve(entry.target); // 停止观察该目标元素
    }
  });
});

const elements = document.querySelectorAll('.exposure-element');
elements.forEach((element) => {
  observer.observe(element); // 开始观察每个目标元素
});
```

通过使用 `IntersectionObserver` 进行有效曝光埋点，可以准确地追踪用户对指定元素的曝光情况，而无需依赖滚动事件或定时器。这样可以提供更准确的数据分析和用户行为洞察。

## 3.5 用户兴趣埋点

用户兴趣埋点是一个类似有效曝光埋点的功能。通过观察用户与特定元素的交叉状态，可以获取用户对该元素的兴趣程度，从而进行个性化推荐、内容优化和用户行为分析等。 注意：兴趣埋点规则是一种定义用户对特定元素兴趣的规则。在本文中，规则是当某元素在视口停留时间达到2秒以上时，被认为用户对该元素感兴趣。 实现该规则的步骤如下：

1. 创建 `IntersectionObserver` 实例，并指定观察的目标元素。
2. 在回调函数中，根据目标元素的交叉状态判断用户对该元素的兴趣。
3. 根据规则判断适口停留时间是否满足条件。
4. 如果满足条件，则记录兴趣数据或触发相应操作。 示例代码如下：

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting &&
        entry.intersectionRatio >= 0.5 &&
        entry.intersectionRect.width >= entry.boundingClientRect.width * 0.5 &&
        entry.intersectionRect.height >= entry.boundingClientRect.height * 0.5 &&
        entry.time >= 2000
      ) {
      trackInterest(entry.target); // 记录兴趣数据或触发相应操作
    }
  });
});

const elements = document.querySelectorAll('.interest-element');
elements.forEach((element) => {
  observer.observe(element); // 开始观察每个目标元素
});
```

在上述示例中，除了判断目标元素是否交叉以外，还添加了其他条件来确保兴趣的准确性。例如，使用 `intersectionRatio` 判断元素的可见比例是否超过一定阈值，使用 `intersectionRect` 和 `boundingClientRect` 比较元素的交叉区域与元素自身的尺寸，确保元素的大部分内容都在视口中可见。
 通过将适口停留时间（`entry.time`）与2秒进行比较，可以判断用户对元素的兴趣是否达到规定的时间阈值。

充分利用 `IntersectionObserver`，开发者可以更好地了解用户的需求和行为，提供更有针对性的用户体验和增值服务。用户兴趣埋点为产品优化和业务决策提供了重要的数据，可以更精确地了解用户的兴趣和行为模式，从而提供更个性化和有价值的用户体验。

> ps: 具体的兴趣埋点规则可能因业务需求而异，以上示例仅提供了一种可能的实现方式。在实际应用中，可以根据业务需求和用户行为模式进行相应调整和定制化。

## 3.6 可视区域内外动画/视频暂停（腾讯视频 app 列表效果）

可视区域内外视频暂停也可以用 `IntersectionObserver` 实现。通过观察视频元素与视窗的交叉状态，可以控制视频的播放和暂停，以提升用户体验和优化资源消耗。

具体应用场景包括：

1. 自动播放与暂停：当视频元素完全进入视窗时，自动播放视频；当视频元素完全离开视窗时，暂停视频的播放。这样可以确保只有在用户可见的范围内才播放视频，避免不必要的资源浪费和带宽消耗。
2. 音频控制：当视频元素进入视窗时，开始播放视频的音频；当视频元素完全离开视窗时，暂停视频的音频。这样可以确保只有在用户可见的范围内才播放视频的声音，避免用户同时播放多个视频的声音干扰。
3. 视频列表优化：当网页中包含多个视频列表时，只有在用户滚动或浏览到特定视频时才播放该视频，其他视频则保持暂停状态。这样可以减少同时加载和播放多个视频对带宽和性能的压力，提升页面加载速度和用户体验。
4. 节省用户流量：当用户在移动设备上浏览网页时，可以通过 `IntersectionObserver` 监测视频元素与视窗的交叉状态，仅当视频元素进入视窗时才加载和播放视频。这样可以避免不必要的流量消耗，节省用户的数据流量。

示例代码如下：

```js
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    const video = entry.target;
    if (entry.isIntersecting) {
      video.play(); // 播放视频
    } else {
      video.pause(); // 暂停视频
    }
  });
});

const videos = document.querySelectorAll('video');
videos.forEach((video) => {
  observer.observe(video); // 开始观察每个视频元素
});
```

通过使用 `IntersectionObserver` 控制视频的播放和暂停，可以优化用户体验、减少资源消耗，提升页面性能和加载速度。

> 具体的应用场景和交互方式可能因实际需求而异。开发者可以根据自己的业务需求和用户体验目标，合理运用 `IntersectionObserver` 来实现可视区域内外视频的暂停和播放控制。

## 3.7 视差效果与动画

视差效果与动画也可以通过 `IntersectionObserver` 实现精准的控制。通过观察元素与视窗的交叉状态，可以触发或控制视差效果和动画，为网页或应用添加更丰富的交互和视觉效果。

以下是视差效果和动画的一些具体应用场景：

1. 滚动视差效果：当网页中的元素与视窗交叉时，根据滚动的位置和速度，以不同的速率和方向来移动元素，创造出立体感和深度感。例如，背景图片或图层随滚动动态移动，给用户带来视觉上的差异感和沉浸感。
2. 动态加载和过渡效果：当元素进入视窗时，根据预定义的动画效果或过渡效果，使元素以流畅和吸引人的方式进入页面。例如，图片或文本逐渐渐显现，元素从一种状态平滑过渡到另一种状态，为用户提供更优雅的页面加载和内容展示。
3. 触发动画效果：当特定元素进入视窗时，通过 `IntersectionObserver` 触发相应的动画效果，增加用户与页面的互动性。例如，当用户滚动到某个区域时，元素以动画形式弹出、旋转、渐变等，吸引用户的注意力和参与度。
4. 动态内容加载：当用户滚动到页面底部或特定区域时，通过 `IntersectionObserver` 触发动态加载更多的内容。这种技术常用于实现无限滚动列表或延迟加载，提供流畅的用户体验，避免一次性加载大量内容带来的性能问题。
5. 页面交互控制：通过观察元素与视窗的交叉状态，根据需要触发特定的交互控制。例如，当特定元素完全进入视窗时，启用按钮、链接或其他交互元素；当元素完全离开视窗时，禁用或隐藏相关元素。

## 3.8 标题和导航联动

标题和导航联动是 `IntersectionObserver` 的一种常见应用场景，通过观察元素与视窗的交叉状态，实现标题与导航之间的联动效果，提升用户导航的便利性和可视性。
 此场景**张鑫旭**大佬已经有一篇非常详细的文章，这里不做过多介绍，请[移步](https://link.juejin.cn?target=https%3A%2F%2Fwww.zhangxinxu.com%2Fwordpress%2F2020%2F12%2Fjs-intersectionobserver-nav%2F)

## 3.9 虚拟列表优化

虚拟列表中的滚动是一个重要的性能考量因素。传统的滚动监听需要在滚动事件中实时计算列表项的位置，并判断其可见性。而使用 `IntersectionObserver`，可以将交叉状态的监测交给浏览器进行异步处理，避免了频繁的计算操作，从而提高了滚动的流畅性和性能。

## 3.10 消息已读状态标记

在消息已读状态场景中，`IntersectionObserver` 可以被用于实现即时的状态追踪。
 通常，当用户滚动浏览消息列表时，我们需要确定哪些消息已经出现在可视区域内，以便标记它们为已读状态。
 通过使用`IntersectionObserver`，我们可以监测消息列表中每个消息元素与可视区域的交叉情况。一旦某个消息元素进入可视区域，我们可以触发一个回调函数来处理相应的逻辑，例如将该消息标记为已读。

以下是一个简单的示例，演示了`IntersectionObserver`在消息已读状态场景中的应用：

```js
// 创建一个 IntersectionObserver 实例
const observer = new IntersectionObserver((entries) => {
  entries.forEach((entry) => {
    if (entry.isIntersecting) {
      // 当消息元素进入可视区域时，将其标记为已读
      markMessageAsRead(entry.target);
    }
  });
});

// 获取所有消息元素
const messageElements = document.querySelectorAll('.message');

// 监测每个消息元素与可视区域的交叉情况
messageElements.forEach((messageElement) => {
  observer.observe(messageElement);
});

// 标记消息为已读的逻辑
function markMessageAsRead(messageElement) {
  // 将消息标记为已读状态，例如改变消息的样式或发送已读状态的请求
  messageElement.classList.add('read');
  // 其他处理逻辑...
}
```

在上面的代码中，我们创建了一个`IntersectionObserver`实例，并为其指定了一个回调函数。当消息元素进入可视区域时，该回调函数会被触发。然后，我们可以在回调函数中执行将消息标记为已读的逻辑。

通过将消息元素与`IntersectionObserver`进行关联，我们可以动态地监测它们与可视区域的交叉情况，无需依赖用户的滚动行为或其他事件来触发状态的更新。这种方式可以提供更即时、精确的消息已读状态更新，增强用户体验。

# 四、最佳实践

1. **选择合适的根元素**
    根据你的需求，选择合适的根元素进行监听。根元素可以是整个文档或特定的容器元素。确保选择的根元素能够包含你要监听的目标元素。

2. **优化阈值设置**
    设置合适的交叉比例阈值可以减少不必要的回调函数触发。过多的阈值设置可能会导致频繁的回调函数执行，因此需要根据具体情况进行优化。

3. **避免频繁的回调函数执行**
    由于 `IntersectionObserver` 可能在短时间内多次触发回调函数，为了避免频繁的操作或网络请求，可以使用节流（`throttling`）或防抖（`debouncing`）技术进行处理。节流可以限制回调函数的执行频率，而防抖可以在指定时间内的连续触发中只执行最后一次。

4. **优化性能与资源消耗**
    尽管 `IntersectionObserver` 可以提供更好的性能，但当处理大量元素或复杂布局时，仍需考虑性能和资源消耗。可以结合使用时间间隔、限制最大触发次数等策略，确保在合理的范围内处理交叉状态变化。

5. **控制监听范围**
    仅监听真正需要监测的元素，避免不必要的监听。过多的监听会增加性能消耗，并可能导致不必要的回调函数触发。

6. **谨慎使用多个 `IntersectionObserver`**
    当需要监测多个元素时，使用多个 `IntersectionObserver` 可能会增加代码复杂性和性能开销。在这种情况下，可以考虑合并监听逻辑，减少 `IntersectionObserver` 的数量。

7. **处理边界情况**
    注意处理边界情况，如元素尺寸变化、容器滚动等。在这些情况下，`IntersectionObserver` 可能无法及时检测到交叉状态的变化，需要进行额外的处理。

8. **考虑兼容性**
    尽管大多数现代浏览器都支持 `IntersectionObserver`，但在一些旧版本浏览器中可能不被支持。为了确保兼容性，可以使用 `IntersectionObserver` 的 `polyfill` 或提供降级方案。

9. **处理 `IntersectionObserver` 回调中的异步操作**

   9.1 取消异步操作：在某些情况下，当元素离开视窗或不再需要异步操作时，可能需要取消正在进行的异步操作。例如，当用户迅速滚动页面时，可能需要取消之前触发的异步操作，以避免不必要的网络请求或计算。可以使用适当的方法，如取消 `Promise` 或中断正在进行的异步任务。

   9.2 性能优化：对于耗时的异步操作，需要注意性能优化。考虑使用并发执行、缓存结果或其他优化策略，以减少延迟和资源消耗。

10. **清理资源**
     当不再需要 `IntersectionObserver` 监听或元素被销毁时，确保正确地清理和释放相关的资源。取消监听、解除绑定和清理回调函数，以避免内存泄漏和不必要的资源占用

# 五、React Hooks 之 useIntersection

React 传感器钩子跟踪目标元素与祖先元素或顶级文档视口的交集变化。使用[Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)并返回[IntersectionObserverEntry](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserverEntry)。

```typescript
import * as React from 'react';
import { useIntersection } from 'react-use';

const Demo = () => {
  const intersectionRef = React.useRef(null);
  const intersection = useIntersection(intersectionRef, {
    root: null,
    rootMargin: '0px',
    threshold: 1
  });

  return (
    <div ref={intersectionRef}>
      {intersection && intersection.intersectionRatio < 1
        ? 'Obscured'
        : 'Fully in view'}
    </div>
  );
};
```

