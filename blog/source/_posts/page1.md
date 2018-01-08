---
title: iframe不能初始化高度
---
## 问题描述
管理系统通过左边导航栏点击，然后在右边的iframe标签下打开新的页面。但是iframe不能自动伸缩高度，如果给iframe设置默认高度，当iframe内容过高，则iframe会出现滚动条。加上浏览器的滚动条，就会出现双滚动条的问题（真的丑爆了）。有在网上看了一些给iframe设置高度的方法，思路是在父页面给iframe的onload事件并没有动态修改高度。但是并不适用我遇到的bug。
## 解决方案
在子页面动态修改父页面里面的iframe的高度
## 代码如下
``` bash
<script>
  function resize() {
    var ifm = window.parent.document.getElementsByTagName('iframe')[0];
    var h = ifm.contentWindow.document.body.scrollHeight;
    ifm.style.height = h + 'px';
  }
  window.onload = function(){
    resize();
  }
</script>
```

More info: 该方法是在子页面里执行的。只要子页面内容有改变了，就要重新调取该方法，重新计算iframe的高度