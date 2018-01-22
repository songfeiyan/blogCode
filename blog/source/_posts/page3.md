---
title: js倒计时代码
---
## 问题描述
前一段时间项目里需要写倒计时代码，在这里保存下~
## HTML代码
``` bash
<div>
  <span class="tt">00</span>天
  <span class="tt">00</span>时
  <span class="tt">00</span>分
  <span class="tt">00</span>秒
</div>
```
## js代码
``` bash
<script>
    var deadline = "2018-01-15 15:00";
    var times = {
        deadline: deadline,
        timeDiff:function(){
            var star = new Date();
            var end  = new Date(this.deadline);
            var timediff = end.getTime()-star.getTime();
            timediff = parseInt(timediff/1000);
            return timediff;
        },
        countdown:function(){
            var intDiff = this.timeDiff();
            setInterval(function(){
              var day=0, hour=0, minute=0, second=0;
              var dayStr, hourStr, minuteStr, secondStr;
              if(intDiff > 0){
                  day = Math.floor(intDiff / (60 * 60 * 24));
                  hour = Math.floor(intDiff / (60 * 60)) - (day * 24);
                  minute = Math.floor(intDiff / 60) - (day * 24 * 60) - (hour * 60);
                  second = Math.floor(intDiff) - (day * 24 * 60 * 60) - (hour * 60 * 60) - (minute * 60);
              }
              // if (day <= 9) day = '0' + day;
              // if (hour <= 9) hour = '0' + hour;
              // if (minute <= 9) minute = '0' + minute;
              // if (second <= 9) second = '0' + second;
              if (day < 10) {
                dayStr = '<span>0</span><span>'+ day +'</span>';
              }
              else {
                dayStr = '<span>'+ day +'</span>';
              }
              if (hour < 10) {
                hourStr = '<span>0</span><span>'+ hour +'</span>';
              }
              else {
                hourStr = '<span>'+ hour +'</span>';
              }
              if (minute < 10) {
                minuteStr = '<span>0</span><span>'+ minute +'</span>';
              }
              else {
                minuteStr = '<span>'+ minute +'</span>';
              }
              if (second < 10) {
                secondStr = '<span>0</span><span>'+ second +'</span>';
              }
              else {
                secondStr = '<span>'+ second +'</span>';
              }
              $('.tt').eq(0).html(dayStr);
              $('.tt').eq(1).html(hourStr);
              $('.tt').eq(2).html(minuteStr);
              $('.tt').eq(3).html(secondStr);
              intDiff--;
            }, 1000);
        }
    }
    times.countdown();
  </script>
```