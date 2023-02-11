# set集合

### 什么是集合：
保存多个数据的数据结构  
### set：
一般用于存放不重复的数据，类似一个数组，里面的内容是不重复的  
##### 创建：  
		1. new Set() //创建一个没有任何内容的集合
		2. new Set(iterable) //创建一个具有初始内容的集合。iterable：可迭代的对象。也是一种非常简单的去重方式
##### API：
		1. add(数据)：添加一个数据到set集合的末尾
		2. has(数据)：判断set集合中是否存在对应的数据  
		3. delete(数据)：表示删除匹配的数据
		4. clear()：表示清空整个set集合
		5. 属性：size 获取set集合中元素的个数，只读属性
##### 强调：
		set集合本身也是一个可迭代对象 
		如何遍历一个set集合：
			1. for...of
			2. s.forEach((item,index,s)=>{ })
			3. 强调：set集合中不存在下标，所以forEach中前两个参数都表示set集合中的值
```
const s=new Set()
conslole.log(s);//空集合
const arr=[1,1,1,22,3,6]

const s1=new Set(arr);
s1.add("a")
s1.delete("22")
console.log(s1) //[1,3,6,"a"]

//遍历set集合
for(const item of s2){
	console.log(item);//依次输出s2中的数据
}
s2.forEach((item,index,s)=>{
	console.log(item,indexms);
})

//笔试题：根据已给定的数组进行去重之后得到新的数组
const oldarr= [1,2,3,5,5,5,66,6,6,9,9];
const s3=new Set(oldarr);
const newarr=[...oldarr]//利用展开运算符可以把set集合展开
```
### set的应用
```
//求两个数组的并集、交集、差集
const arr1=[1,2,3,4,5,6,7,8,9]
const arr2=[2,5,6,8,9,9,66,33,4,5,6,8]

//并集
const result=[...new Set(arr1.concat(arr2))];
console.log(result)

//交集
const s1=new Set(arr1)
const s2=new Set(arr2)
[...s1].filter(item=>{
	return s2.has(item)
});

const result1=[...new Set(arr1)].filter(item=>arr2.indexOf(item) >=0)

//差集
console.log("差集",[...new Set([...arr1,arr2])].filter(item=>{arr1.indexOf(item)>=0 && arr2.indexOf(item)<0 || arr.indexOf(item)>=0 && arr1.indexOf(item)<0}))

```
以上