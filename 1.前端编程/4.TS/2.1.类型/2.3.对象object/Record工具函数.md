# Record 工具函数

## 概述

+ 将一个类型的所有属性值都映射到另一个类型上并创造一个新的类型

## 源码

+ 源码：将 k 中的每个属性(`[P in K]`)，都转为 T 类型

  ```js
  type Record<K extends keyof any, T> = {
    [P in K]: T;
  }
  ```

+ 使用格式

  ```js
  type ProxKType = Record<K, T>
  ```

+ K可以是联合类型、对象、枚举

## 实际使用

+ `Record<string, unknown>` 和 `Record<string, any>` 是日常使用较多的形式，通常我们使用这两者来代替 `object`

## 示例1

+ 将petsGroup中的每个值(‘dog’ | ‘cat’ | ‘fish’)都转为 IPetInfo 类型

  ```js
  type petsGroup = 'dog' | 'cat' | 'fish';
  interface IPetInfo {
    name:string,
    age:number,
  }

  type IPets = Record<petsGroup, IPetInfo>;

  const animalsInfo:IPets = {
    dog:{
      name:'dogName',
      age:2
    },
    cat:{
      name:'catName',
      age:3
    },
    fish:{
      name:'fishName',
      age:5
    }
  }
  ```

+ 也可以自己在第一个参数后追加额外的值

  ```js
  type petsGroup = 'dog' | 'cat' | 'fish';
  interface IPetInfo {
    name:string,
    age:number,
  }

  type IPets = Record<petsGroup | 'other', IPetInfo>;

  const animalsInfo:IPets = {
    dog:{
      name:'dogName',
      age:2
    },
    cat:{
      name:'catName',
      age:3
    },
    fish:{
      name:'fishName',
      age:5
    },
    other: {
      name:'fishName',
      age:5
    }
  }
  ```

## 仅定义对象键和值的类型

+ 代码

  ```js
  type ProxKType = Record<string, number>

  // 相当于 使用索引签名语法
  interface: ProxKType {
    [key: string]: number
  }
  ```
