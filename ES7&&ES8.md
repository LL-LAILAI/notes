  ### 1.数组 
  * includes(数组是否包含某个东西)
  ```javascript
  let arr=[12,5,8];
  alert(arr.includes(8));
  ```

   * for···in和for···of
   ```
                     数组          json
     for...in        下标(key)     key
     for...of        值(value)     ×
   ```
```javascript
let arr=[12,5,8,99,31];

    for(let i in arr){
      alert(i); // 0,1,2,3,4
    }

    for(let i of arr){
      alert(i); //12,5,8,99,31
    }
```
```javascript
let json={a: 12, b: 5, c: 99};

    for(let i in json){
      alert(i); // a,b,c
    }
    
    for(let i of json){
      alert(i); // 出错
    }
```
* keys/values/entries

  * keys=>所有的key拿出来               
   ```javascript
   let arr=[12,5,8,99];

    for(let key of arr.keys()){
      alert(key); //  0,1,2,3,4,...
    }
   ```
  * values=>所有的values拿出来          
   ```javascript
   arr=[12,5,8,99];
   for(let value of arr.values()){
       alert(value); //12,5,8,99,...
    }
   ```
  * entries=>所有的key-value对拿出来    
  {key: 0, value: 12},{key: 1, value: 5}, ...entry实体
   ```javascript
   let arr=[12,5,8,99];

    for(let entry of arr.entries()){
      alert(entry); // 0,12  1,5 ...
    }
   ```

### 2.求幂   

> 符号：** ， 例：3**8
### 3.字符串
* padStart：从开始位置补位，第一参数补多少，第二参数补什么，默认为空格
```javascript
console.log('('+'5641'.padStart(10, '0')+')');
```
* padEnd：从末尾位置补位
```javascript
console.log('('+'abc'.padEnd(10)+')');
```

### 4.generator yield =>async await

* 不依赖于外部的runner了——统一、性能
* 可以用箭头函数

```javascript
    let readData=async ()=>{
    let data1=await $.ajax({url: 'data/1.txt', dataType: 'json'});
    let data2=await $.ajax({url: 'data/2.txt', dataType: 'json'});
    let data3=await $.ajax({url: 'data/3.txt', dataType: 'json'});
      console.log(data1, data2, data3);
    }
    readData();
```