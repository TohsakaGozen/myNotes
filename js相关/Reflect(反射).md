# Reflect(反射)
## Reflect（反射）是什么：
js的内置对象
### 内置API：
1. Reflect.set(target,propertyKey,value)；设置对象target的属性propertyKey的值为value，等同于给对象的属性赋值
```
const obj={}
Reflect.set(obj,"name","kiven");
console.log(obj) //控制台打印:{name:'Kiven'}
```
2. Reflect.get(target,propertyKey)；读取对象target的属性propertyKey的值，等同于直接读取对象的属性值
3. Reflect.apply(target,thisArgument,argumentsList)；调用一个指定的函数，并绑定this和参数列表，等同于函数调用
4. Reflect.deleteProperty(target,propertyKey)；删除一个对象的属性
5. Reflect.defineProperty(target,propertyKey,attributes)；类似与Object.defineProperty，不同的是如果配置出现问题，返回false而不是报错
6. Reflect.construct(target,argumentsList)；用构造函数的方式创建一个对象
7. Reflect.has(target,propertyKey)；判断一个对象中是否存在propertyKey属性
8. 其他的API:https://developer.mozilla.org/zh-CN/docs/web/JavaScript/Reference/Global_Objects/Reflect