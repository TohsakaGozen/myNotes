# 字符串的常用API
## javascript 字符串函数

定义一个字符串

```javascript
var str = "Aheloworld";
```

1、获取字符串的长度 length

```javascript
var str = "Aheloworld";
console.log("str变量中字符串的长度为："+str.length)
```
2、charAt()方法可返回指定位置的字符

```javascript
var str = "Aheloworld";
var str1 = str.charAt(3)
console.log("通过charAt()方法指定下标返回字符为："+str1)
```
3、 charcodeAt() 方法可返回指定位置的字符的 Unicode 编码 语法string.charCodeAt(index)

```javascript
var str = "Aheloworld";
var str1 = str.charCodeAt(0)
console.log("通过charCodeAt()方法指定下标返回指定位置的字符的 Unicode 编码为："+str1)
```
4、fromcharcode() 可接受一个指定的 Unicode 值，然后返回一个字符串

```javascript
var str = "Aheloworld";
var str1 = String.fromCharCode(65)
console.log("fromcharcode()指定的 Unicode 值，然后返回一个字符串"+str1)
```
5、concat() 拼接字符串 可同时拼接过个字符串 作用等同于+

```javascript
var str = "Aheloworld";
var str1 = str.concat("二傻子","三傻子")
console.log("concat() 拼接字符串后的结果为："+str1)
```
6、indexOf() 方法可返回某个指定的字符串值在字符串中首次出现的位置。

如果没有找到匹配的字符串则返回 -1

```javascript
string.indexOf(searchvalue,start)
var str = "heloworld"
var str1 = str.indexOf("l");
console.log("通过indexOf()查找指定字符串第一次出现的位置的下标："+str1)

var str1 = str.indexOf("l",3);
console.log("通过indexOf()查找指定字符串规定字符串查找位置的开始地点，返回出现的位置的下标："+str1)

var str1 = str.indexOf("l");
console.log("通过indexOf()查找指定字符串如果字符串不存在，返回-1："+str1)
```
7、lastindexof() 从后往前找，下标从0往后数

```javascript
var str = "abcABCabc"
var str1 = str.lastIndexOf("a")
console.log("通过lastIndexOf()查找指定字符串最后一次出现的位置的下标【从后往前找，下标从0往后数】："+str1)
```
8、slice() 方法可提取字符串的某个部分，并以新的字符串返回被提取的部分。 不改变源数组

参数1：开始位置的索引（包含了开始位置）  
参数2：结束位置的索引（不包含结束位置）
注意：  
1- 如果省略第二个参数，则会截取后面所有的字符串  
2- 如果传递一个负数，会从后面开始计算

```javascript
var str = "abcABCabc"
var str1 = str.slice(1,4)
console.log("slice()方法提取str2字符串中 下标1开始到下标4之前结束的字符串为："+str1)
var str1 = str.slice(1,-3)// bcABC
var str1 = str.slice(0)//bcABCabc
var str1 = str.slice(-3,-1)//ab
console.log(str1)		
```
9、substring() 方法返回的子串包括 开始 处的字符，但不包括 结束 处的字符。

参数1：开始截取的索引（包含了开始位置）  
参数2：结束位置的索引（不包含结束位置）
注意：  
1- 如果传递一个负数，默认为0  
2- 如果传递的第一个参数大于第二个参数，则自动交换

```javascript
var str = "aocdefghyjklmn"
	// var str1 = str.substring(0,3)
	var str1 = str.substring(4,2)
	console.log(str1)
```
10、substr() 方法可在字符串中抽取从 开始 下标开始的指定数目的字符。  
参数1：提取字符串的起始位置 如果为负数，默认从后向前计算  
参数2：提取字符串的数量
注意：  
无论是正数还是负数 都从左向右计算

```javascript
var str = "aocdefghyjklmn"
var str1 = str.substr(2,3)
var str1 = str.substr(-3,3)
console.log(str1)
```
11、split() 方法用于把一个字符串分割成字符串数组。  
如果不指定拆分的字符，则每个字符为一个数组元素  
如果指定拆分的字符，则以指定字符拆分为数组元素
```js
var str = "aocdefghyjklmn"
var arr = str.split("")
var arr = str.split("f")
console.log(arr)

```
12、 toUpperCase() 转为大写 toLowerCase() 转为小写

```javascript
var str6 = "abcABC"
console.log("转为大写"+str6.toUpperCase())
console.log("转为小写"+str6.toLowerCase())
```
以上