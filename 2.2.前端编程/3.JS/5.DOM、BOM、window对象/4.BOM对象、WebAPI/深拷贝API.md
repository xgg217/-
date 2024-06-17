# 深拷贝

## 概述

+ `structuredClone` 浏览器内置

## 语法

+ `structuredClone(value)`

+ `structuredClone(value, { transfer })`

+ 示例

  ```js
  const original = { name: "MDN" };
  original.itself = original;

  // 深拷贝
  const clone = structuredClone(original);

  console.log(clone !== original); // true
  console.log(clone.name === "MDN"); // true
  console.log(clone.itself === clone); // true
  ```
