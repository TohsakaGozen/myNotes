# map集合
### 什么是map集合：
专门用于存储多个键值对的数据
#### 如何创建：
1. new Map(); 创建一个空的map集合
2. new Map(iterator); 创建一个具有初始内容的map集合，要求每一次迭代的结果必须是一个长度为2的数组。数组的第一项表示键，第二项表示值。
```js
const falseMap=new Map([3,4,5,6,9]) //错误的参数，报错，无法对该数组进行迭代

const map=new Map([["a",3],["b",4],["c",5],["d",6],["e",9]])//正确的参数，成功创建了带有初始内容的map集合
console.log(map) //控制台打印为：Map(5){'a' => 3,'b' => 4,'c' => 5,'d' => 6,'e' => 9,}
```
#### 属性：
size:只读，表示获取当前map中键的数量

#### API：
1. set(键,值)；设置一个键值对，键和值可以是任何类型，但键不可以重复
```js
const map=new Map([["a",3],["b",4],["c",5],["d",6],["e",9]])
map.set("f",12) //键可以是任何类型，包括数字。强调：map集合中的键是不可以重复的，如果键在map中存在则会使用新的值覆盖旧的值
```
2. get(键)；根据一个键得到对应的值，如果获取一个不存在的键返回结果是undefined
```js
const map=new Map([["a",3],["b",4],["c",5],["d",6],["e",9]])
const result=map.get("a")
console.log(result) //控制台打印：3
```
3. has(键)；判断某个键是否存在
```js
const map=new Map([["a",3],["b",4],["c",5],["d",6],["e",9]])
const result1=map.has("b")
console.log(result1) //控制台打印：true
```
4. delete(键)；删除指定的键
5. clear(键)；清空一个map集合
#### 遍历
1. for...of
```js
const map=new Map([["a",3],["b",4],["c",5],["d",6],["e",9]])
for(const item of map){
	console.log(item)
}
```
2. forEach(callback(value,key,map))
```js
const map=new Map([["a",3],["b",4],["c",5],["d",6],["e",9]])
map.forEach((value,key,map)=>{
	console.log(value,key,map)
})
```

### map集合的应用
```js
//根据已给定的数组进行去重之后得到新的数组
const map=new Map([["a",3],["b",4],["c",5],["d",6],["e",9]])
const arr=[...map];
console.log(arr)
```
以上