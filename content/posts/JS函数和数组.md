---
title: "JS函数和数组"
date: 2020-03-02T21:27:22+08:00
draft: false
---

## 创建一个数组

- 新建数组

```
let arr = [1,2,3]

let arr = newArray(1,2,3)

let arr = newArray(3)  //当只有一个参数时，只会定义数组的长度

```

- 数组转化

```
let arr = '1,2,3'.split(',')

let arr = '123'.split('')
let arr = 'abcde'.split('')//将字符串转化为数组

Array.from('123')
Array.from({0:'a',1:'b',2:'c',3:'d',length:4)}//可以将一个属性名为0 1 2 3 的对象，加上长度后转化为数组。
//如果 0 1 2 3 之中缺少一个属性名，那么会自动补上一个值为 undefined 的属性名
```

- 伪数组

```
// 没有数组共同属性的数组，即是伪数组
array = {0:'a',1:'b',2:'c',3:'d',length:4}
```

- 合并两个数组

```
arr1.concat.arr2
```

- 截取数组的一部分

```
arr1.slice(1) //从数组 arr1 中第二个元素开始，截取一个元素。不会影响原先的数组
arr1.slice(0) //全部截取（也是复制一个数组的方式）
```

## 数组元素的增删改查

### 删除元素

```
let arr = [1,2,3]
delete arr[0]
//删除第一个数值，但是会保留这个数值的位置，长度依然不变。
//数字小于长度的数组成为稀疏数组

//改变数组的length
let arr = [1,2,3,4,5]
arr.length = 1
arr = [1]  //如此直接定义长度，会让后面的数字消失。
```

正确的方法

```
arr.shift() //删除头部元素，并且返回被删除的元素

arr.pop() //删除尾部元素，并且返回被删除元素

arr.splice(index,x) //自第 index个数字起，删除 x 个元素

arr.splice(index,1,'x') // 将第 index 个元素替换为 'x'

arr.splice(index,1,'x','y') //删除第 index 个元素，更换为 'x','y'
```

### 查看数组内元素

查看所有的属性名（和对象查看方式相似）

```
let arr = [1,2,3,4,5];
arr.x = 'xxx' //在 arr 里面添加一个名为 x ，值伪 'xxx' 的元素

Object.keys(arr) //打印出数组的名，结果为: 0,1,2,3,4,x

for (let key in arr){
    console.log(`${key} : ${arr[key]}`)
}
// in 是指自动遍历所有的 key ，取值最大为数组长度，所以最后一个值会有 bug。 '$' 表示后面跟可以跟变量
```

查看数字（字符串）属性名和值

```
//采用 for 循环
for (let i = 0; i<arr.length ; i++){
    console.log(`$[i] : ${arr[i]}`)
}

arr.forEach(function( item,index ){
    console.log(`${index} : ${item}`)
})

//forEach 函数详情
function forEach(array , fn){
    for(let i = 0; i<array.length; i++){
        fn(array[i],i,array)
    }
}// 定义函数：forEach 输入数组 和函数，
forEach(['a','b','c'],function(x,y,z){
    console.log(x,y,z)
}) //调用函数

//for 循环相比较 forEach ，中途可以通过break 或 continue 终止循环
```

查看单个属性

```
let arr = [1,2,3]
arr[0] = 1

arr[arr.length] === undefined//当索引的值超出数组的范围时，会返回值 undefined

arr.indexOf(item) //查看元素 item 是否在数组里，是的话返回索引，否返回-1

arr.find(item => item%2===0)//条件索引。找到第一个偶数
arr,findIndex(item => item%2 === 0)// 找到第一个偶数的编号
```

### 增加数组的元素

在尾部增加元素

```
arr.push(newItem)
arr.push(item1,item2)
//在尾部增加元素，并且返回新的长度

arr.unshift(newItem)
arr.unshift(item1,item2)
//在头部增加元素

arr.splice(index,0,'x','y')
// 在index处，删除 0个元素，添加'x' 和 'y'
```

修改顺序

```
arr.reverse() //反转数组arr 的顺序


let arr = [1,2,3,4,5,6,7]
arr.sort(function(a,b){
    if(a>b){return 1}
    else if( a===b ){return 0}
    else{return -1}
})     //比较 a b 的大小，若a>b，返回1，a=b,返回 0 ，a<b 返回-1. 按照返回值由小到大排序，排序结果为从小到大。  更改return 值即可完成逆排序


let arr = [ {name:'小明',score:99} ,{name: '小红',score:97},{name: '小花',score:88}]
arr.sort(function(a,b){
    if(a.score > b.score){return 1}
    else if(a.score === b.score){return 0}
    else{return -1}
})
//简写为：

arr.sort((a,b) => a.score - b.score)
//判断 a b 两者分数的差，默认小的排在前面


let s = 'a,b,c,d,e'
s.split('')

s.split('').reverse()

s.split('').reverse().join('')
//将字符串重新排序
```

## 数组变换

map filter reduce 这三个变换不会影响到原先的数组

map n=>n

```
arr.map( item => item*item )   //将 arr 内的每个 item 取平方


let arr = [0,1,2,2,3,3,3,4,4,4,4,6]
let arr2 = arr.map( index =>
    {return {0:'周日',1:'周一',2:'周二',3:'周三',4:'周四',5:'周五',6:'周六'}[index]}

)
console.log(arr2) // ['周日', '周一', '周二', '周二', '周三', '周三', '周三', '周四', '周四', '周四', '周四','周六']

```

filter n 变少

```
arr.filter( item => item %2 ===0 ? true : false )
//判断 item 是否可被 2 整除，保留 true ，删除 false
// item%2 === 0 ?  自会返回 true 和 false值，所以后面的呢 true:false 可以省略
```

reduce n 变 1

```
arr.reduce((sum,item) => {return sum+item} , 0 )
//初始的 sum 为 0，将 sum+item 作为新的 sum 再和下一个 item 相加。


arr.reduce((result,item) => {return result.concat( item*item )}, [] )
//初始为空数组 []，将 result和item*item 结合成为新的数组，再和下一个 item*item 结合成新数组，最终得到原先数组每个 item 的平方



arr.reduce( (result,item) =>{
    if(item%2===0){return result.concat(item)}
    else{return  result}
} ,[])


// 简写为：

arr.reduce((result,item) => result.concat(item%2===0? item : []),[])
//初始result为 [] 数组 , 如果 item整除2，就concat(item), 否则 concat([]), 这样就可以筛选出数组中的偶数
```

##### ending
