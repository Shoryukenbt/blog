---
title: Tips
date: 2019-05-05 15:05:52
tags: js css html
---

### CSS
#### 1. 排版
正常流的排版行为可以用**一次排列，空间不足换行**来总结，在CSS标准中规定了如何排布一个盒或者文字的算法，这个算法依赖排班的当前状态， 这个当前状态就是**格式化上下文(formatting context)**, 可以这样认为:
> 格式化上下文 + 盒 / 文字 = 位置
需要排版元素（盒/文字）根据其行为分为**行内元素**和**块级元素**，排版分别为他们规定了**块级格式化上下文(BFC)**和**行内及格式化上下文(IFC)**, 当把正常流中的元素排版时就会有这三种情况，可以将一个块级格式化上下文中的排版规则分为三种情况：
  * **遇到块级盒** -> 排入当前块级格式化上下文
  * **遇到行内级盒或者文字** -> 如果当前行内级格式化上下文可以排下，直接排入当前行内级格式化上下文；如果排不下，会创建一个行盒(行盒是一个块级，按照上述排版)，然后行盒会创建一个行内级格式化上下文
  * **遇到float盒** -> 会把喝的顶部和当前行内级上下文的上边缘对其， 再根据其方向将对应边与块级格式化上下文的边缘对齐， 然后重排当前行盒

  ##### 新建BFC
实际上页面中的布局远比这复杂， 有些元素还会在其内部创建新的块格式化上下文
  * 浮动定位元素
  * 绝对定位元素
  * 能包含块级元素的非块级容器(inline-block, table-cell等)
  * overflow不为visible的能包含块级元素的块级容器

  ##### 正常流实用技巧
  * 等分布局问题
  * 自适应宽
#### 2. flex布局

### JS
#### 1. 判断对象类型的方法
* 普通对象可以通过`instanceOf`，`Object.prototype.toString`来判断
* 对于基本类型和function可以通过`typeof`来判断
* NaN 可以用es6提供的方法`Number.isNaN`, 和*NaN*的特性自身不相等`obj !== obj`来判断
* Array类型还可以用`Array.isArray`来判断

#### 2. JS运行机制

### Vue
#### 1. Vue中computed,methods,watch的特点区别以及各自的适用场景
#### 2. Vuex
#### 3. Vue-router
#### 4. 虚拟DOM, 为什么比直接操纵DOM快

### React
#### 1. React中的state和props
#### 2. Redux
#### 3. Reat-router