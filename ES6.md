### 1.变量
  * var     重复声明、函数级
  * let     不能重复声明、块级块级作用域、变量
  * const   不能重复声明、块级作用域、常量

### 2.函数——箭头函数
```javascript
function name(){}
// 变成了：
let name = ()=>{}
```
```javascript
let arr=[12, 5, 8, 99, 33, 14, 26];
// 箭头函数：
arr.sort((n1, n2)=>n1-n2);
// 等价于：
arr.sort(function (n1, n2){
    return n1-n2;
});
```

>总结：如果只有一个参数，()可以省;如果只有一个return，{}可以省;箭头函数不会创建自己的this,它只会从自己的作用域链的上一层继承this。

### 3.函数的参数
1. 参数扩展/数组展开
+ 1-1 收集参数
    ```javascript
    function show(a, b, ...args){}
    // Rest Parameter必须是最后一个
    ```
+ 1-2展开数组
    ```javascript
    let arr1=[1,2,3];
    let arr2=[5,6,7];
    let arr=[...arr1, ...arr2]; // 1,2,3,5,6,7

    // 展开后的效果，跟直接把数组的内容写在这儿一样 

    function show(...args){
      fn(...args);
    }
    function fn(a, b){
      alert(a+b);
    }
    show(12, 5);
    ```
2. 默认参数
```javascript
function show(a, b=5, c=12){
    console.log(a, b, c);
}
show(99, 19, 88);
```
### 4.解构赋值：
1. 左右两边结构必须一样
```javascript
let [json, arr, num, str]=[{a: 12, b: 5}, [12,5,8], 8, 'cxzcv'];  // 正确
let {a, c, d}={a: 12, c: 5, d: 6};  // 正确
let [a,b]={a: 12, b: 45};  //错误
let {a,b}={12,45}; // 错误
```
2. 右边必须是个合法的数据类型(数组，json类型)
```javascript
let {a,b}={12,5}; // 错误
```
3. 声明和赋值不能分开(必须在一句话里完成)
```javascript
    let [a,b];
    [a,b]=[12,5];
    // 错误
```
### 5.数组：
1.map（映射：一一对应）
```javascript
let arr=[12,5,8];
let result=arr.map(item=>item*2);

let score=[19, 85, 99, 25, 90];
let result=score.map(item=>item>=60?'及格':'不及格');
```
2.reduce(汇总:一堆出来一个)
```javascript
// 求和
let arr1=[12,69,180,8763];
// tep:临时值，中间值（第一次为数组的第一个值）
// item：数组的值（从数组的第二个值开始）
// index: 0，1，2，3...
let result1=arr.reduce(function (tmp, item, index){ 
    //alert(tmp+','+item+','+index);
    return tmp+item;
});
 alert(result);
// 求平均数
let arr2=[12,69,180,8763];
let result2=arr.reduce(function (tmp, item, index){
    if(index!=arr.length-1){ //不是最后一次
        return tmp+item;
    }else{                    //最后一次
        return (tmp+item)/arr.length;
    }
});
 alert(result2);
```
3.filter（过滤器）
```javascript
let arr=[12,5,8,99,27,36,75,11];
let result=arr.filter(item=>item%3==0);
alert(result);
```
4.forEach（循环、迭代）
```javascript
let arr=[12,5,8,9];
arr.forEach((item,index)=>{
    alert(index+': '+item);
});
```
### 6.字符串：

1.多了两个新方法
  1-1.startsWith
  ```javascript
    let str='git://www.baidu.com/2123123';
    if(str.startsWith('http://')){
        alert('普通网址');
    }else if(str.startsWith('https://')){
        alert('加密网址');
    }else if(str.startsWith('git://')){
        alert('git地址');
    }else if(str.startsWith('svn://')){
        alert('svn地址');
    }else{
        ('其他');
    }
  ```
  1-2.endsWith
  ```javascript
    let str='1.png';

    if(str.endsWith('.txt')){
        alert('文本文件');
    }else if(str.endsWith('.jpg')){
        alert('JPG图片');
    }else{
        alert('其他');
    }
  ```

2.字符串模板(字符串连接)
>用法：把内容用两个反单引号包裹起来

  i. 直接把变量塞到字符串里面，如：${变量}  
  ii. 可以折行
  ```javascript
    let title='标题';
    let content='内容';
    let str='<div>\
      <h1>'+title+'</h1>\
      <p>'+content+'</p>\
    </div>';
    // 等价于
    let str2=`<div>
      <h1>${title}</h1>
      <p>${content}</p>
    </div>`;
  ```  

### 7.面向对象

1. class关键字、构造器和类分开了,class里面直接加方法
```javascript
    function User(name, pass){
      this.name=name;
      this.pass=pass;
    }

    User.prototype.showName=function (){
      alert(this.name);
    };
    User.prototype.showPass=function (){
      alert(this.pass);
    };
    // 等价于ES6的写法
    class User{
      constructor(name, pass){
        this.name=name;
        this.pass=pass;
      }

      showName(){
        alert(this.name);
      }
      showPass(){
        alert(this.pass);
      }
    }
    var u1=new User('blue', '123456');
    u1.showName();
    u1.showPass();
```
2. 继承：super  超类==父类
```javascript
class User{
    constructor(name, pass){
        this.name=name;
        this.pass=pass;
    }

    showName(){
        alert(this.name);
    }
    showPass(){
        alert(this.pass);
    }
}

class VipUser extends User{
    constructor(name, pass, level){
    super(name, pass);
    this.level=level;
    }

    showLevel(){
        alert(this.level);
    }
}

var v1=new VipUser('blue', '123456', 3);
v1.showName();
v1.showPass();
v1.showLevel();
```

### 8.JSON对象
1. JSON对象  

  1.1 JSON转成字符串:  `JSON.stringify`
  ```javascript
  JSON.stringify({a:12,b:5})  =>  '{"a":12,"b":5}'
  ```
  1.2 字符串转成JSON:  `JSON.parse`
  ```javascript
   JSON.parse('{"a":12,"b":5}')=>  {a:12,b:5}
  ```

2. 简写
  *  名字跟值(key和value)一样的,留一个就行
  ```JavaScript
  let a=12;
  let b=5;
  let json={a, b, c: 55};
  ```
* 方法: function一块删

>show: function (){...} <=> show(){...}
```javascript
let json={
      a: 12,
      show(){
        alert(this.a);
      }
    };

    json.show();
```
3.json的标准写法：  
* 只能用双引号  
*  所有的名字都必须用引号包起来
```javascript
{a: 12, b: 5}       ×
{"a": 12, "b": 5}   √

{a: 'abc', b: 5}    ×
{"a": "abc", "b": 5}√
```

### 10.Promise——消除异步操作
* 异步：操作之间没啥关系，同时进行多个操作
* 同步：同时只能做一件事

1. Promise.all
```javascript
// 异步：
ajax('/banners', function (banner_data){
  ajax('/hotItems', function (hotitem_data){
    ajax('/slides', function (slide_data){
      ajax('/slides', function (slide_data){

      }, function (){
        alert('读取失败');
      });
    }, function (){
      alert('读取失败');
    });
  }, function (){
    alert('读取失败');
  });
}, function (){
  alert('读取失败');
});

// 有了Promise之后的异步：
Promise.all([
      $.ajax({url: 'data/arr.txt', dataType: 'json'}),
      $.ajax({url: 'data/json.txt', dataType: 'json'}),
      $.ajax({url: 'data/num.txt', dataType: 'json'})
    ]).then(results=>{
      let [arr, json, num]=results;

      alert('成功了');

      console.log(arr, json, num);
    }, err=>{
      alert('失败了');
    });

```

2. Promise.race(竞速,谁快取谁)
```javascript
Promise.race([
  $.ajax({url: 'http://a2.taobao.com/data/users'}),
  $.ajax({url: 'http://a15.taobao.com/data/users'}),
  $.ajax({url: 'http://a3.taobao.com/data/users'}),
  $.ajax({url: 'http://a7.taobao.com/data/users'})
]);
```
### 11.generator-生成函数
1. 函数运行时可停止，停止关键字yield，generator函数的关键字*，即： 

```javascript
function *函数(){...}

function * 函数(){...} 

function* 函数(){...}
```
>generator不能写成箭头函数

```javascript
function *函数(){
  代码...
  // yield 停止的标志
  yield ajax(xxx);

  代码...
}
```
```javascript
 function *show(){
      alert('a');

      yield;

      alert('b');
    }

    function show_1(){
      alert('a');
    }
    function show_2(){
      alert('b');
    }

    let genObj=show();
    // next一下执行一步，类似单步调试
    genObj.next();    //等价于show_1
    genObj.next();    //等价于show_2
```

2. yield
>简单的说yield把函数体分成了多个部分，并且相当于一个中间值，把上一步执行的结果返回给下一步，而且yield还可以传参，还可以返回值。
```javascript
function *show(num1, num2){
      alert(`${num1}, ${num2}`);
      alert('a');

      let a=yield;

      alert('b');
      alert(a);

      return;
    }

    let gen=show(99, 88);

    gen.next(12); //第一步yield没出现，没法给yield传参
    gen.next(5); // 结果为5
```

```javascript
function *show(){
      alert('a');

      yield 12;

      alert('b');

      return 55;
    }

    let gen=show();

    let res1=gen.next();
    console.log(res1);      //{value: 12, done: false}

    let res2=gen.next();
    console.log(res2);      //{value: 55, done: true}
```
### 12.异步操作
1. 异步方法对比（回调、Promise、 generator）

```javascript
//回调
$.ajax({
  url: xxx,
  dataType: 'json'
  success(data1){
    $.ajax({
      url: xxx,
      dataType: 'json'
      success(data2){
        $.ajax({
          url: xxx,
          dataType: 'json'
          success(data3){
            //完事儿
          },
          error(){
            alert('错了');
          }
        });
      },
      error(){
        alert('错了');
      }
    });
  },
  error(){
    alert('错了');
  }
});

//Promise
Promise.all([
  $.ajax({url: xxx, dataType: 'json'}),
  $.ajax({url: xxx, dataType: 'json'}),
  $.ajax({url: xxx, dataType: 'json'})
]).then(results=>{
  //完事儿
}, err=>{
  alert('错了');
});

//generator
runner(function *(){
  let data1=yield $.ajax({url: xxx, dataType: 'json'});
  let data2=yield $.ajax({url: xxx, dataType: 'json'});
  let data3=yield $.ajax({url: xxx, dataType: 'json'});
  console.log(data1, data2, data3);
  //完事儿
});
```
```javascript
//借助generator的辅助函数runner
function runner(_gen){
  return new Promise((resolve, reject)=>{
    var gen=_gen();

    _next();
    function _next(_last_res){
      var res=gen.next(_last_res);

      if(!res.done){
        var obj=res.value;

        if(obj.then){
          obj.then((res)=>{
            _next(res);
          }, (err)=>{
            reject(err);
          });
        }else if(typeof obj=='function'){
          if(obj.constructor.toString().startsWith('function GeneratorFunction()')){
            runner(obj).then(res=>_next(res), reject);
          }else{
            _next(obj());
          }
        }else{
          _next(obj);
        }
      }else{
        resolve(res.value);
      }
    }
  });
}

```

2. 带逻辑性的异步
```javascript
//带逻辑-普通回调
$.ajax({url: 'getUserData', dataType: 'json', success(userData){
  if(userData.type=='VIP'){
    $.ajax({url: 'getVIPItems', dataType: 'json', success(items){
      //生成列表、显示...
    }, error(err){
      alert('错了');
    }});
  }else{
    $.ajax({url: 'getItems', dataType: 'json', success(items){
      //生成列表、显示...
    }, error(err){
      alert('错了');
    }});
  }
}, error(err){
  alert('错了');
}});

//带逻辑-Promise
Promise.all([
  $.ajax({url: 'getUserData', dataType: 'json'})
]).then(results=>{
  let userData=results[0];

  if(userData.type=='VIP'){
    Promise.all([
      $.ajax({url: 'getVIPItems', dataType: 'json'})
    ]).then(results=>{
      let items=results[0];

      //生成列表、显示...
    }, err=>{
      alert('错了');
    });
  }else{
    Promise.all([
      $.ajax({url: 'getItems', dataType: 'json'})
    ]).then(results=>{
      let items=results[0];

      //生成列表、显示...
    }, err=>{
      alert('错了');
    });
  }
}, err=>{
  alert('失败');
});

//带逻辑-generator
runner(function *(){
  let userData=yield $.ajax({url: 'getUserData', dataType: 'json'});

  if(userData.type=='VIP'){
    let items=yield $.ajax({url: 'getVIPItems', dataType: 'json'});
  }else{
    let items=yield $.ajax({url: 'getItems', dataType: 'json'});
  }

  //生成、...
});
```
> 总结：Promise——一次读一堆，generator——逻辑性

### 13.模块化
```javascript
// module1.js
// 定义
export name = 'LL'
export age = 20
export function sayHello(){
    console.log(`hello ${name}`)
}

export default site='xxx.com'
```

```javascript
// 定义module2.js
// 引用
import site, {name, age} from './module1' // 有default关键字时引用不需要{}，其他的需要{}括起来
import * as module1 from './module1'  // * as ···表示引用所有的变量
console.log(site,name,age)
moule1.sayHello()
```