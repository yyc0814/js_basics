## closure
http://bonsaiden.github.io/JavaScript-Garden/#function.closures
Closures and References
One of JavaScript's most powerful features is the availability of closures. With closures, scopes always keep access to the outer scope, in which they were defined. Since the only scoping that JavaScript has is function scope, all functions, by default, act as closures.

```javascript
function Counter(start) {
    var count = start;
    return {
        increment: function() {
            count++;
        },

        get: function() {
            return count;
        }
    }
}

var foo = Counter(4);
foo.increment();
foo.get(); // 5
```

### scope change with setTimeout
```javascript
for(var i = 0; i < 5; i++) {
    setTimeout(function() {
        console.log(i);  
    }, 1000);
}

//5 for 5 times
```

to resolve the issue

```javascript
for(var i = 0; i < 5; i++) {
    (function(j){
    setTimeout(function() {
        console.log(j);  
    }, 1000);
    })(i)
}
```


#### 0.2+0.1 is not 0.3
#### use math.js or decimal.js to resolve it

## Promise
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

#### microtask
```javascript
Promise
Object.observe
```

#### macrotask
```javascript
setTimeout()
setInterval()
```

## CROSS DOMAIN
JSONP
#### 1.

```javascript
<script src="http://domain/api?param1=a&param2=b&callback=jsonp"></script>
<script>
    function jsonp(data) {
    	console.log(data)
	}
</script>
```

#### 2.

```javascript
function jsonp(url, jsonpCallback, success) {
  let script = document.createElement('script')
  script.src = url
  script.async = true
  script.type = 'text/javascript'
  window[jsonpCallback] = function(data) {
    success && success(data)
  }
  document.body.appendChild(script)
}
jsonp('http://xxx', 'callback', function(value) {
  console.log(value)
})
```

#### 3.
CORS

Access-Control-Allow-Origin
set in service or 
<meta http-equiv="Access-Control-Allow-Origin" content="*">

##### 4.

nginx proxy_pass

#### 5.
window.postMessage(message, targetOrigin);

## Storage

localStorage sessionStorage cookies

localStorage and session are both so-called WebStorages and features of HTML5.

localStorage on user side /larger storage base on browser / no expiration till user delete them 

session store on server side/ the data is stored until the browser (or tab) is closed. / 5MB

cookies store on user side/4KB / login status, shopping cart

https://juejin.im/post/5c6bcdc8e51d45209a1ca3b6

localStorage stores information as long as the user does not delete them.

sessionStorage stores information as long as the session goes. Usually until the user closes the tab/browser.



## curry function

1. Write little code modules that can be reused and configured with ease, much like what we do with npm:
2. Avoid frequently calling a function with the same argument:

```javascript
function multiply(a) {
    return (b) => {
        return (c) => {
            return a * b * c
        }
    }
}
log(multiply(1)(2)(3)) // 6
```

```javascript
function discount(discount) {
    return (price) => {
        return price * discount;
    }
}
const tenPercentDiscount = discount(0.1);
```
```javascript
function multiply(a) {
	return function m1(b){
		return function m2(c){
			return a*b*c
		}
	}
}
```



### reduce() 
method executes a reducer function (that you provide) on each member of the array resulting in a single output value.

### map() 
method creates a new array with the results of calling a provided function on every element in the calling array.

pokemonName.call(pokemon,'sushi', 'algorithms'); // Pika Chu  loves sushi and algorithms

pokemonName.apply(pokemon,['sushi', 'algorithms']); // Pika Chu  loves sushi and algorithms

## immutability 

#### string is immutable

Object.seal() preventing new properties from being added to it and marking all existing properties as non-configurable
Object.freeze() cant be changed, immutable
Object.preventExtensions()
