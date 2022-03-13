# Vue3

[TOC]



## v-model （表单输入绑定）

```html
<!-- 自动将用户的输入值转为数值类型 -->
<input v-model.number="age" type="text" />
<!-- 自动过滤用户输入的首尾空白字符 -->
<input v-model.trim="msg" />
```

## v-bind
```html
<img v-bind:src="url" />
<!-- 缩写 -->
<img :src="url" />
<!-- 内联字符串拼接 -->
<img :src="'/path/to/images/' + fileName" />

<!-- 动态 attribute 名 -->
<button v-bind:[key]="value"></button>
<!-- 动态 attribute 名缩写 -->
<button :[key]="value"></button>
```

## v-for （列表渲染）

```html
<div v-for="item in items">{{ item.text }}</div>
<!-- 默认行为会尝试原地修改元素而不是移动它们 -->
<div v-for="(item, index) in items"></div>
<div v-for="(value, key) in object"></div>
<div v-for="(value, name, index) in object"></div>
<!-- 强制其重新排序元素 -->
<div v-for="item in items" :key="item.id">{{ item.text }}</div>
```

为了给 Vue 一个提示，以便它能跟踪每个节点的身份，从而重用和重新排序现有元素，你需要为每项提供一个唯一的 key attribute：
建议尽可能在使用 v-for 时提供 key attribute，除非遍历输出的 DOM 内容非常简单，或者是刻意依赖默认行为以获取性能上的提升。

```html
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```

**数组更新方法**

```js
app.items.push({ message: 'Baz' })
```

* push()
* pop()
* shift()
* unshift()
* splice()
* sort()
* reverse()


**数组替换方法**

* filter()
* concat()
* slice()

```js
example1.items = example1.items.filter(item => item.message.match(/Foo/))
```



### v-for-list

```html
<li v-for="todo in todos">{{ todo.text }}</li>
```

```js
data() {
    return {
        // 通常为空数组，通过json调用
        todos: [{
            text: 'Learn JavaScript'
        }, {
            text: 'Learn Vue'
        }, {
            text: 'Build something awesome'
        }]
    }
}
```

### v-for-indexlist

```html
<li v-for="(item, index) in items">{{ index }} - { item.message }}</li>
```

```js
data() {
    return {
        items: [{
            message: 'Foo'
        }, {
            message: 'Bar'
        }]
    }
}
```

### v-for-object

```html
<li v-for="value in myObject">
    {{ value }}
</li>
```

```js
data() {
    return {
        myObject: {
            title: 'How to do lists in Vue',
            author: 'Jane Doe',
            publishedAt: '2016-04-10'
        }
    }
}
```

### v-for-object2

```html
<li v-for="(value, name, index) in myObject">
    {{ index }}. {{ name }}: {{ value }}
</li>
```

```js
data() {
    return {
        myObject: {
            title: 'How to do lists in Vue',
            author: 'Jane Doe',
            publishedAt: '2016-04-10'
        }
    }
}
```


*** 

## v-on （事件处理）

```
1.完整写法:    v-on:click
2.简写：       @click
3.动态参数简写: @[event]
```
```
@click
@submit
@scroll
```

按键
```html
<!-- 只有在 `key` 是 `Enter` 时调用 `vm.submit()` -->
<input @keyup.enter="submit" />
```

```
# 按键别名
.enter
.tab
.delete (捕获“删除”和“退格”键)
.esc
.space
.up
.down
.left
.right

# 系统修饰符
.ctrl
.alt
.shift
.meta

# 精准修饰符
.exact

# 鼠标按钮修饰符
.left
.right
.middle
```


```html
<button @click="counter += 1">Add 1</button>
<!-- 内联语句（带参） -->
<button @click="say('hi')">Say hi</button>
<!-- 内联语句 特殊变量 $event 把它传入方法 -->
<button @click="warn('Form cannot be submitted yet.', $event)">Submit</button>
<!-- 多事件处理 -->
<button @click="one($event), two($event)">Submit</button>

<!-- 有且只有 Ctrl 被按下的时候才触发 -->
<button @click.ctrl.exact="onCtrlClick">A</button>
<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
<!-- Alt + Enter -->
<input @keyup.alt.enter="clear" />
```