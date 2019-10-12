---
title: 给出两个长度相等的字符串，找出相同索引处字符值相同的字符
tags: 算法
categories:
  - purefunc
date: 2019-09-28 00:00:00
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570614180902&di=25b89f9ed3e160ab6d32dc48df0dd751&imgtype=0&src=http%3A%2F%2Fwww.1ke.co%2Ffiles%2Fcourse%2F2017%2F01-20%2F110919fc868a787658.jpg%3F4.9.3
---

如：
```javascript
function find(str1, str2) {
    // do ur logic
}
const result = find('abdiec','doaiac'); // result = ic
```

如：输入字符串`aBcD`，返回字符串`AbCd`

### Beck
```javascript
function find(str1, str2) {
    const str1Arr = str1.split('');
    const result = str1Arr.map((alpha, index) => str2[index] === alpha ? alpha : '').filter(a => a!== '');
    return result;
}

// console.log(find('abdiec','doaiac'))
```

### Helen
```javascript
function findSame(str1, str2) {
    let outStr = '',
        strLength = str1.length;
    for (let index = 0; index < strLength; index++){
        if(str1[index] === str2[index]){
            outStr += str1[index];
        }
    }
    return outStr;
}
console.log(findSame('abdiec', 'doaiac'));
```

### Irene
```javascript
function find(str1, str2) {
    let result = '';
    for (let i in str1) {
        str2.indexOf(str1[i]) === parseInt(i) ? result += str1[i] : ''
    }
    return result;
}
const result = find('abdiec', 'doaiac'); // result = ic
```

### Mia
```javascript
function find(str1, str2) {
    var str;
    return str1.split('')
        .map(function(item, i){
            if(item === str2[i]) return item;
        })
        .join("");
}
const result = find('abdiec','doaiac'); // result = ic
```

### Jack
```javascript
function findSame(str1, str2){
    str1.split("");
    let sameStr = "";
    for(let i=0; i<str1.length; i++){
        if(str1[i] === str2[i]){
            sameStr += str1[i];
        }
    }
    return sameStr;
}
```
