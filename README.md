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
