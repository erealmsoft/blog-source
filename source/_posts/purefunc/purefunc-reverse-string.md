---
title: 反转一个字符串里面的大小写，其它字符不变
tags: 算法
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570614180902&di=25b89f9ed3e160ab6d32dc48df0dd751&imgtype=0&src=http%3A%2F%2Fwww.1ke.co%2Ffiles%2Fcourse%2F2017%2F01-20%2F110919fc868a787658.jpg%3F4.9.3
categories:
  - purefunc
date: 2019-09-28 00:00:00
---

如：输入字符串`aBcD`，返回字符串`AbCd`

### Ada
```javascript
//A-Z 65-90
// a-z 97-122
//A - a = 32
function parseStr (str){
    var result = '';
    for(var i= 0;i<str.length;i++){
        var temp = str.charAt(i);
        var code = temp.charCodeAt();
        if('a' <= temp && temp <= 'z'){
            temp= String.fromCharCode(code-32);
        } else if('A' <= temp && temp <= 'Z'){
            temp= String.fromCharCode(code+32);
        }

        result += temp;
    }
    return result;
}

console.log(parseStr('aBcD'))
```

### Beck
```javascript
function reverseCase(str) {
    let charCodeStr = '';
    const lowerStart = 'a';
    const upperStart = 'A'
    const diff = Math.abs(lowerStart.charCodeAt(0) - upperStart.charCodeAt(0));
    for (let index = 0; index < str.length; index++) {
        let currentChartCode = str.charCodeAt(index);
        if (currentChartCode >= 65 && currentChartCode < 91) {
            currentChartCode = currentChartCode + diff;
        } else if (currentChartCode >= 97 && currentChartCode < 123) {
            currentChartCode = currentChartCode - diff;
        }
        charCodeStr += String.fromCharCode(currentChartCode);
    }
    return charCodeStr;
}

// console.log(reverseCase('abcIasd'))
```

### Helen
```javascript
// a.先判断是大写还是小写，再做相应改变
function reverseCase(str) {
    let outStr = '';
    for (const key in str) {
        let item = str[key];
        /[a-z]/.test(item) && (outStr += item.toUpperCase());
        /[A-Z]/.test(item) && (outStr += item.toLowerCase());
        /[^a-zA-Z]/.test(item) && (outStr += item);
    }
    return outStr;
}
console.log(reverseCase('aBcDeeeeeeeEDS'));
```

### Irene
```javascript
function test(item) {
    return item
        .split('')
        .map((item, index) => item.charCodeAt(0) < 90 ? item.toLowerCase() : item.toUpperCase())
        .join('')
}
```

### Mia
```javascript
function f3(str){
    return str.split("")
        .map(function(item,i){
            var charCode = item.charCodeAt();
            console.log(i);
            if(charCode<91){
                return item.toLowerCase();
            }else{
                return item.toUpperCase();
            }
        }).join("");
}
f3("aBcD");
```

### Jack
```javascript
function changeStr(str){
    return(str.split("")
        .map(
            function (index){
                let outStr = index.charCodeAt();
                if(outStr < 91){
                    return index.toLowerCase()
                }else{
                    return index.toUpperCase()
                }
            }
        ).join("")
    )
}
```
