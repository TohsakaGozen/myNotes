# 数组的新增API
## 数组新增API：
1. Array.of(...args);
```
//根据指定的数组项创建数组
const arr=Array.of(1,2,3,4,6,7);
console.log(arr) //控制台打印：(6)[1,2,3,4,6,7]
```
2. Array.from(arg);
```
//通过给定的类数组或者可迭代的对象创建一个新的数组
const div=document.querySelectorAll("div")
console.log(div) //控制台打印：NodeList(10)[div,div,div,div,div,div,div,div,div,div]
Array.prototype.slice.call(div,0);//老方法将类数组对象进行转换为数组
const result = Array.from(div)//新方法将类数组对象进行转换为数组
console.log(resulet) //控制台打印：(10)[div,div,div,div,div,div,div,div,div,div]
```
3. find(callback());
```
//用来查找满足条件的第一个元素，依次判读数组中的每一项是否满足要求，返回满足要求的内容

const arr=[
	{name:"tohsaka",id:1},
	{name:"gozen",id:2},
	{name:"rill",id:3},
	{name:"sill",id:4},
	{name:"alice",id:5},
]
//求数组中id为5的name
const result = arr.find(item=>{
	if(item.id==5){
		return true
	}else{
		return false
	}
})

console.log(result);//控制台打印：{name:"alice",id:5}
```
4. findIndex(callback());
```
//用来查找满足条件的第一个元素，依次判读数组中的每一项是否满足要求，返回满足要求的下标,如果没找到返回-1

const result= arr.findIndex(item=>{
	return item.id==5
})
```
5. fill(data)
```
//用指定的数据充满数组的所有内容

const arr=new Array(3);
arr.fill("数组的每一项都是我")
console.log(arr) //控制台打印：["数组的每一项都是我","数组的每一项都是我","数组的每一项都是我",]
```
6. copyWithin(target,start,end);
```
//在数组内部完成复制
const arr=[2,4,6,78,20]
//从4开始之后用前面的替换后面的
arr.copyWithin(2)
console.log(arr) //控制台打印：[2,4,2,4,6,78,20]
```
7. includes(data);
```
//判断数组是否包含某个值
const arr = [11,22,33,44,55,66,77,88,99];
console.log(arr.idnexOf(55));//返回的下标,控制台打印：4     
console.log(arr.includes(55));//控制台打印: true
```

以上