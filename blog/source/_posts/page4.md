---
title: 移动端无缝滚动
---
## 问题描述
前一段时间项目里需要写移动端的无缝滚动，在这里保存下~
## HTML代码
``` bash
<div class="scroll-txt">
  <ul class="font-inner">
    <li>滚动内容滚动内容</li>
    <li>滚动内容滚动内容</li>
    <li>滚动内容滚动内容</li>
  </ul>
</div>
```
## css代码
``` bash
<style>
   *{ padding: 0;margin: 0;}
    a{text-decoration:none; color:inherit;}
    ul{margin:0; padding:0;}
    ul li{list-style:none;}
    .scroll-txt{width:350px; height:60px; border:1px solid #ccc; color:#484848; position:relative;  overflow:hidden; box-sizing: border-box;}
    .scroll-txt .font-inner{position:absolute; left:8px; top:0;}
    .scroll-txt .font-inner li{height:30px; line-height:30px;}
    .scroll-txt a:hover{color:#0C6796;}
  </style>
```
## js代码
``` bash
<script>
    $(function(){
      var index = 0;

      var oInner = $(".font-inner");
      var oLi = $(".font-inner li");

      //克隆前两个放到最后（实现无缝）
      oLi.eq(0).clone(true).appendTo(oInner);
      oLi.eq(1).clone(true).appendTo(oInner);

      var liHeight = $(".scroll-txt").height();//获取视口的高度
      var totalHeight = (oLi.length * oLi.eq(0).height());//获取li的总高度

      //给ul赋值高度
      oInner.height(totalHeight);

      function tab(){
        oInner.animate({
          top: -index * oLi.eq(0).height()
        },400,function(){
          if(index == oLi.length) {
            oInner.css({top: 0});
            index = 0;
          }
        })
      }
      function next() {
        index++;
        if(index > oLi.length) {
          index = 0;
        }
        tab();
      }
      //自动轮播
      var autoTimer = setInterval(next,2000);
    });
  </script>
```
More info: 该方法适用于jquery和zepto，如果遇到不兼容zepto，在zepto下面追加fx.js的代码即可