# 数组的常用API
## 1.静态方法：
### 1.1 Array.from():

从类数组对象或者可迭代对象中创建一个新的数组实例
```javascript
	let set = new Set(['a', 'b', 'c', 'd'])
    let arr = Array.from(set)
    console.log(arr, arr instanceof Array);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/bafe3a90621748c0b880309683e993b2.png)

### 1.2 **Array.isArray()**：

用来判断某个变量是否是一个数组对象
```javascript
	let arr = [1, 2, 3]
    console.log(Array.isArray(arr));
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/e87202c7942240a78866930f1f2c8ed0.png)

### 1.3 **Array.of()**：

根据一组参数来创建新的数组实例，支持任意的参数数量和类型
```javascript
 	let arr3 = Array.of('开发小白', { name: 'Liderder ' })
    console.log(arr3);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/a6c09ddf18204c0aa1f034237a1a8774.png)

## 2.实例方法：

设arr为Array对象的实例对象：
```javascript
let arr = new Array()
```

### 2.1 **arr.at()**：

返回给定索引处的数组项。接受从最后一项开始倒数的负整数。
```javascript
 	let arr = [1, 5, 6, 8, 7, 9]
    console.log('arr.at(-1)', arr.at(-1));
    console.log('arr.at(1)', arr.at(1));
```

浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/e217a616d0b14e9f825d9229bba1fbce.png)

### 2.2 **arr.concat()**：

用于合并两个或多个数组。**此方法不会更改现有数组，而是返回一个新数组**
```javascript
	let arr2 = [1, 2, 3], arr3 = [4, 5, 6]
    let arr = arr2.concat(arr3, arr2)
    console.log(arr,arr2,arr3);
```

浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/9fb28e2714004d8da99c8a5c895db33f.png)

### 2.3 **arr.copyWithin()** ：

浅复制数组的一部分到同一数组中的另一个位置，并返回它，不会改变原数组的长度，但是会 **改变数原数组元素**
```javascript
	let arr = [1, 2, 3]
    arr.copyWithin(0, 1, 2)
    console.log(arr);
```

浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/08091ea40e7142bd9bca50fb487475c2.png)

### 2.4 **arr.entries()** ：

方法返回一个新的Array Iterator对象，该对象包含数组中每个索引的键/值对。
```javascript
	let arr = ['a', 'b', 'c']
    let iterator1 = arr.entries()
    console.dir(iterator1);
    console.log(iterator1.next().value);
    console.log(iterator1.next().value);
```
浏览器打印结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/097e836aeccd4600b7bf09080bc86cca.png)

### 2.5 **arr.every()** ：

方法测试一个数组内的所有元素是否都能通过某个指定函数的测试。它返回一个布尔值
```javascript
	let arr = [1, 5, 6, 8, 7, 9]
    let res = arr.every((item, index, array) => {
        return item > 1
    })
    console.log(res);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/9103dcefc5534aeea163084674b6ce6d.png)

### 2.6 **arr.fill()** ：

方法用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引  
需要注意的是：  
fill 方法接受三个参数 **value, start 以及 end**. start 和 end 参数是可选的, 其默认值分别为 0 和 this 对象的 length 属性值。  
如果 start 是个负数, 则开始索引会被自动计算成为 length+start, 其中 length 是 this 对象的 length 属性值。如果 end 是个负数, 则结束索引会被自动计算成为 length+end.。  
fill 方法故意被设计成通用方法, 该方法不要求 this 是数组对象。  
fill 方法是个可变方法, 它会改变调用它的 this 对象本身, 然后返回它, 而并不是返回一个副本。  
当一个对象被传递给 fill方法的时候, 填充数组的是这个对象的引用  
这里只介绍一下最基本的使用：
```javascript
	let arr = [1, 5, 6, 8, 7, 9]
    arr.fill(0, 1, 3)
    console.log(arr);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/119f5b8b45ae4f91baaa207eaacaf3e2.png)

### 2.7 **arr.filter()** ：

方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素。
```js
	let arr = [1, 5, 6, 8, 7, 9]
    let newArr = arr.filter((item) => {
        return item > 6
    })
    console.log(newArr);

```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/a7d475867c774aa2a5e5000f157e156d.png)

### 2.7 **arr.find()** ：

方法返回数组中满足提供的测试函数的=第一个元素的值。否则返回 undefined
```js
et arr = [1, 5, 6, 8, 7, 9]
    let res = arr.find((item) => {
        return item > 6
    })
    console.log(res);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/8fc02ec1b33e4b7daf4cf4ffe20cdb0c.png)

### 2.8 **arr.find()** ：

返回数组中满足提供的测试函数的第一个元素的索引。若没有找到对应元素则返回-1
```js
	let arr = [1, 5, 6, 8, 7, 9]
    let res = arr.findIndex((item) => {
        return item > 6
    })
    console.log(res);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/123f25592b2b4b7d9fac419fe2b94f1e.png)

### 2.9 **arr.flat()** ：

方法会按照一个可指定的深度递归遍历数组，并将所有元素与遍历到的子数组中的元素**合并为一个新数组返回**  
接收一个参数，指定要提取嵌套数组的结构深度，默认值为 1。  
**当然也可以使用Infinity，可展开任意深度的嵌套数组**
```js
	let arr = [1, 2, [3, 4, [5, 6]]]
    let newArr = arr.flat(2)
    console.log(newArr);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/dd16fe520e0c40e0a2205789cb897b8a.png)

### 2.10 **arr.flatMap()** ：

使用映射函数映射每个元素，然后将结果压缩成一个新数组

### 2.11 **arr.forEach()** ：

对数组的每个元素执行一次给定的函数
```js
	let arr = [1, 2, 3, 4, 5]
    arr.forEach((item, index, a) => {
        a[index] = item + 1
    })
    console.log(arr);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/69902bb260a74c00a79c1dce88346284.png)

### 2.12 **arr.includes()** ：

方法用来判断一个数组是否包含一个指定的值，根据情况，如果包含则返回 true，否则返回false
```js
	let arr = ['cat', 'dog', 'bat'];
    console.log(arr.includes('cat'));
    console.log(arr.includes('at'));
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/8d354c129af146f9bb2d113b538eaac2.png)

### 2.13 **arr.indexOf()** ：

方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

### 2.13 **arr.join()** ：

方法将一个数组（或一个类数组对象）的所有元素连接成一个字符串并返回这个字符串。如果数组只有一个项目，那么将返回该项目而不使用分隔符。
参数：separator 可选    
指定一个字符串来分隔数组的每个元素。如果需要，将分隔符转换为字符串。如果缺省该值，数组元素用逗号（,）分隔。如果separator是空字符串("")，则所有元素之间都没有任何字符。  
```js
	let arr = ['cat', 'dog', 'bat'];
    let newStr = arr.join('*');
    console.log(newStr);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/e4f9213622614587a720f2cf99b9751b.png)

### 2.14 **arr.keys()** ：

方法返回一个包含数组中每个索引键的Array Iterator对象。
```js
	let arr = ['cat', 'dog', 'bat'];
    let iterator = arr.keys()
    for (const key of iterator) {
        console.log(key);
    }
```
浏览器打印如下：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/6c7a53ecab6744589668f80198c0d7bf.png)

### 2.15 **arr.lastIndexOf()** ：

语法：arr.lastIndexOf(searchElement[, fromIndex])  
lastIndexOf() 方法返回指定元素（也即有效的 JavaScript 值或变量）在数组中的最后一个的索引，如果不存在则返回 -1。从数组的后面向前查找，从 fromIndex 处开始。

### 2.16 **arr.map()** ：

方法创建一个新数组，其结果是该数组中的每个元素是调用一次提供的函数后的返回值。即返回对数组中的元素进行操作之后得到的新数组
```js
	let arr = [1, 2, 3, 4, 5]
    let arr1 = arr.map((item) => item + 1)
    console.log(arr1,arr);
```
浏览器打印如下：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/b93b25b8f1f5404e8e9d5b6569220e20.png)

### 2.17 **arr.pop()** ：

从数组中删除最后一个元素，并返回该元素的值

### 2.18 **arr.push()** ：

将一个或多个元素添加到数组的末尾，并返回该数组的新长度

### 2.18 **arr.reduce()** ：

对数组中的每个元素执行一个由提供的reducer函数（升序执行），将其结果汇总为单个返回值
```js
	let arr = [1, 2, 3, 4, 5]
    let sum = arr.reduce((pre, cur) => pre + cur)
    console.log(sum);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/92f62354790840a3b817a81d37c2a2ea.png)

### 2.19 **arr.reverse()** ：

将数组中元素的位置颠倒，并返回该数组。该方法会改变原数组

### 2.20 **arr.shift()** ：

从数组中删除第一个元素，并返回该元素的值

### 2.21 **arr.slice()** ：

方法返回一个新的数组对象，这一对象是一个由 begin 和 end 决定的原数组的浅拷贝（包括 begin，不包括end）。原始数组不会被改变。
```js
	let arr = ['a', 'b', 'c', 'd', 'e']
    let arr1 = arr.slice(1, 2)
    console.log(arr1, arr);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/3a35edd5dee741088fe19d56b30af043.png)

### 2.22 **arr.some()** ：

方法测试数组中是不是至少有1个元素通过了被提供的函数测试。它返回的是一个Boolean类型的值。
```js
	let arr = ['a', 'b', 'c', 'd', 'e']
    let a = arr.some((item => item === 'b'))
    console.log(a);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/8d153a88cc3e48ee87a5e17b30d7785b.png)

### 2.23 **arr.sort()** ：

sort() 方法用原地算法对数组的元素进行排序，并返回数组。默认排序顺序是在将元素转换为字符串，然后比较它们的UTF-16代码单元值序列时构建的

由于它取决于具体实现，因此无法保证排序的时间和空间复杂性。
```js
	let arr = [1, 8, 13, 2,0]
    let a = arr.sort((a, b) => a - b)
    console.log(a);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/1f83f517b9c449beb76b8828152ff212.png)

### 2.23 **arr.splice()** ：

通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容,此方法会改变原数组。
#### 参数:
start​:  
指定修改的开始位置（从0计数）。如果超出了数组的长度，则从数组末尾开始添加内容；如果是负值，则表示从数组末位开始的第几位（从-1计数，这意味着-n是倒数第n个元素并且等价于array.length-n）；如果负数的绝对值大于数组的长度，则表示开始位置为第0位。
deleteCount(可选):  
整数，表示要移除的数组元素的个数。如果 deleteCount 大于 start 之后的元素的总数，则从 start 后面的元素都将被删除（含第 start 位）。如果 deleteCount 被省略了，或者它的值大于等于array.length - start(也就是说，如果它大于或者等于start之后的所有元素的数量)，那么start之后数组的所有元素都会被删除。如果 deleteCount 是 0 或者负数，则不移除元素。这种情况下，至少应添加一个新元素。
item1,item2....(可选):  
要添加进数组的元素,从start 位置开始。如果不传入，则 splice() 将只删除数组元素。

#### 返回值:
由被删除的元素组成的一个数组。如果只删除了一个元素，则返回只包含一个元素的数组。如果没有删除元素，则返回空数组。

```js
	let arr = [1, 8, 13, 2,0]
    arr.splice(1,2,10,10)
    console.log(arr);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/a3a3ac8698824916a8a1748b4aff862d.png)

### 2.24 **arr.toLocaleString()** ：

toLocaleString() 返回一个字符串表示数组中的元素。数组中的元素将使用各自的 toLocaleString 方法转成字符串，这些字符串将使用一个特定语言环境的字符串（例如一个逗号 “,”）隔开。

### 2.25 **arr.toString()** ：

toString() 返回一个字符串，表示指定的数组及其元素。

### 2.26 **arr.unshift()** ：

unshift() 方法将一个或多个元素添加到数组的开头，并返回该数组的新长度(该方法修改原有数组)。
```js
	let arr = [1, 8, 13, 2, 0]
    let res = arr.unshift(1, 22)
    console.log(res, arr);
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/b7a118349b5342bea207c9a076e44160.png)

### 2.27 **arr.values()** ：

values() 方法返回一个新的 Array Iterator 对象，该对象包含数组每个索引的值
```js
let array1 = ['a', 'b', 'c'];
let iterator = array1.values();
for (const value of iterator) {
  console.log(value);
}
```
浏览器打印结果：  
![在这里插入图片描述](https://img-blog.csdnimg.cn/1d48ea66953a49d1bf8dc439108f67c6.png)