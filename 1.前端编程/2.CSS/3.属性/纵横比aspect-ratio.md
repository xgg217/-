# aspect-ratio

## 概述

+ aspect-ratio CSS 属性为 box 容器规定了一个期待的纵横比，这个纵横比可以用来计算自动尺寸以及为其他布局函数服务

## 语法

+ 值

  + `auto`

  + `width / height`

    ```css
    /* 保持原有的纵横比 */
    aspect-ratio: auto;

    aspect-ratio: 1 / 1;

    /* 纵横比为 16:9 */
    aspect-ratio: 16 / 9;
    ```

+ 任何一个具有宽高的元素都可以使用

  ```css
  div .box {
    aspect-ratio: 5 / 4;
  }
  ```

## 示例

+ 准备一个盒子，盒子里面放入图片。无论容器的宽高怎么变化，图片都能保持 1:1 的纵横比

  ```css
  .box {
    width:500px;
    height:500px;
    border:1px solid red;
    resize:both; // 图片容器设置随意缩放
    overflow:auto;
  }

  .box img {
    max-width:100%;
    max-height:100%;
    aspect-ratio:1 / 1;   /* 设置图片的纵横比为 1:1，最大高度和宽度都是容器的 100%，图片不会超出容器 */
  }
  ```
