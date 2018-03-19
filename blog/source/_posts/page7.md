---
title: 浏览器预览最大化
---
进入全屏
``` bash
var $pdfMax = $('.pdf-top')[0];
if ($pdfMax.requestFullscreen) {   // W3C
  $pdfMax.requestFullscreen();
}
else if ($pdfMax.mozRequestFullScreen) {   // FireFox
  $pdfMax.mozRequestFullScreen();
}
else if ($pdfMax.webkitRequestFullScreen) {  // Chrome
  $pdfMax.webkitRequestFullScreen();
}
else if ($pdfMax.msRequestFullscreen) {   //IE11
  $pdfMax.msRequestFullscreen();
}
```
退出全屏
``` bash
var $pdfMax = $('.pdf-top')[0];
if ($pdfMax.exitFullscreen) {
  $pdfMax.exitFullscreen();
}
else if ($pdfMax.mozCancelFullScreen) {
  $pdfMax.mozCancelFullScreen();
}
else if ($pdfMax.webkitCancelFullScreen) {
  $pdfMax.webkitCancelFullScreen();
}
else if ($pdfMax.msExitFullscreen) {
  $pdfMax.msExitFullscreen();
}
```
最大化时样式
``` bash
<!-- 当pdf-content进入全屏的时候，对.bottom的操作 -->
.pdf-content {
  &:-webkit-full-screen .bottom{ 
    display: none;
  }
  &:-moz-full-screen .bottom{
    display: none;
  }
  &:-ms-fullscreen .bottom{ 
    display: none;
  }
  &:fullscreen .bottom{ 
    display: none;
  }
}
```
