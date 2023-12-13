# Required

## 必填

+ 将类型 T 中的成员变成 **可选**

  ```js
  interface User {
    age: number
    name: string
  }

  const u:Partial<User> = {
    age: 12
  }
  ```

## 源码

+ 源码

  ```js
  type Required<T> = {
    [P in keyof T]-?: T[P];
  };
  ```
