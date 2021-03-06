---
title: "JS的基本语法"
date: 2020-02-28T22:31:00+08:00
draft: false
---

# JS 基本语法

### 表达式和语句

语句是为了完成某种人物的操作，一般会改变环境变量，例如声明或者赋值等。语句以分号结尾，标志一句结束。

而表达式则是类似于 1+3 这种为了得到返回值的计算式。

语句和表达式的区别在于语句是为了进行某种操作，一般情况下不需要返回值；而表达式则是为了得到返回值，所以一定有一个返回值出现。

### 书写规范

在 JS 当中大小写是非常敏感的，需要注意两者的区别。而空格和回车对整体代码没有影响，可以适当添加让代码更加清晰。不过需要注意的一个地方就是 return 的后面不能添加回车。

不需要没条代码都写上注释，则重挑选记录便可。

可以使用 { } 将代码放在一起组合成代码块，常与 if/while/for 等语句合用。

### 标识符

即用来规定各种名称的合理写法，例如变量名或者函数名等。

在命名的时候可以 除数字之外的字母 、中文 或者 '\$' / '\_'开头，第二位及以后就可使用数字。也可以使用中文作为合法标识符。

### 常见的基础语句

#### if...else...

语法规则为

    if(表达式)
    {
     语句1
     }else{ 语句2 }

[语句 1 在只有一句话的时候可以省略 { } ，不过以防产生歧义，还是写完整比较好]

#### switch

适用于多层判断结构。语法结构为：

    switch ( fruit ){
    case 'banana':
    console.log( 'banana' );
    break;
    case 'apple':
    console.log( 'apple' );
    break;
    default:
    console.log( 'none' );
    }

[`break`记得要写上，不然代码有可能一直执行下去]
还有几种类似的逻辑判断语句

- 表达式 1 ? 表达式 2 : 表达式 3

  - 意为判断表达式 1，如果值为 true，则执行表达式 2，否则执行表达式 3
  - 可以用来代替 if else 结构

- A && B && C && D
  - 如果 A 正确就取 B，B 正确再执行 C，C 正确再取 D. 即取第一个假值，或者执行 D。
- A || B || C || D
  - 和上面那个相反，取第一个真的值，或者 D

#### while 循环

语法为：

```
while( 表达式 )
{ 语句 }
```

意为：判断表达式的真假，如果为真，执行语句，之后再判断表达式的真假；当表达式为假则执行之后的语句。

#### for 循环

为 `while`的简单写法，语法为：

```
for(语句1;表达式2;语句3){
循环体
}
```

先执行语句 1，然后判断表达式 2，如果为真，那么执行循环体，再执行语句 3；如果为假就直接退出循环，执行之后的语句。

#### break 和 continue

break 用于退出所有的循环.

continue 则用于推出当前一次循环。

break：

```
for (var i = 0; i < 5; i++) {
  console.log(i);
  if (i === 3)
    break;
}
```

这段代码再执行到 i=3 的时候，就会终止循环。

continue：

```
var i = 0;
while (i < 100){
  i++;
  if (i % 2 === 0) continue;
  console.log('i 当前为：' + i);
}
```

在 i 为偶数的时候，就会执行 continue，跳出当前循环直接执行下一轮。

#### label 标签

标签格式如下：

    label:
      语句

标签可以是任意标识符，但不能是保留字，语句可以是任意语句。
也可以用于跳出代码块

```
foo: {
  console.log(1);
  break foo;
  console.log('本行不会输出');
}
console.log(2);
```

在执行到 break foo 的时候，就会跳出区块。
