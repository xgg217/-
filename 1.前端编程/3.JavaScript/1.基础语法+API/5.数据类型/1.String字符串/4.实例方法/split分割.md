# split

## API

+ `split(separator)`
+ `split(separator, limit)`

  + 参数

    + separator

      + 指定分隔符，可以是字符串或正则表达式

        ```js
        'a|b|c'.split('|') // ["a", "b", "c"]
        ```

      + 如果省略，则返回整个字符串作为数组

        ```js
        'a|b|c'.split('') // ["a", "|", "b", "|", "c"]
        ```

      + 可以是 `undefined` 、 字符串或者一个具有 `Symbol.split` 方法的对象

    + limit `[可选]` 整数，限制返回的数组的最大长度。如果超过限制，多余的部分将被忽略

      ```js
      'a|b|c'.split('|', 0) // []
      'a|b|c'.split('|', 1) // ["a"]
      'a|b|c'.split('|', 2) // ["a", "b"]
      'a|b|c'.split('|', 3) // ["a", "b", "c"]
      'a|b|c'.split('|', 4) // ["a", "b", "c"]
      ```

  + 返回值



## 注意点

+ `split` 方法按照给定规则分割字符串，返回一个由分割出来的子字符串组成的数组

  ```js
  'a|b|c'.split('|') // ["a", "b", "c"]
  ```

+ 如果分割规则为空字符串，则返回数组的成员是原字符串的每一个字符

  ```js
  'a|b|c'.split('') // ["a", "|", "b", "|", "c"]
  ```

+ 如果省略参数，则返回数组的唯一成员就是原字符串

  ```js
  'a|b|c'.split() // ["a|b|c"]
  ```

+ 如果满足分割规则的两个部分紧邻着（即中间没有其他字符），则返回数组之中会有一个空字符串

  ```js
  'a||c'.split('|') // ['a', '', 'c']
  ```

+ 如果满足分割规则的部分处于字符串的开头或结尾（即它的前面或后面没有其他字符），则返回数组的第一个或最后一个成员是一个空字符串

  ```js
  '|b|c'.split('|') // ["", "b", "c"]
  'a|b|'.split('|') // ["a", "b", ""]
  ```

## 踩坑点

+ 空字符串的分割

  ```js
  const result = "".split(",");
  console.log(result);
  // 输出: [''] （非空数组，包含一个空字符串）
  ```

  + 原因：空字符串没有内容，split() 默认返回一个数组，包含原始字符串

  + 解决方案：

    ```js
    const result = "".split(",").filter(Boolean);
    console.log(result);
    // 输出: [] （使用 filter 移除空字符串）
    ```

+ 多余分隔符

  ```js
  const text = ",,苹果,,华为,,";
  const result = text.split(",");
  console.log(result);
  // 输出: ['', '', '苹果', '', '华为', '', '']
  ```

  + 原因：连续的分隔符会在数组中插入空字符串

  + 解决方案：

    ```js
    const text = ",,苹果,,华为,,";
    const result = text.split(",").filter(Boolean);
    console.log(result);
    // 输出: ['苹果','华为']
    ```

+ 分割 Unicode 字符

  ```js
  const text = "👍😊👨‍👩‍👦";
  const result = text.split('');
  console.log(result);
  // 输出: ['👍', '😊', '👨', '‍', '👩', '‍', '👦']
  ```

  + 原因：split("") 按字节分割，无法正确识别组合型字符

  + 解决方案：

    ```js
    const text = "👍😊👨‍👩‍👦";
    const result = Array.from(text);
    console.log(result);
    // 输出: ['👍', '😊', '👨‍👩‍👦'] （完整分割）
    ```
