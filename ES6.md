  ## 1、ES6

### 1）基本语法

#### （1）let 声明变量

1. 不能重复声明，防止命名污染
2. 块级作用域，但不影响作用域链

```javascript
{
    let school = 'Halo';
    function fn(){
        console.log(school);
    }
    fn();
}
```

3. 不存在变量提升

#### （2）const 声明常量

1. 必须赋初始值
2. 命名使用全大写
3. 块级作用域
4. 修改数组或者对象的元素, 不会报错

```javascript
	const TEAM = ['UZI','MXLG','Ming','Letme'];
	TEAM.push('Meiko');
```

#### （3）模板字符串

1. 内容中可以直接出现换行符

   ```javascript
   	let str = `<ul>
                <li>沈腾</li>
                <li>艾伦</li>
                </ul>`;
   ```

2. 变量拼接

   ```javascript
   		let lovest = '魏翔';
           let out = `${lovest}是我心目中最搞笑的演员!!`;
           console.log(out);
   ```

#### （4）变量解构赋值

- ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构赋值。

##### 【1】数组的解构赋值

	//数组的解构赋值
	const arr = ['张学友', '刘德华', '黎明', '郭富城'];
	let [zhang, liu, li, guo] = arr;
	console.log(zhang)		// 张学友

##### 【2】对象的解构赋值

     	//对象的解构赋值
            const zhao = {
                name: '赵本山',
                age: '不详',
                xiaopin: function(){
                    console.log("我可以演小品");
                }
            };
            
    	let {name, age, xiaopin} = zhao;
        console.log(name);
        console.log(age);
        console.log(xiaopin);
        xiaopin();

#### （5）箭头函数

##### 【1】基本语法

- 编写规范

```javascript
let fn = (a , b) => {
    return a + b ;
}
```

- this 是静态的，this 始终指向函数声明时所在作用域下的 this 的值

- 不能作为构造实例化对象

##### 【2】简写

- 省略小括号, 当形参有且只有一个的时候

```javascript
	 let add = n => {
                return n + n;
            }
```

- 省略花括号, 当代码体只有一条语句的时候, 此时 return 必须省略，而且语句的执行结果就是函数的返回值。

```javascript
	let pow = n => n * n;
```

##### 【3】应用场景

- 箭头函数适合与 this 无关的回调. 定时器, 数组的方法回调
- 箭头函数不适合与 this 有关的回调. 事件回调, 对象的方法

```javascript
 		// 从数组中返回偶数的元素
		const arr = [1,6,9,10,100,25];

        const result = arr.filter(function(item){
            if(item % 2 === 0){
                return true;
            }else{
                return false;
            }
        });
        
        const result = arr.filter(item => item % 2 === 0);
```

#### （6）参数默认值

- 形参初始值，具有默认值的参数，位置靠后。

```javascript
function add(a,b,c = 10) {
    return a + b + c;
}
```

#### （7）rest 参数

1. 用于获取函数的实参，用来代替 arguments，rest 参数必须要放到参数最后。

   ```javascript
       function fn(a,b,...args){
           console.log(a);
           console.log(b);
           console.log(args);
       }
       fn(1,2,3,4,5,6);
   ```

2. 应用于对象

   ```javascript
    		function connect({host, port, ...user}){
               console.log(host);
               console.log(port);
               console.log(user);
           }
   
           connect({
               host: '127.0.0.1',
               port: 3306,
               username: 'root',
               password: 'root',
               type: 'master'
           });
   ```

#### （8）扩展运算符

- 『 . . . 』 扩展运算符能将==『数组』或者 { 对象 }== 转换为逗号分隔的『参数序列』

1. 数组的合并

   ```javascript
    		const kuaizi = ['王太利','肖央'];
           const fenghuang = ['曾毅','玲花'];
           const zuixuanxiaopingguo = [...kuaizi, ...fenghuang];
           console.log(zuixuanxiaopingguo);
   ```

2. 数组的克隆，元素含有引用类型则为浅拷贝

   ```javascript
           const sanzhihua = ['E','G','M'];
           const sanyecao = [...sanzhihua];//  ['E','G','M']
           console.log(sanyecao);
   ```

3. 将伪数组转为真正的数组

   ```javascript
   		const divs = document.querySelectorAll('div');
           const divArr = [...divs];
           console.log(divArr);
   ```

4. 对象合并

   ```javascript
           //对象合并
           const skillOne = {
               q: '天音波'
           }
           const skillTwo = {
               w: '金钟罩'
           }
           const skillThree = {
               e: '天雷破'
           }
           const skillFour = {
               r: '猛龙摆尾'
           }
   
           const mangseng = {...skillOne, ...skillTwo, ...skillThree, ...skillFour};
           console.log(mangseng)
   ```

### 2）symbol

#### （1）概念 

1. Symbol 的值是唯一的，用来解决命名冲突的问题 ，==**遇到唯一性的场景时要想到** **Symbol**==

2. Symbol 值不能与其他数据进行运算，但是可以显示转为字符串，不能转为数字

   ```javascript
   let s = Symbol(666)
   console.log( String(s) )	// 输出 Symbol(666)
   ```

#### （2）定义

1. 添加标识的 symbol，标识只是为了便于开发，并不是 Symbol 的值，此方法返回的结果 不固定

   ```javascript
   	 	let s2 = Symbol('尚硅谷');
           let s3 = Symbol('尚硅谷');
   ```

2. 使用 symbol . for，此方法返回的结果 固定

   ```javascript
   		let s4 = Symbol.for('尚硅谷');
   ```

3. Symbol. prototype. description 可以获取描述字符串

   ```javascript
           //创建 Symbol
           let s = Symbol('尚硅谷');
           console.log(s.description);
   ```

#### （3）应用场景

##### 【1】定义颜色值

```javascript
// 使用symbol定义几个颜色值
const COLOR_RED = Symbol('red')
const COLOR_GREEN = Symbol('green')
const COLOR_PINK = Symbol('pink')
 
// 封装方法，对颜色值进行判断
function getColor(color) {
    switch (color) {
        case COLOR_RED:
            return '红色'
        case COLOR_GREEN:
            return '绿色'
        case COLOR_PINK:
            return '粉色'
        default:
            return '未知色'
    }
}
 
console.log(getColor(COLOR_RED));
```

##### 【2】定义对象的唯一属性名

 ==这类属性不会被 Object.keys 或者 for...in 遍历到，不能被 JSON . stringfy() 序列化，起到保护隐私属性的作用==

```javascript
let a = {
    name:'zhangShan',
    [ Symbol('password') ]:'123456'
    [ Symbol('red') ]:function(){
        console.log("this is red")
    }
}

console.log( a[s] )		// 输出对象a的属性s的值
```

### 3）迭代器

#### （1）概念

- 一种接口，为各种不同的数据结构提供统一的访问机制。任何数据结构只要部署 Iterator 接口，就可以完成遍历操作。

- ES6 创造了一种新的遍历命令 for...of 循环，Iterator 接口主要供 for...of 消费。

  a) Array 

  b) Arguments 

  c) Set 

  d) Map 

  e) String 

  f) TypedArray 

  g) NodeList

- ==for...in...保存的是键名，for...of...保存的是键值。==

  ```javascript
  for( let v of xiyou ){
      console.log(v);
  }
  ```

#### （2）自定义

```javascript
  //声明一个对象
        const banji = {
            name: "终极一班",
            stus: [
                'xiaoming',
                'xiaoning',
                'xiaotian',
                'knight'
            ],
            [Symbol.iterator]() {
                //索引变量
                let index = 0;
                //
                let _this = this;
                return {
                    next: function () {
                        if (index < _this.stus.length) {
                            const result = { value: _this.stus[index], done: false };
                            //下标自增
                            index++;
                            //返回结果
                            return result;
                        }else{
                            return {value: undefined, done: true};
                        }
                    }
                };
            }
        }

        //遍历这个对象 
        for (let v of banji) {
            console.log(v);
        }
```

### 4）生成器

#### （1）概念

- 异步编程解决方案，起到延时加载任务的作用，语法行为与传统函数完全不同 。

- 代码说明： 

  1) * 的位置没有限制。 

  2) 生成器函数返回的结果是迭代器对象，调用迭代器对象的 next 方法可以得到 yield 语句后的值。

  3) yield 相当于函数的暂停标记，也可以认为是函数的分隔符，每调用一次 next 方法，执行一段代码。 

  4) next 方法可以传递实参，作为上一个 yield 语句的返回值。

#### （2）语法

```javascript
	//函数代码的分隔符
        function * gen(){
            // console.log(111);
            yield '一只没有耳朵';
            // console.log(222);
            yield '一只没有尾部';
            // console.log(333);
            yield '真奇怪';
            // console.log(444);
        }

        let iterator = gen();
		gen().next();
       
        //遍历
        for(let v of gen()){
            console.log(v);		// 每次返回的结果为 yield 语句后的字符串
        }
```

#### （3）应用场景

##### 【1】定时器套娃

```javascript
	// 1s 后控制台输出 111  2s后输出 222  3s后输出 333 
   	// 回调地狱
        // setTimeout(() => {
        //     console.log(111);
        //     setTimeout(() => {
        //         console.log(222);
        //         setTimeout(() => {
        //             console.log(333);
        //         }, 3000);
        //     }, 2000);
        // }, 1000);

        function one(){
            setTimeout(()=>{
                console.log(111);
                iterator.next();
            },1000)
        }

        function two(){
            setTimeout(()=>{
                console.log(222);
                iterator.next();
            },2000)
        }

        function three(){
            setTimeout(()=>{
                console.log(333);
                iterator.next();
            },3000)
        }

        function * gen(){
            yield one();
            yield two();
            yield three();
        }

        //调用生成器函数
        let iterator = gen();
        iterator.next();
```

### 5）Promise函数

#### （1）概念

- Promise 是 js 中进行异步编程的新解决方案。
- Promise 对象用于封装一个异步操作并获取其成功 / 失败的结果值。

- ==支持链式调用，可以解决回调地狱的问题。==

#### （2）编码流程 

```javascript
	 const p = new Promise((resolve, reject) => {
                setTimeout(() => {
                    //获取从1 - 100的一个随机数
                    let n = rand(1, 100);
                    //判断
                    if(n <= 30){
                        resolve(n); // 将 promise 对象的状态设置为 『成功』
                    }else{
                        reject(n); // 将 promise 对象的状态设置为 『失败』
                    }
                }, 1000);
            });

            console.log(p);
            //调用 then 方法
            // value 值
            // reason 理由
            p.then((value) => {
                alert('恭喜恭喜, 奖品为 10万 RMB 劳斯莱斯优惠券, 您的中奖数字为 ' + value);
            }, (reason) => {
                alert('再接再厉, 您的号码为 ' + reason);
            });
```

#### （3）对象属性

##### 【1】状态属性 PromiseState

- pending	 未知的
- resolved     成功，结果数据称 value
- rejected     失败，结果数据称 reason

##### 【2】结果属性 PromiseResult

- 保存着异步任务 [成功 / 失败] 的结果。
- 只能由 resolved 或者 rejected 赋值。

#### （4）方法

##### 【1】resolve()

- 属于 Promise 函数对象的方法，不属于实例对象的方法。

- 传入的参数为 非Promise类型的对象, 则返回的结果为成功promise对象
- 传入的参数为 Promise 对象, 则参数的结果决定了 resolve 的结果

```javascript
 let p1 = Promise.resolve(521);
        //如果传入的参数为 非Promise类型的对象, 则返回的结果为成功promise对象
        //如果传入的参数为 Promise 对象, 则参数的结果决定了 resolve 的结果
        let p2 = Promise.resolve(new Promise((resolve, reject) => {
            // resolve('OK');
            reject('Error');
        }));
        p2.catch(reason => {
            console.log(reason);
        })
```

##### 【2】reject()

- 属于 Promise 函数对象的方法，不属于实例对象的方法。
- 无论参数是什么，永远返回一个失败的 promise 对象。

##### 【3】all()

- promises: 包含 n 个 promise 的数组
- 返回一个新的 promise
  - 只有所有的 promise 都成功才成功, 结果为所有  promise 对象 成功的结果所组成的数组。
  - 只要有一个失败了就直接失败，结果为该  promise 对象 失败的结果。

```javascript
 	    let p1 = new Promise((resolve, reject) => {
            resolve('OK');
        })
        
        // let p2 = Promise.resolve('Success');
        let p2 = Promise.reject('Error');
        let p3 = Promise.resolve('Oh Yeah');
        
        const result = Promise.all([p1, p2, p3]);
        console.log(result);
```

##### 【4】race()

- promises: 包含 n 个 promise 的数组

- 返回一个新的 promise，由第一个完成的 promise 的结果状态就是最终的结果状态

```javascript
		let p1 = new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve('OK');
            }, 1000);
        })
        
        let p2 = Promise.resolve('Success');
        let p3 = Promise.resolve('Oh Yeah');

        //调用
        const result = Promise.race([p1, p2, p3]);
        console.log(result);
```

#### （5）关键问题

##### 【1】能否执行多个回调

- 当 promise 实例对象的结果状态 改变为对应状态时都会调用。

##### 【2】 promise 状态改变和指定回调函数的执行顺序

- 都有可能
  - 执行器函数为同步任务时，先改变状态再指定回调函数
  - 执行器函数为异步任务（定时器）时，先指定回调函数再改变状态。但如果 then 方法也是异步任务且延迟时间更长，则先改变状态再指定回调函数。

##### 【3】串联多个任务

1. promise 的 then()返回一个新的 promise, 可以开成 then()的链式调用
2. 通过 then 的链式调用串连多个同步/异步任务

```javascript
  	    let p = new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve('OK');
            }, 1000);
        });

        p.then(value => {
            return new Promise((resolve, reject) => {
                resolve("success");
            });
        }).then(value => {
            console.log(value);         // 输出 success
        }).then(value => {
            console.log(value);         // 输出 underfined
        })
```

##### 【4】异常穿透

- 当使用 promise 的 then 链式调用时, 可以在最后指定失败的回调。前面任何操作出了异常, 都会传到最后失败的回调中处理。

```javascript
 	p.then(value => {
            // console.log(111);
            throw '失败啦!';
        }).then(value => {
            console.log(222); 
        }).then(value => {
            console.log(333);
        }).catch(reason => {
            console.warn(reason);
        });
```

##### 【5】中断 Promise 链

- 有且只有一个方式，返回一个 pending 状态的 Promise 实例对象

```javascript
 	p.then(value => {
            console.log(111);
            return new Promise(() => {});       // 中断 Promise 链条
        }).then(value => {
            console.log(222);
        }).catch(reason => {
            console.warn(reason);
        });
```

### 6）async 函数

#### （1）概述

- async 与 await 结合，可以让异步代码像同步代码一样。

#### （2）async 函数

- 返回值不是 promise 对象，则返回结果的 Promise 对象 PromiseState 为 true，PromiseResult 为返回值。

- 返回值是 promise 对象，函数的返回结果与该对象一致。

#### （3）await 语句

- await 必须写在 async 函数中，await 右侧的表达式一般为 promise 对象。
- 如果表达式是 promise 对象, await 返回的是 promise 成功的值 。
- 如果 await 的 promise 失败了, 就会抛出异常, 需要通过 try...catch 捕获处理。

```javascript
 // await 要放在 async 函数中.
        async function main() {
            try {
                let result = await new Promise((resolve, reject) => {
                    // resolve("用户数据");
                    reject("失败啦!");
                });
                console.log(result);
            } catch (e) {
                console.log(e);
            }
        }
```

#### （4）应用场景

1. 读取文件

   ```javascript
   //1. 引入 fs 模块
   const fs = require("fs");
   
   //读取『为学』
   function readWeiXue() {
       return new Promise((resolve, reject) => {
           fs.readFile("./resources/为学.md", (err, data) => {
               //如果失败
               if (err) reject(err);
               //如果成功
               resolve(data);
           })
       })
   }
   
   function readGuanShu() {
       return new Promise((resolve, reject) => {
           fs.readFile("./resources/观书有感.md", (err, data) => {
               //如果失败
               if (err) reject(err);
               //如果成功
               resolve(data);
           })
       })
   }
   
   //声明一个 async 函数
   async function main(){
       //获取为学内容
       let weixue = await readWeiXue();
       // 获取观书有感
       let guanshu = await readGuanShu();
   
       console.log(weixue.toString());
       console.log(guanshu.toString());
   }
   ```

2. 封装 AJAX 请求

   ```javascript
     // 发送 AJAX 请求, 返回的结果是 Promise 对象
           function sendAJAX(url) {
               return new Promise((resolve, reject) => {
                   //1. 创建对象
                   const x = new XMLHttpRequest();
                   //2. 初始化
                   x.open('GET', url);
                   //3. 发送
                   x.send();
                   //4. 事件绑定
                   x.onreadystatechange = function () {
                       if (x.readyState === 4) {
                           if (x.status >= 200 && x.status < 300) {
                               //成功啦
                               resolve(x.response);
                           }else{
                               //如果失败
                               reject(x.status);
                           }
                       }
                   }
               })
           }
     
           // async 与 await 测试  axios
           async function main(){
               //发送 AJAX 请求
               let result = await sendAJAX("https://api.apiopen.top/getJoke");
               console.log(tianqi);
           }
   ```

### 7）axios 函数

#### （1）基本使用

```javascript
 	//添加一篇新的文章
        btns[1].onclick = function(){
            //发送 AJAX 请求
            axios({
                //请求类型
                method: 'POST',
                //URL
                url: 'http://localhost:3000/posts',
                //设置请求体
                data: {
                    title: "今天天气不错, 还挺风和日丽的",
                    author: "张三"
                }
            }).then(response => {
                console.log(response);
            });
        }
```

#### （2）默认配置

```javascript
 //默认配置
        axios.defaults.method = 'GET';//设置默认的请求类型为 GET
        axios.defaults.baseURL = 'http://localhost:3000';//设置基础 URL
        axios.defaults.params = {id:100};
        axios.defaults.timeout = 3000;//

        btns[0].onclick = function(){
            axios({
                url: '/posts'
            }).then(response => {
                console.log(response);
            })
        }
```

#### （3）拦截器

1. 请求拦截器

   ```javascript
    // 设置请求拦截器  config 配置对象
           axios.interceptors.request.use(function (config) {
               console.log('请求拦截器 成功 - 1号');
               //修改 config 中的参数
               config.params = {a:100};
               return config;
           }, function (error) {
               console.log('请求拦截器 失败 - 1号');
               return Promise.reject(error);
           });
   
           axios.interceptors.request.use(function (config) {
               console.log('请求拦截器 成功 - 2号');
               //修改 config 中的参数
               config.timeout = 2000;
               return config;
           }, function (error) {
               console.log('请求拦截器 失败 - 2号');
               return Promise.reject(error);
           });
   ```

2. 响应拦截器

   ```javascript
     // 设置响应拦截器
           axios.interceptors.response.use(function (response) {
               console.log('响应拦截器 成功 1号');
               return response.data;
               // return response;
           }, function (error) {
               console.log('响应拦截器 失败 1号')
               return Promise.reject(error);
           });
   
           axios.interceptors.response.use(function (response) {
               console.log('响应拦截器 成功 2号')
               return response;
           }, function (error) {
               console.log('响应拦截器 失败 2号')
               return Promise.reject(error);
           });
   ```

### 8）数据结构

#### （1）Set 集合

- 类似于数组，元素的值唯一，创建时自动去重

- 本质是一个对象，实现了 iterator 接口

- 属性方法

  |  方法  |                    含义                     |
  | :----: | :-----------------------------------------: |
  |  size  |             返回集合的元素个数              |
  |  add   |        增加一个新元素，返回当前集合         |
  | delete |          删除元素，返回 boolean 值          |
  |  has   | 检测集合中是否包含某个元素，返回 boolean 值 |
  | clear  |          清空集合，返回 undefined           |

- 运算

  1. 数组去重

  ```javas
          let result = [...new Set(arr)];
          console.log(result);
  ```

  2. 交集

  ```javascript
  		let arr = [1,2,3,4,5,4,3,2,1];
          let arr2 = [4,5,6,5,6];
          let result = [...new Set(arr)].filter(item => new Set(arr2).has(item));
  ```

  3. 并集

  ```javascript
  	  let union = [...new Set([...arr, ...arr2])];
        console.log(union);
  ```

  4. 差集

  ```javascript
  	let diff = [...new Set(arr)].filter(item => !(new Set(arr2).has(item)));
      console.log(diff);
  ```

#### （2）Map

- 类似于对象，也是键值对的集合。

- ==Object.entries 可以结合使用== 

  ```javascript
  		//声明对象
          const school = {
              name:"尚硅谷",
              cities:['北京','上海','深圳'],
              xueke: ['前端','Java','大数据','运维']
          };
  
          // 创建 Map
          const m = new Map(Object.entries(school));
          console.log(m.get('cities'));
  
          // 输出 ['北京', '上海', '深圳']
  ```

- ==但是“键” 的范围不限于字符串，各种类型的值（包括对象）都可以当作键。==

- 实现了 iterator 接口，遍历时每个元素形成一个数组，每个数组有两个元素，元素1是键名，元素2是键值。

- 属性方法

  | 方法  |                     含义                     |
  | :---: | :------------------------------------------: |
  | size  |             返回 Map 的元素个数              |
  |  set  |         增加一个新元素，返回当前 Map         |
  |  get  |              返回键名对象的键值              |
  |  has  | 检测 Map 中是否包含某个元素，返回 boolean 值 |
  | clear |           清空集合，返回 undefined           |


### 9）Class 类

#### （1）构造方法

```javascript
 //class
        class Shouji{
            //构造方法 名字不能修改
            constructor(brand, price){
                this.brand = brand;
                this.price = price;
            }

            //方法必须使用该语法, 不能使用 ES5 的对象完整形式 call:function(){}
            call(){
                console.log("我可以打电话!!");
            }
        }

        let onePlus = new Shouji("1+", 1999);
        console.log(onePlus);
```

#### （2）私有属性

- ‘ # ’ 表示私有属性

  ```javascript
          class Person{
              //公有属性
              name;
              //私有属性
              #age;
              #weight;
              //构造方法
              constructor(name, age, weight){
                  this.name = name;
                  this.#age = age;
                  this.#weight = weight;
              }
          }
  ```

#### （3）静态成员

- 对于 static 标注的属性方法，属于类而不属于实例对象。

  ```javascript
   class Phone{
              //静态属性
              static name = '手机';
              static change(){
                  console.log("我可以改变世界");
              }
          }
  
          let nokia = new Phone();
          console.log(nokia.name);	// underfined
          console.log(Phone.name);	// 手机
  ```

#### （4）类继承

- 子类对父类方法的重写，只能是完全重写

```javascript
		class Phone{
            //构造方法
            constructor(brand, price){
                this.brand = brand;
                this.price = price;
            }
            //父类的成员属性
            call(){
                console.log("我可以打电话!!");
            }
        }

        class SmartPhone extends Phone {
            //构造方法
            constructor(brand, price, color, size){
                super(brand, price);// Phone.call(this, brand, price)
                this.color = color;
                this.size = size;
            }

            photo(){
                console.log("拍照");
            }

            playGame(){
                console.log("玩游戏");
            }

            // 重写父类的方法
            call(){
                console.log('我可以进行视频通话');
            }
        }

        const xiaomi = new SmartPhone('小米',799,'黑色','4.7inch');
        console.log(xiaomi);
        xiaomi.call();
        xiaomi.photo();
        xiaomi.playGame();
```

#### （5）getter 与 setter

- 设置、获取属性时，自动调用。

```javascript
 	// get 和 set  
        class Phone{
            get price(){
                console.log("价格属性被读取了");
                return 'iloveyou';
            }

            set price(newVal){
                console.log('价格属性被修改了');
            }
        }

        //实例化对象
        let s = new Phone();
        console.log(s.price);      // 输出 价格属性被读取了
        s.price = 'free';         // 输出 价格属性被修改了
```

### 10）扩展

#### （1）Numer 类

1. Number.EPSILON 是 JavaScript 表示的最小精度

   ```javascript
    function equal(a, b){
               if(Math.abs(a-b) < Number.EPSILON){
                   return true;
               }else{
                   return false;
               }
           }
           console.log(0.1 + 0.2 === 0.3);     // false
           console.log(equal(0.1 + 0.2, 0.3))  // true
   ```

2. 进制

   ```javascript
     		let b = 0b1010;
           let o = 0o777;
           let d = 100;
           let x = 0xff;
           console.log(x);
   ```

3. 属性方法

   |       方法        |                       作用                       |
   | :---------------: | :----------------------------------------------: |
   |  Number.isFinite  |             检测一个数值是否为有限数             |
   |   Number.isNaN    |              检测一个数值是否为 NaN              |
   |  Number.parseInt  |                   字符串转整数                   |
   | Number.parseFloat |                  字符串转浮点数                  |
   | Number.isInteger  |               判断一个数是否为整数               |
   |    Math.trunc     |               将数字的小数部分抹掉               |
   |     Math.sign     | 判断一个数到底为正数 负数 还是零，返回1 / -1 / 0 |

#### （2）Object 类

0. 属性方法

   |        方法        |                           作用                           |
   | :----------------: | :------------------------------------------------------: |
   |    Object.keys     |                     获取对象所有的键                     |
   |   Object.values    |                     获取对象所有的值                     |
   |   Object.entries   | 对象转数组，返回二维数组，第二层数组的元素为键名，键值。 |
   | Object.fromEntries |      数组转对象，用于创建对象，参数为二维数组或 Map      |

1. Object.is 判断两个值是否完全相等 

   ```javascript
   console.log(Object.is(120, 120));// true
   console.log(Object.is(NaN, NaN));// true
   console.log(NaN === NaN);// false
   ```

2. Object.assign 对象的合并，有相同属性时，参数2 把参数1 覆盖

   ```javascript
    		const config1 = {
               host: 'localhost',
               port: 3306,
               name: 'root',
               pass: 'root',
               test: 'test'
           };
           const config2 = {
               host: 'http://atguigu.com',
               port: 33060,
               name: 'atguigu.com',
               pass: 'iloveyou',
               test2: 'test2'
           }
           console.log(Object.assign(config1, config2));
   
   // 输出
           host: "http://atguigu.com"
           name: "atguigu.com"
           pass: "iloveyou"
           port: 33060
           test: "test"
           test2: "test2"
   ```

#### （3）数组

1. Includes 方法用来检测数组中是否包含某个元素，返回布尔类型值 

   ```javascript
           const mingzhu = ['西游记','红楼梦','三国演义','水浒传'];
           console.log(mingzhu.includes('西游记'));
           console.log(mingzhu.includes('金瓶梅'));
   ```

2. flat 方法用于数组降维，参数为深度，是一个数字

   ```javascript
           //将多维数组转化为低位数组
           const arr = [1,2,3,4,[5,6,[7,8,9]]];
           console.log(arr.flat(2));  
   ```

#### （4）字符串

- trimStart 清除左侧空白
- trimEnd 清除右侧空白

#### （5）指数操作符

- 在 ES7 中引入指数运算符「**」，用来实现幂运算，功能与 Math.pow 结果相同

  ```javascript
   		console.log(2 ** 10);
          console.log(Math.pow(2, 10));
  ```

### 11）模块化

#### （1）暴露方式

##### （1）分别暴露

```javascript
    //分别暴露
    export let school = '尚硅谷';

    export function teach() {
        console.log("我们可以教给你开发技能");
    }

	import * as m1 from "./src/js/m1.js";
```

##### （2）统一暴露

```javascript
    //统一暴露
    let school = '尚硅谷';

    function findJob(){
        console.log("我们可以帮助你找工作!!");
    }

    export {school, findJob};
```

##### （3）默认暴露

- default 是一个对象

```javascript
    //默认暴露
    export default {
        school: 'ATGUIGU',
        change: function(){
            console.log("我们可以改变你!!");
        }
    }

	import * as m3 from "./src/js/m3.js";

	m3.default.change();	// 需要添加 default
```

#### （2）导入方式

##### （1）通用导入

```javascript
	import * as m2 from "./src/js/m2.js";
```

##### （2）解构赋值形式

- 使用别名，防止命名冲突

```javascript
	import {school, teach} from "./src/js/m1.js";
	import {school as guigu, findJob} from "./src/js/m2.js";
	import {default as m3} from "./src/js/m3.js";
```

##### （3）简便形式

- 简便形式  针对默认暴露

```javascript
	import m3 from "./src/js/m3.js";
```

### 12）正则表达式

#### （1）元字符

|     类型      |   符号   |             说明             | 注解 |
| :-----------: | :------: | :--------------------------: | :--: |
|    边界符     |    ^     |         必须以谁开头         |      |
|    边界符     |    $     |         必须以谁结尾         |      |
|               |    .     | 默认匹配除换行符外的单个字符 |      |
| 大括号/原子表 |   [ ]    |         匹配其一即可         |  1   |
| 中括号/量词符 |  { n }   |          重复 n 次           |      |
| 小括号/原子组 |   （）   |            优先级            |  4   |
|    字符类     |   [^]    |             取反             |      |
|    范围符     |  [ - ]   |           范围限定           |  2   |
|    量词符     |    *     |          0次及以上           |  3   |
|    量词符     |    +     |          1次及以上           |      |
|    量词符     |    ？    |           0次及1次           |      |
|    量词符     | { n , }  |       重复 n 次及以上        |      |
|    量词符     | { n , m} |       重复 n 次到 m 次       |      |

1. [] 表示有一系列字符可以选择，匹配其一即可

   ```javascript
   let rg = /[abc]/;
   console.log(rg.test('andy'));	// true
   ```

2. 字符组合，大小写字母、数字、短杆、下划线都可以

   ```javascript
   let rg = /^[a-zA-Z0-9_-]$/
   ```

3. 量词符 *

   ```javascript
   let reg = /^a*$/
   console.log(reg.test(''))		// true
   console.log(reg.test('a'))		// true
   console.log(reg.test('aaaa'))	// true
   ```

4. （）表示优先级

   ```javascript
   let reg = /^(abc){3}$/;
   console.log(reg.test('abccc'))	// false
   console.log(reg.test('abcabcabc'))	// true
   ```

#### （2）预定义类

| 预定义类 |                             说明                             |
| :------: | :----------------------------------------------------------: |
|   \ d    |                        相当于[ 0-9 ]                         |
|   \ D    |                        相当于[ ^0-9 ]                        |
|   \ w    |                     相当于[ a-zA-Z0-9_ ]                     |
|   \ W    |                    相当于[ ^a-zA-Z0-9_ ]                     |
|   \ s    | 匹配空格（换行符、制表符、空格符），相当于[ \t \r \n \v \f ] |
|   \ S    |                        相当于 \s 取反                        |

#### （3）方法

1. replace 替换，参数1是正则表达式，参数2是替换为的字符串

   ```javas
   let str = 'andy和red';
   let newStr = str.replace(/andy/,'baby');	// baby和red
   ```

2. test 匹配，返回 true 或者 false

3. exec 捕获，返回 Array 或者 null

#### （4）参数

- g：全局匹配

- i：忽略大小写

- gi：全局匹配并且忽略大小写

- m：多行搜索模式

- s：使 . 能够匹配换行符

  ```javascript
  let reg = /^(abc){3}$/g;
  ```