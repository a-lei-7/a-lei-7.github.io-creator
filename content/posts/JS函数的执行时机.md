---
title: "JS函数的执行时机"
date: 2020-03-04T13:59:59+08:00
draft: false
---

S 的执行顺序一般是从上往下依次进行，比如下面这个函数， 先是声明了 i ，然后利用 for 循环，将 i 不断 +1 ，依次打出。打印结果依次为: 0 1 2 3 4 5

```
let i = 0
for(i =0; i<6; i++){
	console.log(i)
}
```

如果这时在 for 循环内添加一个延时执行函数，那么结果就会发生变化，将打印出 6 个 6

```
let i = 0
for(i = 0; i<6; i++){
  setTimeout(()=>{
    console.log(i)
  },0)
}
```

我们可以在 setTimeout 后面加上一句，以此判断函数的执行顺序。

```
let i = 0
for(i=0;i<6;i++){
    setTimeout(()=>{
        console.log(i)
},0)
    console.log(i)
}
// 结果为：
0
1
2
3
4
5

6
6
6
6
6
6
```

当执行到延时函数 setTimeout 时，JS 会先跳过，将 setTimeout 函数放在另一个地方，继续执行 for 循环。打出 0 1 2 3 4 5 ,当 for 循环执行完毕之后，再将 setTimeout 函数取出执行，在这个时候 i 经过 for 循环已经变成了 6 ，所以之后 setTimeout 打印出的结果就都是 6 .

以下有几种解决方案，让打印的结果为 0 1 2 3 4 5

可以将 let 声明加入 for 循环的头部，这样会让变量在循环的过程中被声明多次，每次变量变化的时候，值都会再次声明，这样就可以保证在 setTimeout 执行的时候拥有所有 i 的值

```
for (let i=0; i<6 ; i++){
	setTimeout(()=>{
  	console.log(i)}
  ,0)
}
```

除此之外，可以将 setTimeout 放在一个立即执行函数里面，将 i 作为参数传到函数内

```
let i = 0
for(i=0; i<6; i++){
	! function(i){
  	setTimeout(()=>{console.log(i)},0)
  }(i)
}
```

也可以将 setTimeout 单独放在一个函数里面，等到循环的时候一次次去调用

```
let a = function(i){
    setTimeout(()=>{console.log(i)},0)
}
let i = 0
for(i=0;i<6;i++){
    a(i)
}
```

使用 bind 函数，将 i 的值绑定在 setTimeout 上面

```
let i =0
for (i=0; i<6; i++) {
  setTimeout( function timer(i) {
    console.log(i);
  }.bind(null,i), 0 );
}
```

利用 setTimeout 的第三个参数

```
for (var i=1; i<=5; i++) {
  setTimeout( function timer(i) {
    console.log(i);
   }, 0,i );
}
```
