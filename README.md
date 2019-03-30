// 0.2+0.1 is not 0.3
// use math.js or decimal.js to resolve it

```javascript
var p = new Promise(function(resolve, reject){
    //做一些异步操作
    setTimeout(function(){
        console.log('');
        resolve('');
        rejct('')
    }, 2000);
});
```

```javascript
Promise
.all([runAsync1(), runAsync2(), runAsync3()])
.then(function(results){
    console.log(results);
});
```

```javascript
Promise
.race([runAsync1(), runAsync2(), runAsync3()])
.then(function(results){
    console.log(results);
});
```
