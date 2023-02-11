# Promise的基本使用

#### 如何使用：
```
var pro = new Promise(resolve,reject)=>{
	//未决阶段的处理
	//通过调用reslove函数将promise推向已决阶段的resolve状态
	//通过调用reject函数将Promise推向已决阶段的reject状态
	//resolve和reject均可以传递一个参数
	}
	pro.then(data=>{
	//这是一个then函数，如果当前的Promise已经是resolve状态
	//data未状态数据
	},err=>{
	//这是catch函数，如果当前的Promise已经是reject状态
	//err未状态数据
	});
```


```
const pro = new Promise((resolve,reject)=>{
	console.log("进行未决处理");
	setTimeout(()=>{
		if(Math.random()<0.5){
			resolve("转变为成功的已决状态")
		}else{
			reject("转变为失败的已决状态")
		}
	},1000)
})
pro.then(data => {
            console.log(data)
        }, error => {
            console.log(error)
        })
```
![[Pasted image 20230117160522.png]]
![[Pasted image 20230117160451.png]]
强调：Promise不是为了消除回调，而是让回调变得可控。
细节：
1. 未决阶段的处理是同步的，会立即执行
2. then和catch函数是异步的，就算是立即执行，也会加入到事件队列中等待执行，并且加入的队列是微队列
3. `pro.then()`可以只添加thenable函数，`pro.catch()`可以单独添加catchable函数
4. 在未决阶段的处理函数中，如果发生未捕获的错误，会自动将状态推向rejected并且被catchable捕获
5. 一旦推向已决状态，无法再对状态做任何更改

#### Promise的串联：
当后续的Promise需要用到之前的Promise的处理结果。
	无论then()/catch()，都有返回值，返回一个新的Promise对象
	then():返回的对象的状态：
		1. 如果当前的Promise是挂起状态，则得到的新的Promise也是挂起状态
		2. 如果当前的Promise是已决状态，则运行相应的后续处理函数，并将后续的处理函数的结果作为resolved状态的数据，应用到新的Promise中
		3. 如果后续的处理函数发生错误，则将返回值作为rejected状态的数据应用到新的Promise当中
```
  let snackPromise = function (snackName) {

            return new Promise((resolve, reject) => {

                console.log(`商家准备${snackName}中`)

                let alertFood = {

                    foodName: snackName

                }

                return resolve(`${alertFood.foodName}`)

                console.log(`商家已完成${snackName}`)

            })

        }

        snackPromise("烤冷面").then(data => {

            console.log("你吃到了" + data)

            return snackPromise("臭豆腐")

        }).then(data => {

            console.log("你吃到了" + data)

        })
```
	强调：后续的Promise一定要等到前一个Promise执行完成才会变成已决状态

#### Promise的其它api
 原型成员:
		then()
		catch()
		finally()：注册一个后续处理函数，当Promise为已决状态时运行该函数，只要是已决状态，无论是成功还是失败一
		定执行
		例子：
```
        new Promise(function (resolve, reject) {
            setTimeout(() => {
                let i = Math.random()
                if (i < 0.5) {
                    resolve(`成功了,i=${i}`)
                } else {
                    reject(`失败了,i=${i}`)
                }
            }, 1000)
        }).then(data => {
            console.log(data)
        }).catch(error => {
            console.log(error)
        }).finally(() => {
            console.log(`Promise已执行`)
        })
```
实例成员：
	resolve(data):
	reject(err):
	all(iterable):返回一个新的Promise对象，iterable：数组，每一项都是一个Promise对象，只有当iterable当中的所有对象都执行成功才会触发整体成功，一旦有任何一个对象失败，则整体返回失败
	race(iterable):iterable当中的任意一个Promise被执行成功或失败后，父Promise马上也会用子Promise的成功或者失败结果作为参数调用父Promise绑定响应的结果，返回该Promise对象
```
let MeiShaoJiu = function (name, tell) {
            let p = new Promise((resolve, reject) => {
                if (Math.random() < 0.5) {
                    resolve(`吾名${name}，${tell}`)
                } else {
                    reject(`${name}酱魔力不够啦！`)
                }
            })
            return p
        }
  
        let Megumin = MeiShaoJiu("Megumin", `以大魔法师为业，操纵最强攻击魔法，爆裂魔法，乃终将穷极爆裂魔法之人·····！`)
        let Yunyun = MeiShaoJiu("Yunyun", `操纵上级魔法！！红魔族第一的大魔法师！！乃终将成为红魔族族长之人！！！`)
        let Rikka = MeiShaoJiu(`Rikka`, `爆裂吧，现实！粉碎吧，精神！Banishiment this world!`)
  
        Promise.all([Megumin, Yunyun, Rikka]).then((data) => {
            console.log(data)
        }).catch(err => {
            console.log(err)
        })

        Promise.race([Megumin, Yunyun, Rikka]).then(data => {
            console.log(data)
        }).catch((err) => {
            console.log(err)
        })
```

#### async和await
async关键字：简化函数在返回值中对Promise的创建 异步的
	将该关键字放置再函数的开始位置，则被修饰的函数返回的结果一定是一个Promise对象
await关键字：等待
	特点：必须要出现在async函数中，用在某个表达式前边，如果该表达式是Promise得到的