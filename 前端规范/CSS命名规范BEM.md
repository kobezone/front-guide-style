# CSS BEM 命名规范
## 使用BEM命名规范，理论上讲，每行 css 代码都只有一个选择器。
## BEM代表“块（block）,元素（element）,修饰符（modifier）”,我们常用这三个实体开发组件。
在选择器中，由以下三种符合来表示扩展的关系：

>
* `-`  中划线 ：仅作为连字符使用，表示某个块或者某个子元素的多单词之间的连接记号。
* `__`  双下划线：双下划线用来连接块和块的子元素
* `_`   单下划线：单下划线用来描述一个块或者块的子元素的一种状态

`type-block-name__element-name_modifier`    
`B__E_M`


### 块（block）


一个块是设计或布局的一部分，它有具体且唯一地意义 ，要么是语义上的要么是视觉上的。
在大多数情况下，任何独立的页面元素（或复杂或简单）都可以被视作一个块。它的HTML容器会有一个唯一的CSS类名，也就是这个块的名字。
针对块的CSS类名会加一些前缀（ ui-），这些前缀在CSS中有类似 命名空间 的作用。
一个块的正式（实际上是半正式的）定义有下面三个基本原则：
CSS中只能使用类名（不能是ID）。
每一个块名应该有一个命名空间（前缀）
每一条CSS规则必须属于一个块。
例如：一个自定义列表 .list 是一个块，通常自定义列表是算在 mod 类别的，在这种情况下，一个 list 列表的block写法应该为:
```css
 .list
```

### 元素（element）
块中的子元素是块的子元素，并且子元素的子元素在 bem 里也被认为是块的直接子元素。一个块中元素的类名必须用父级块的名称作为前缀。
如上面的例子，li.item 是列表的一个子元素，
```css
.list{}
.list .item{}

.list{}

.list__item{}
```

### 修饰符（modifier）

一个“修饰符”可以理解为一个块的特定状态，标识着它持有一个特定的属性。
用一个例子来解释最好不过了。一个表示按钮的块默认有三个大小：小，中，大。为了避免创建三个不同的块，最好是在块上加修饰符。这个修饰符应该有个名字（比如：size ）和值（ small，normal 或者 big ）。
如上面的例子中，表示一个选中的列表，和一个激活的列表项
```css
.list{}
.list.select{}
.list .item{}
.list .item.active{}


.list{}
.list_select{}
.list__item{}
.list__item_active{}
```

### 关于书写原则
#### 1. 原则上不会出现 **2层以上** 选择器的嵌套
使用BEM原则，用命名来解耦，所有类名都为一层，增加效率和复用性

#### 2. 两侧选择器嵌套.block-name__element--modifier 子元素的情况
推荐使用内部嵌套和SASS书写
常规写法：
 ```css
.xxx{}
.xxx__item{}
.xxx__item_current{}
// 嵌套写法
.xxx__item_current .mod-xxx__link{}
```
推荐
```css
.xxx{}
.xxx__item{}
.xxx__item_current{}

.xxxx__item_current{
    .xxx__link{}
}

```

### 例子
```html
<ul class="xxx">
    <li class="xxx__item">第一项
        <div class="xxx__product-name">我是名称</div>
        <span class="xxx__ming-zi-ke-yi-hen-chang">看类名</span>
        <a href="#" class="xxx__link">我是link</a>
    <li>
    <li class="xxx__item xxx__item_current">第二项 且 当前选择项
        <div class="xxx__product-name">我是名称</div>
        <a href="#" class="xxx__item-link">我是link</a>
    <li>
    <li class="xxx__item xxx__item_hightlight">第三项 且 特殊高亮
         <div class="xxx__product-name">我是名称</div>
        <a href="#" class="xxx__item-link">我是link</a>
    <li>
</ul>
```

推荐写法
```css

.xxx{}
.xxx__item{}
.xxx__product-name{}
.xxx__item_current{}

.xxx__item-link{}

.xxx__item_current .xxx__item-link{}


// 使用sass 如下: 推荐
.xxx{
    &__item{
        &_current{

        }
        &-link{

        }
    }

    &__ming-zi-ke-yi-hen-chang{

    }
    &__link{

    }
}


```