##### 判断当前环境是否是浏览器

```
/**
 * 判断当前环境是否是浏览器
 */
const isBrowser = () => typeof window !== 'undefined';

```

##### 判断对象是否有原型属性

```
/**
 * 判断对象是否有原型属性
 */
const hasProto = (obj) => '__proto__' in obj;
```

##### 获取浏览器的用户代理

```
/**
 * 获取浏览器的用户代理
 */
const getUserAgent = () => isBrowser() && window.navigator.userAgent.toLowerCase();
```

##### 判断是否是 IE 浏览器

```
/**
 * 判断是否为IE浏览器
 */
const isIE = () => getUserAgent() && /msie|trident/.test(getUserAgent());
```

##### 判断浏览器是否为 IE9

```
/**
 * 判断浏览器是否为IE9
 */
const isIE9 = () => getUserAgent() && getUserAgent().indexOf('msie 9.0') > 0;
```

##### 判断浏览器是否为 Edge

```
/**
 * 判断浏览器是否为Edge
 */
const isEdge = () => getUserAgent() && getUserAgent().indexOf('edge/') > 0;
```

##### 判断浏览器是否为 Chrome

```
/**
 * 判断浏览器是否为Chrome
 */
const isChrome = () => getUserAgent() && /chrome\/\d+/.test(getUserAgent()) && !isEdge();
```

##### 判断字符串是否以某字符开头

```
/**
 * 判断字符串是否以某字符开头
 * @param {*} str
 * @param {*} char
 */
const isStartWithSomeChar = (str, char) => {
  return (char + '').charCodeAt(0) === (str + '').charCodeAt(0);
}
```

##### 连字符转驼峰

```
/**
 * 连字符转驼峰
 * @param {*} str
 */
const hyphenToHump = (str) => {
  return str.replace(/-(\w)/g, (_, c) => c ? c.toUpperCase() : '')
}

```

##### 变量转字符串

```
/**
 * 变量转字符串
 * @param {*} val
 */
const transString = (val) => {
  return val == null ?
    '' :
    typeof val === 'object' ?
    JSON.stringify(val, null, 2) :
    String(val)
}

```

##### 合并到某个数组

```
/**
 * 合并到某个数组
 * @param {*} parentVal []
 * @param {*} childVal  []|string
 */
const mergeToArr = (parentVal, childVal) => {
  return childVal ?
    parentVal ?
    parentVal.concat(childVal) :
    Array.isArray(childVal) ?
    childVal : [childVal] : parentVal
}

```

##### 首字符大写

```
/**
 * 首字母大写
 * @param {*} str
 */
const capitalizeFirstChar = (str) => {
  return str.charAt(0).toUpperCase() + str.slice(1)
}

```

##### 驼峰转连字符

```
/**
 * 驼峰转连字符
 * @param {*} str
 */
const humpToHyphen = (str) => {
  return str.replace(/\B([A-Z])/g, '-$1').toLowerCase();
}
```

##### 判断变量是否为原型类型

```
/**
 * 判断变量是否为原型类型
 * @param {*} value
 */
const isPrimitive = (value) => {
  return (
    typeof value === 'string' ||
    typeof value === 'number' ||
    typeof value === 'symbol' ||
    typeof value === 'boolean'
  )
}

```

##### 判断变量是否为正则对象

```
/**
 * 判断变量是否为正则对象
 * @param {*} val
 */
const isRegExp = (val) => {
  return Object.prototype.toString.call(val) === '[object RegExp]';
}
```

##### 判断变量是否含有效的数组索引

```
/**
 * 判断变量是否含有效的数组索引
 * @param {*} val
 */
const isValidArrayIndex = (val) => {
  let n = parseFloat(String(val));
  return n >= 0 && Math.floor(n) === n && isFinite(val);
}

```

##### 判断是否为对象

```
/**
 * 判断是否为对象
 * @param {*} obj
 */
const isObject = (obj) => {
  return obj !== null && typeof obj === 'object'
}

```

##### 返回一个判断变量是否包含在传入字符串里的函数

```
/**
 * 返回一个判断变量是否包含在传入字符串里的函数
 * @param {*} str
 * @param {*} expectLowerCase
 */
const makeObj = (str, expectLowerCase) => {
  const obj = Object.create(null);
  const list = str.split(',');
  for (let i = 0; i < list.length; i++) {
    obj[list[i]] = true
  }
  return expectLowerCase ?
    val => obj[val.toLowerCase()] :
    val => obj[val]
}
```

##### 返回调用一次的函数

```
/**
 * 返回调用一次的函数
 * @param {*} func
 */
const onceFunc = (func) => {
  let called = false
  return function () {
    if (!called) {
      called = true
      func.apply(this, arguments)
    }
  }
}
```

##### 创建一个缓存函数

```
/**
 * 创建一个缓存函数
 * @param {*} fn
 */
const cached = (fn) => {
  var cache = Object.create(null)
  return function cachedFn(str) {
    var hit = cache[str]
    return hit || (cache[str] = fn(str))
  }
}
```

##### 判断两个变量是否相等

```

/**
 * 判断两个变量是否相等
 * @param {*} a
 * @param {*} b
 */
const looseEqual = (a, b) => {
  // 当 a === b 时，返回true
  if (a === b) return true
  // 否则进入isObject判断
  const isObjectA = a !== null && typeof a === 'object'
  const isObjectB = b !== null && typeof b === 'object'
  // 判断是否都为Object类型
  if (isObjectA && isObjectB) {
    try {
      // 调用 Array.isArray() 方法，再次进行判断
      // isObject 不能区分是真数组还是对象（typeof）
      const isArrayA = Array.isArray(a)
      const isArrayB = Array.isArray(b)
      // 判断是否都为数组
      if (isArrayA && isArrayB) {
        // 对比a、b数组的长度
        return a.length === b.length && a.every((e, i) => {
          // 调用 looseEqual  进入递归
          return looseEqual(e, b[i])
        })
      } else if (!isArrayA && !isArrayB) {
        // 均不为数组，获取a、b对象的key集合
        const keysA = Object.keys(a)
        const keysB = Object.keys(b)
        // 对比a、b对象的key集合长度
        return keysA.length === keysB.length && keysA.every(key => {
          //长度相等，则调用 looseEqual  进入递归
          return looseEqual(a[key], b[key])
        })
      } else {
        // 如果a、b中一个是数组，一个是对象，直接返回 false
        return false
      }
    } catch (e) {
      return false
    }
  } else if (!isObjectA && !isObjectB) {
    return String(a) === String(b)
  } else {
    return false
  }
}

```
