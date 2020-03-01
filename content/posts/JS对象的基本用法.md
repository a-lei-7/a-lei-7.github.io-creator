---
title: "JS对象的基本用法"
date: 2020-03-01T15:03:04+08:00
draft: false
---

## 对象的定义和写法

定义： 对象是一个 无序的，由键值对组成的集合。

有两种声明的方式：

```
let obj = {name :'ergou',age:18} //多组数据可以用 ',' 隔开，这种为新的书写方式

let obj = new Object({name:'ergou'})  //这种一次只能添加一个属性，是以前的写法

// 属性名为字符串，可以是任意字符。如果不是标识符的话，就需要加上引号。 symbol 也可以作为属性名
```

当中的 'name' 为 key，即属性名; 后面的 'ergou' 为 value ，即属性值

```
let a = 'name'
let obj = { [a]:'ergou' } //这样的话，属性名就是变量 a 的值，为'name'
let obj = { a:'ergou' } //这样属性名就是 'a'

// 属性名没有添加[] 的话，会自动变为字符串。
```

JS 的每一个对象中都含有一个隐藏属性，这个隐藏属性中存储着共有属性组成的对象地址，这个共有属性的对象被称作原型。即原型当中存储着对象的共有属性。这个原型的原型值为 null

```
let obj = ()
obj
    {}
        __proto__:Object
```

## JS 的增删改查

### 删除对象中的属性

如何删除一个属性

```
obj.name = undefined //删除对象 obj 中'name'的属性值

delete obj.name
delete obn['name']
//这两种都是删除对象 obj 当中的属性'name'
```

检测对象中属性是否存在

```
'name' in obj  //判断'name'是否在对象 obj 里，如果值为 false，说明对象 obj 不含有这个属性；
              //为 true 表示存在，若为 undefined ，表示存在这个属性且属性值为 undefined

obj.name  //如果输出值为：undefined 的话，代表对象 obj 中的属性'name'值为 undefined
          //不能断定 name 是否是 obj 的属性
```

### 属性的读取

查看对象的属性名和属性值

```
Object.keys(obj)  //查看对象 obj 的所有属性名
Object.values(obj) //查看对象 obj 的所有属性值
Object.entries(obj) //查看对象 obj 的属性名和属性值

console.dir(obj) //查看自身属性和共有属性
Object.keys(obj.__proto__) //查看对象 obj 的共有属性

obj.hasOwnProperty('属性名') //判断'属性名'是属于对象 obj ,还是属于共有属性
```

查看对象中单个属性的值

```
'name' in obj  //判断属性 'name' 是否在对象 obj 内

obj.hasOwnPropety('name')  //判断属性 'name' 属于对象 obj ,还是属于原型
```

### 增加 / 修改属性

可以直接赋值

```
let obj = {name:'ergou'}
obj.name = 'ergou'

//此时若声明一个变量值为'name'那么这个变量作为属性名指向的属性值也是‘ergou’

let key = 'name'
obj[key] = 'ergou'

Object.assign(obj,{age:18,国籍:'中国'}) //可以对上面的对象 obj 批量增加多个属性
```

修改或者增加共有属性

```
obj.toString = 'x'  //这个只会作用在一个对象身上，无法通过自身修改增加共有属性

//下面的两种可以修改共有属性，【一般还是轻易不要更改】
Object.prototype.toString = 'x'
obj.__proto__.toString = 'x'
//不建议直接引用 __proto__,因为不是所有浏览器的隐藏属性都叫'__proto'
```

修改隐藏属性

```
let common = {性别:'男',民族:'汉'} //声明这个隐藏属性
let obj = Object.create(common) //将这个隐藏属性 common 通过 Object.create 赋予给对象 obj

//这样obj就被赋予了新的隐藏属性，之后可以再向 obj 内写入值
```

![示例](/img/示例.png)
