# 避坑Tip
JS 代码可以不在最后加分号，但有一点需要注意，如果某一行代码涉及利用解构赋值进行变量交换，它的上一行代码必须有分号
```js
let a = 1
let b = 2
// do something
console.log(a, b)
[a, b] = [b, a]
console.log(a, b)
```
如果你觉得上面代码没问题，那事可大了
```js
[a, b] = [b, a]
       ^
TypeError: Cannot set properties of undefined (setting '2')
    at Object.<anonymous> (C:\Users\16000\Desktop\practice-webpack\src\index.js:5:8)
    at Module._compile (node:internal/modules/cjs/loader:1101:14)
    at Object.Module._extensions..js (node:internal/modules/cjs/loader:1153:10)
    at Module.load (node:internal/modules/cjs/loader:981:32)
    at Function.Module._load (node:internal/modules/cjs/loader:822:12)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:79:12)       
    at node:internal/main/run_main_module:17:47
```
由于[没有分号](https://zh.javascript.info/structure#semicolon)，JS 会把 `console.log(a, b)` 和 `[a, b] = [b, a]` 当成同一行处理，报错是不可避免的。一个有效的解决办法如上所说，在解构赋值进行变量交换的上一行末尾添加分号
```js
let a = 1
let b = 2
// do something
// extra semicolon
console.log(a, b);
[a, b] = [b, a]
console.log(a, b)
```

# 常用函数

包括数组求最大最小值、求和

```js
// 函数式
const max = arr => {
  return Math.max.apply(null, arr)
}
const sum = arr => {
  return arr.reduce((pre, cur) => pre + cur)
}

// 方法式
Array.prototype.max = function () {
  return Math.max.apply(null, this)
}
Array.prototype.sum = function () {
  return this.reduce((pre, cur) => pre + cur)
}
```

# 巧用位运算

- 判断一个整数 `x` 的奇偶性：`x & 1 = 1 (奇数) ， x & 1 = 0 (偶数)`

  求一个浮点数 `x` 的整数部分：`~~x`，对于正数相当于 `floor(x)` 对于负数相当于 `ceil(-x)`

  计算 `2 ^ n`：`1 << n` 相当于 `pow(2, n)`

  计算一个数 `x` 除以 2 的 n 倍：`x >> n` 相当于 `~~(x / pow(2, n))`

  判断一个数 `x` 是 2 的整数幂（即 x = 2 ^ n）: `x & (x - 1) = 0`

  ※注意※：**上面的位运算只对32位带符号的整数有效，如果使用的话，一定要注意数！据！范！围！**

  记住这些技巧的作用：

  提升运行速度 ❌

  提升逼格 ✅

  举一个实用的例子，快速幂（原理自行google）

  ```js
  // 计算x^n n为整数
  function qPow(x, n) {
      let result = 1;
      while (n) {
          if (n & 1) result *= x; // 同 if(n%2)
          x = x * x;
          n >>= 1; // 同 n=floor(n/2)
      }
      return result;
  }
  ```
