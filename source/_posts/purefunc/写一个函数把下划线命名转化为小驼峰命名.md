---
title: 写一个函数把下划线命名转化为小驼峰命名
tags: 算法
cover: >-
  https://timgsa.baidu.com/timg?image&quality=80&size=b9999_10000&sec=1570614180902&di=25b89f9ed3e160ab6d32dc48df0dd751&imgtype=0&src=http%3A%2F%2Fwww.1ke.co%2Ffiles%2Fcourse%2F2017%2F01-20%2F110919fc868a787658.jpg%3F4.9.3
categories:
  - purefunc
date: 2019-09-28 00:00:00
---


如：输入字符串`a_bc_de`，返回字符串`aBcDe`

### Ada
```javascript
function format (num) {
    return num.replace(/_(\w)/g, function(all, letter){
        return letter.toUpperCase();
    });
}
```

### Beck
```javascript
function underscore2upper(str) {
    let words = str.split('_');
    let newWords = words.map((element, index) => {
        return index === 0 ? element : element[0].toUpperCase() + element.substring(1, element.length)
    });
    return newWords.join('');
}
```

### Helen
```javascript
// a.找到_位置，如果_后一位为字母，大写
// b.将多余的_去除
function camelCase(str) {
    let outStr = str.replace(/_([a-zA-Z])/g, function (regValue, groupValue) {
        return groupValue.toUpperCase();
    });
    return outStr.replace(/_/g, '');
}
console.log(camelCase('_____a_bc_de__________w___'));
```

### Irene
```javascript
function test(item){
    return item.replace(/_([a-zA-Z])/g, (a, b) => b.toUpperCase())
}
```

### Mia
```javascript
function f2(str){
    return str.split("_")
        .map(function(item, i){
        if(i>0){
            return item.replace(item[0],item[0].toUpperCase());
        }else{
            return item;
        }
    }).join("");
}
f2("a_bc_de");
```

### Jack
```javascript
function toString(foo){
	var arr = foo.split('_');
	for(let i=1; i<arr.length; i++){
		arr[i]=arr[i].charAt(0).toUpperCase()+arr[i].substr(1);
	}
	return arr.join('')
}
```
