## CSS(Cascading style sheets) 层叠样式表

### 兼容处理

- `-webkit-`
- `-moz-`
- `-ms-`

### 工具

- `sass`
- `less`
- `autoprefix`

### 选择器

- 元素
- 类
- id
- 属性选择器
- :first-child
- :nth-child

### 边框

- `border-radius`
  
  ```
  border-top-left-radius
  border-top-right-radius
  border-bottom-right-radius
  border-bottom-left-radius
  ```

- `box-shadow` 阴影
- `border-image`

### 背景

- `background-position`
- `background-repeat`

- `background-image`
- `background-size`
- `background-origin`: content-box/padding-box/border-box 图片位置区域
- `background-clip`

### 字体

- `@font-face`

    ```
    @font-face {
        font-family: '自定义字体名称',
        url()
    }
    ```

- `font-family`
- `font-size`
- `font-weight`

### `Float` 浮动

- `left`
- `right`

**Notice**

- 作用元素 块元素
- 清除浮动


### `position` 定位

- `static`
- `relative`
- `absolute`
- `sticky`

**使用场景**

- 弹窗
- 广告
- 悬浮按钮

### flexbox（弹性布局）

- `flex`
- `flex-direction`
- `flex-wrap`
- `justify-content`
- `align-items`
- `order`
- `flex-grow` 放大比例
- `flex-shrink` 缩小比例


**场景**

- 水平居中
- 垂直居中
- 水平+垂直居中
- 排列（九宫格）
- 自适应
- 布局

### box-sizing

- 内/外边框

### 渐变

- `[repeating-]linear-gradient` 线性渐变
- `[repeating-]radial-gradient` 径向渐变

### 文本

- 单词截断
- 换行

### 特效

- animation & @keyframes
    
    ```
    @keyframes some {

        from: {

        }
        to: {

        }
    }

    div {
        animation: some 10s
    }
    ```

- transform

    ```
    div {
        transform: rotateX/rotateY(120deg)
    }
    ```

### `@media`

    ```
    @media screen and (min-width: 900px) {
    article {
        padding: 1rem 3rem;
    }
    }
    ```

### `@import`

