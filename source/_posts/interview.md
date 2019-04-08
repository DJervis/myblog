
---
title: 记录
categories: 原创
tags: js
abbrlink: 65015
date: 2019-04-08 14:09:36
---

1、输入时间戳/时间，输出字符串为 如：1分钟内为“刚刚”，“1小时前”，“1天前”，超过2天的则直接返回时间。
```
var getDate = function(date) {
  if(!date) return false;
  var dateTime = typeof(date) == 'object' ? date.getTime() : date;
  var nowTime = new Date().getTime();
  var day = 1000*60*60*24,
      hour = 1000*60*60,
      min = 1000*60;
  var diff = nowTime - dateTime;
  if(diff < 0) {
    return '时间大于当前时间';
  }
  var day2 = diff/(2*day),
      day1 = diff/day,
      hour1 = diff/hour,
      min1 = diff/min;
  if(day2 > 1) {
    return new Date(dateTime)
  } else if(day1 >= 1) {
    return '1天前'
  } else if(hour1 >= 1) {
    return parseInt(hour1) + '小时前'
  } else if(min1 >= 1) {
    return parseInt(min1) + '分钟前'
  } else {
    return '刚刚'
  }
}
console.log(getDate(new Date('2019/4/8 12:20:00')))
```

2、将数字转为带逗号字符串，如 1123456789.234 转为 1,123,456,789.234，用正则和非正则两种方法。
```
// slice方法
function formatNum(num) {
  var arr = (num || 0).toString().split('.');
  var result = '';
  while(arr[0].length > 3) {
    result = ',' + arr[0].slice(-3) + result;
    arr[0] = arr[0].slice(0, arr[0].length-3);
  }
  if(arr[0]) result = arr[0] + result;
  arr[0] = result;
  return arr.join('.');
}
// toLocaleString
function formatNum(num) {
  return parseFloat(num).toLocaleString()
}
// 正则表达式
function formatNum(num) {
  var arr = (num || 0).toString().split('.');
  arr[0] = arr[0].replace(/(\d)(?=(?:\d{3})+$)/g, '$1,');
  return arr.join('.')
}
```

3、