---
title: 写一个函数，实现千分位
tags: 算法
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570614180902&di=25b89f9ed3e160ab6d32dc48df0dd751&imgtype=0&src=http%3A%2F%2Fwww.1ke.co%2Ffiles%2Fcourse%2F2017%2F01-20%2F110919fc868a787658.jpg%3F4.9.3
categories:
  - purefunc
date: 2019-09-28 00:00:00
---

如：输入数字`13829364`，返回字符串`13,829,364`

### Ada
```javascript
function format(num) {
    var arr = [],
        str = num + '',
        count = str.length;

    while (count >= 3) {
        arr.unshift(str.slice(count - 3, count));
        count -= 3;
    }

    // 如果是不是3的倍数就另外追加到上去
    str.length % 3 && arr.unshift(str.slice(0, str.length % 3));

    return arr.toString();
}
```

### Beck
```javascript
function comma(num) {
    if (typeof num === 'number') {
        num = num.toString();
    }
    if (num.length < 4) {
        return num;
    } else {
        return comma(num.substring(0, num.length - 3)) + ',' + num.substring(num.length - 3, num.length);
    }
}
```

### Helen
```javascript
// a.判断字符串长度余3是否有余数
// b.如有，记录下来
// c.剩余部分分组放入数组
function dealNum(num) {
    const str = num.toString(),
        overNum = str.length % 3, // 超出长度
        overStr = overNum === 0 ? '' : str.slice(0, overNum); // 超出内容
    let dealStr = str.slice(overNum), // 分组内容
        outArr = [];

    // 分组
    for (let i = 0; i < dealStr.length; i += 3) {
        outArr.push(dealStr.substr(i, 3));
    }

    return (overStr && overStr + ',') + outArr.join(',');
}

console.log(dealNum(1234567890));
```

### Irene
```javascript
let b = '';
function thousands(number, n = 1000) {
    b = `${number % n}${b ? ',' + b : ''}`;
    return parseInt(number / n) ? thousands(parseInt(number / n), n) : b
}

console.log(thousands(13829364));
```

### Mia
```javascript
function f1(num){
    var str = num.toString();
    var count = str.length/3;//2
    var first = str.length%3;//2
    var arr = [];
    arr.push(str.substr(0,first));
    for(let i = 0;i<count;i++){
        arr.push(str.substr(first+i*3, 3));//2,3  //5,3
    }
    return arr.join(",").slice(0,-1);
}

f1(13829364);
```

### Jack
```javascript
function format(num){
    num=num+'';
    let str="";
    for(let i=num.length- 1,j=1;i>=0;i--,j++){
        if(j % 3 == 0 && i != 0){
            str+=num[i]+",";
            continue;
        }
        str += num[i];
    }
    return str.split('').reverse().join("");
}
```
