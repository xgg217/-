# 节流

## 原理

+ 如果你持续触发事件，每隔一段时间，只执行一次事件

## 实现方法1：使用时间戳

+ 事件回立刻执行

+ 同时在停止触发后没有办法再执行

  ```js
  /**
   * wait 毫秒 相隔多久触发一次
    */
  function throttle(func, wait) {
    "use strict";
    let st = Date.now(); // 开始时间
    let that = null;
    return function(...args) {
      that = this;
      const end = Date.now();
      if((end + st) > wait) {
        func.apply(that, args);
        st = end;
      }
    }
  }
  ```

## 实现方法2：使用定时器

+ 会在 n 秒后第一次执行

+ 事件停止触发后依然会再执行一次事件

  ```js
  function throttle(func, wait) {
    "use strict";
    let timeout = 0;
    let that = null;
    return function(...args) {
      that = this;
      if(!!timeout) {
        return
      }
      // 能走到这一步，证明上一次定时器已经执行完成
      timeout = setTimeout(function() {
        console.log(timeout);
        timeout = 0;
        func.apply(that, args);
      }, wait);
    }
  }
  ```

## 实现方法3

+ 设置可以禁用第一次执行

+ 设置禁用停止触发的回调

+ 设置可以取消

  ```js
  // 鼠标移入能立刻执行，停止触发的时候还能再执行一次！
  // leading：false 表示禁用第一次执行
  // trailing: false 表示禁用停止触发的回调
  function throttle(func, wait, { leading= true, trailing = true } = {}) {
    let that = null;
    let timeout = 0; // 时间戳ID
    let st = 0; // 开始时间
    let args = [];

    const later = function() {
      st = (leading === false) ? 0 : Date.now();

      timeout = 0;
      func.apply(that, args);
      if (!timeout) {
        args = [];
        that = null;
      }
    };

    const throttled = function(...arg) {
      that = this;
      let end = Date.now();
      args = arg;

      //下次触发 func 剩余的时间
      const remaining = wait + (end + st);

      if(!st && (leading === false)) {
        st = end;
      }
      if(!timeout && (trailing !== false)) {
        timeout = setTimeout(later, remaining);
        return
      }

      // 如果没有剩余的时间了或者你改了系统时间
      if((remaining <= 0) || (remaining > wait)) {
        if(timeout) {
          clearTimeout(timeout);
          timeout = 0;
        }

        st = end;
        func.apply(that, args);
        if (!timeout) {
          args = [];
          that = null;
        }
      }
    };

    // 取消--暂时不知道啥用处
    throttled.cancel = function() {
      clearTimeout(timeout);
      st = 0;
      timeout = null;
    }

    return throttled
  }
  ```

+ 使用

  ```js
  const div3 = document.querySelector(".div4");

  const dq = function() {
    console.log(this);
    console.log("调用4");
  };

  const aa = throttle(dq, 2000, { leading: false, trailing: true });
  div3.addEventListener("mousemove", aa);

  setTimeout(() => {
    console.log("取消");
    aa.cancel();
  }, 10000);
  ```
