### 优雅的取数值的整数和小数部分

#### 1 parseInt
```javascript
    console.log(parseInt(3.1)); // 3
```
**parseInt(string, radix)**
 将字符串转换成整数的方法，如果参数不是字符串，先将其转换成字符串。
 string: 要转换的字符串；
 radix：进制，默认是十进制
 parseInt(3.1) 先将3.1转换成字符串类型'3.1'

 所以用parseInt方法取整数，有两个不好的地方，一是parseInt这个函数名，看起来就是将字符串转整数的，用在这里不是很适合，另一个是转字符串有点多此一举，而且肯定会带来性能开销，所以使用parseInt虽然方便，但不是最好的办法

```javascript
console.log(parseInt(0.00000001)); // 1
console.log(parseInt(1000000000000000000000)); // 1
```

JS中精度小于0.000001的数字会自动转化为科学计数的字符串(1e-6)。
parseInt在匹配时，如果找到了以数字开头然后开始会匹配接下来的字符，直到找到不是数字的字符结束，然后输出匹配到的数字。它能识别八进制、十六进制等，但是不识别科学计数法，而parseFloat只识别十进制，还可以识别科学计数法。对于科学计数法，parseInt和parseFloat会产生不同的输出

0.00000001.toString() === 1e-8
因为0.00000001被转换成字符串时变成"1e-8",所以变成parseInt("1e-8")

#### Math
Math.floor(向下取整) Math.ceil(向上取整) Math.round(四舍五入)

要跟 parseInt 一样的效果，负数用Math.ceil, 正数用Math.floor

 #### Math.trunc
 es2015 Math.trunc
#### tricky
```javascript
    console.log(3.75 | 0); // 3
    console.log(~~3.75); // 3
    console.log(<< 3.75); // 3
```

这是一种利用位操作来取整的手段