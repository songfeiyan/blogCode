---
title: swiper和echarts结合
---
## 问题描述
工作需要，要实现一个整屏滚动的效果，所以想用swiper。页面中嵌杂着图表，用的是echarts。要实现那种每次切换之后重新加载。但是怎么解决echarts每次切换的重新加载呢。
## 解决方案
每次切换之后将（利用swiper的onTransitionStart和onTransitionEnd）页面中echarts清空，通过js动态添加
## HTML代码
``` bash
<div class="swiper-container">
  <div class="swiper-wrapper">
    <div class="swiper-slide">slide1</div>
    <div class="swiper-slide">slide2</div>  
    <div class="swiper-slide">
      <div class="eachrt-box">
        <div id="echart-wrap">
          <div id="echart-wrap"></div>
        </div>
      </div>
    </div>
  </div>
</div>
```
## js代码
``` bash
var myChart = echarts.init(document.getElementById('echart-wrap'));
window.onload = function() {
  $('.loading').hide();
  $('.swiper-slide').eq(0).find('.hideLeft').show().addClass('fadeInLeft');
  // swiper实例
  var swiper = new Swiper('.swiper-container', {
    pagination: '.swiper-pagination',
    direction: 'vertical',
    onTransitionStart: function(swiper){
      var index = swiper.activeIndex;
      if(index < 2) {
        $('.swiper-slide').eq(index).find('.hideLeft').hide().removeClass('fadeInLeft');
      }
      if( index >= 2 ) {
        $('.swiper-slide').eq(index).find('.eachrt-box').empty();
      }
    },
    onTransitionEnd: function(swiper){
      var index = swiper.activeIndex;
      if(index < 2) {
        $('.swiper-slide').eq(index).find('.hideLeft').show().addClass('fadeInLeft');
      }
      if(index == 2){
        $('.swiper-slide').eq(index).find('.eachrt-box').append('<div id="echart-wrap"></div>');
        var myChart = echarts.init(document.getElementById('echart-wrap'));
        echartAnimate(myChart);
      }
    }
  });
}
// 第三屏echart
function echartAnimate(myChart) {
  var datas = [20, 40, 300, 25, 20];
  var data = [];
  for(let i = 0; i < datas.length; i++){
    data[i] = [0, datas[i]];
  }
  var cities = ['北京', '上海', '深圳', '广州', '苏州'];
  var barHeight = 50;

  var option = {
    grid: {
      top: 100
    },
    angleAxis: {
      type: 'category',
      data: cities,
      axisLine: {
        lineStyle: {
          color: '#666'
        }
      }
    },
    tooltip: {
      show: true,
      formatter: function (params) {
        var id = params.dataIndex;
        return cities[id] + '：' +  data[id][1] + '人';
      }
    },
    radiusAxis: {
      show: false
    },
    polar: {
    },
    series: [{
      type: 'bar',
      itemStyle: {
        normal: {
          color: 'lightBlue'
        }
      },
      data: data.map(function (d) {
        return d[0];
      }),
      coordinateSystem: 'polar',
      stack: '最大最小值',
      silent: true
    }, {
        type: 'bar',
        data: data.map(function (d) {
          return d[1] - d[0];
        }),
        itemStyle: {
          normal: {
            color: 'lightBlue'
          }
        },
        coordinateSystem: 'polar',
        name: '价格范围',
        stack: '最大最小值'
    }, {
        type: 'bar',
        itemStyle: {
          normal: {
            color: 'lightBlue'
          }
        },
        data: data.map(function (d) {
          return d[2] - barHeight;
        }),
        coordinateSystem: 'polar',
        stack: '均值',
        silent: true,
        z: 10
    }, {
        type: 'bar',
        data: data.map(function (d) {
          return barHeight * 2
        }),
        itemStyle: {
          normal: {
            color: 'lightBlue'
          }
        },
        coordinateSystem: 'polar',
        name: '均值',
        stack: '均值',
        barGap: '-100%',
        z: 10
    }],
    legend: {
        show: true,
        data: ['A', 'B', 'C']
    }
  };
  myChart.setOption(option);
}
```
