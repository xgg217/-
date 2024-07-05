# ArrayBuffer.isView()

## 概述

+ `ArrayBuffer.isView(value)` 静态方法判断传入值是否是 ArrayBuffer 视图之一，例如 `TypedArray` 对象或 `DataView`

  + 参数

    + value 要检查的值

  + 返回值

    + 如果给定参数是 `ArrayBuffer` 视图之一则返回 `true` ；否则返回 `false`

## 示例

+ code

  ```js
  ArrayBuffer.isView(); // false
  ArrayBuffer.isView([]); // false
  ArrayBuffer.isView({}); // false
  ArrayBuffer.isView(null); // false
  ArrayBuffer.isView(undefined); // false
  ArrayBuffer.isView(new ArrayBuffer(10)); // false

  ArrayBuffer.isView(new Uint8Array()); // true
  ArrayBuffer.isView(new Float32Array()); // true
  ArrayBuffer.isView(new Int8Array(10).subarray(0, 3)); // true

  const buffer = new ArrayBuffer(2);
  const dv = new DataView(buffer);
  ArrayBuffer.isView(dv); // true
  ```
