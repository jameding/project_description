<!-- 项目大标题 -->
# VUE开发相关的代码规范
<!-- 项目说明 -->
具体代码风格遵循了VUE官方推荐的代码风格以及开发方式，在这里将VUE推荐的规范进行统一，将其中部分建议的规范进行强制化。
如果看此篇文档不太直观的话，可以参考VUE官方给的文档，[点击查看](https://cn.vuejs.org/v2/style-guide/)

## 规则归类

### 优先级 A：必要的

这些规则会帮你规避错误，所以学习并接受它们带来的全部代价吧。这里面可能存在例外，但应该非常少，且只有你同时精通 JavaScript 和 Vue 才可以这样做。

### 优先级 B：强烈推荐

这些规则能够在绝大多数工程中改善可读性和开发体验。即使你违反了，代码还是能照常运行，但例外应该尽可能少且有合理的理由。


## 优先级 A 的规则：必要的 (规避错误)

### 组件名为多个驼峰单词<sup data-p="a">必要</sup>

**组件名应该始终是多个单词的，根组件 `App` 以及 `<transition>`、`<component>` 之类的 Vue 内置组件除外。**

这样做可以避免跟现有的以及未来的 HTML 元素[相冲突](http://w3c.github.io/webcomponents/spec/custom/#valid-custom-element-name)，因为所有的 HTML 元素名称都是单个单词的。

#### 正例
``` js
export default {
  name: 'TodoItem',
  // ...
}
```

### 组件数据<sup data-p="a">必要</sup>

**组件的 `data` 必须是一个函数。**

当在组件中使用 `data` property 的时候 (除了 `new Vue` 外的任何地方)，它的值必须是返回一个对象的函数，因为当 `data` 的值是一个对象时，它会在这个组件的所有实例之间共享。


### Prop 定义<sup data-p="a">必要</sup>

**Prop 定义应该尽量详细。**

在你提交的代码中，prop 的定义应该尽量详细，至少需要指定其类型。细致的 [prop 定义](../guide/components-props.html#Prop-验证)有两个好处：

- 它们写明了组件的 API，所以很容易看懂组件的用法；
- 在开发环境下，如果向一个组件提供格式不正确的 prop，Vue 将会告警，以帮助你捕获潜在的错误来源。


### 为 `v-for` 设置键值<sup data-p="a">必要</sup>

**总是用 `key` 配合 `v-for`。**

在组件上*总是*必须用 `key` 配合 `v-for`，以便维护内部组件及其子树的状态。甚至在元素上维护可预测的行为，比如动画中的[对象固化 (object constancy)](https://bost.ocks.org/mike/constancy/)，也是一种好的做法。


### 避免 `v-if` 和 `v-for` 用在一起<sup data-p="a">必要</sup>

**永远不要把 `v-if` 和 `v-for` 同时用在同一个元素上。**

如果需要这样做，将判断过滤的条件设置成计算属性进行过滤后展示；如果需求不允许使用计算属性过滤，请将if放到Item容器上


### 为组件样式设置作用域<sup data-p="a">必要</sup>

**对于应用来说，顶级 `App` 组件和布局组件中的样式可以是全局的，但是其它所有组件都应该是有作用域的。**

使用`scoped` attribute，设定作用域


### 私有 property 名<sup data-p="a">必要</sup>

**使用模块作用域保持不允许外部访问的函数的私有性。如果无法做到这一点，就始终为插件、混入等不考虑作为对外公共 API 的自定义私有 property 使用 `$_` 前缀。并附带一个命名空间以回避和其它作者的冲突 (比如 `$_yourPluginName_`)。**

#### 正例

``` js
var myGreatMixin = {
  // ...
  methods: {
    $_myGreatMixin_update: function () {
      // ...
    }
  }
}
```

``` js
// 甚至更好！
var myGreatMixin = {
  // ...
  methods: {
    publicMethod() {
      // ...
      myPrivateFunction()
    }
  }
}

function myPrivateFunction() {
  // ...
}

export default myGreatMixin
```


## 优先级 B 的规则：强烈推荐 (增强可读性)

### 组件文件<sup data-p="b">强烈推荐</sup>

**只要有能够拼接文件的构建系统，就把每个组件单独分成文件。**

当你需要编辑一个组件或查阅一个组件的用法时，可以更快速的找到它。

#### 正例

```
components/
|- TodoList.js
|- TodoItem.js
```

```
components/
|- TodoList.vue
|- TodoItem.vue
```

### 单文件组件文件的大小写<sup data-p="b">强烈推荐</sup>

**[单文件组件](../guide/single-file-components.html)的文件名应该始终是单词大写开头 (PascalCase)

单词大写开头对于代码编辑器的自动补全最为友好，因为这使得我们在 JS(X) 和模板中引用组件的方式尽可能的一致。

#### 正例

```
components/
|- MyComponent.vue
```

### 基础组件名<sup data-p="b">强烈推荐</sup>

**应用特定样式和约定的基础组件 (也就是展示类的、无逻辑的或无状态的组件) 应该全部以一个特定的前缀开头，比如 `Base`、`App` 或 `V`。**

#### 正例

```
components/
|- BaseButton.vue
|- BaseTable.vue
|- BaseIcon.vue
```

```
components/
|- AppButton.vue
|- AppTable.vue
|- AppIcon.vue
```

### 单例组件名<sup data-p="b">强烈推荐</sup>

**只应该拥有单个活跃实例的组件应该以 `The` 前缀命名，以示其唯一性。**

这不意味着组件只可用于一个单页面，而是*每个页面*只使用一次。这些组件永远不接受任何 prop，因为它们是为你的应用定制的，而不是它们在你的应用中的上下文。如果你发现有必要添加 prop，那就表明这实际上是一个可复用的组件，*只是目前*在每个页面里只使用一次。

#### 正例

```
components/
|- TheHeading.vue
|- TheSidebar.vue
```

### 紧密耦合的组件名<sup data-p="b">强烈推荐</sup>

**和父组件紧密耦合的子组件应该以父组件名作为前缀命名。**

如果一个组件只在某个父组件的场景下有意义，这层关系应该体现在其名字上。因为编辑器通常会按字母顺序组织文件，所以这样做可以把相关联的文件排在一起。


#### 正例

```
components/
|- TodoList.vue
|- TodoListItem.vue
|- TodoListItemButton.vue
```

```
components/
|- SearchSidebar.vue
|- SearchSidebarNavigation.vue
```
{% raw %}</div>{% endraw %}


### 组件名中的单词顺序<sup data-p="b">强烈推荐</sup>

**组件名应该以高级别的 (通常是一般化描述的) 单词开头，以描述性的修饰词结尾。**

#### 正例

```
components/
|- SearchButtonClear.vue
|- SearchButtonRun.vue
|- SearchInputQuery.vue
```

### 自闭合组件<sup data-p="b">强烈推荐</sup>

**在[单文件组件](../guide/single-file-components.html)、字符串模板和 [JSX](../guide/render-function.html#JSX) 中没有内容的组件应该是自闭合的——但在 DOM 模板里永远不要这样做。**

#### 好例子

``` html
<!-- 在单文件组件、字符串模板和 JSX 中 -->
<MyComponent/>
```

``` html
<!-- 在 DOM 模板中 -->
<my-component></my-component>
```

### 模板中的组件名大小写<sup data-p="b">强烈推荐</sup>

### 完整单词的组件名<sup data-p="b">强烈推荐</sup>

**组件名应该倾向于完整单词而不是缩写。**

编辑器中的自动补全已经让书写长命名的代价非常之低了，而其带来的明确性却是非常宝贵的。不常用的缩写尤其应该避免。

#### 好例子

```
components/
|- StudentDashboardSettings.vue
|- UserProfileOptions.vue
```

### Prop 名大小写<sup data-p="b">强烈推荐</sup>

**在声明 prop 的时候，其命名应该始终使用 camelCase，而在模板和 [JSX](../guide/render-function.html#JSX) 中应该始终使用 kebab-case。**

我们单纯的遵循每个语言的约定。在 JavaScript 中更自然的是 camelCase。而在 HTML 中则是 kebab-case。

#### 正例

``` js
props: {
  greetingText: String
}
```

### 多个 attribute 的元素<sup data-p="b">强烈推荐</sup>

**多个 attribute 的元素应该分多行撰写，每个 attribute 一行。**

在 JavaScript 中，用多行分隔对象的多个 property 是很常见的最佳实践，因为这样更易读。模板和 [JSX](../guide/render-function.html#JSX) 值得我们做相同的考虑。

#### 正例

``` html
<img
  src="https://vuejs.org/images/logo.png"
  alt="Vue Logo"
>
```

``` html
<MyComponent
  foo="a"
  bar="b"
  baz="c"
/>
```

### 模板中简单的表达式<sup data-p="b">强烈推荐</sup>

**组件模板应该只包含简单的表达式，复杂的表达式则应该重构为计算属性或方法。**

复杂表达式会让你的模板变得不那么声明式。我们应该尽量描述应该出现的*是什么*，而非*如何*计算那个值。而且计算属性和方法使得代码可以重用。


#### 好例子

``` html
<!-- 在模板中 -->
{{ normalizedFullName }}
```

``` js
// 复杂表达式已经移入一个计算属性
computed: {
  normalizedFullName: function () {
    return this.fullName.split(' ').map(function (word) {
      return word[0].toUpperCase() + word.slice(1)
    }).join(' ')
  }
}
```

### 简单的计算属性<sup data-p="b">强烈推荐</sup>

**应该把复杂计算属性分割为尽可能多的更简单的 property。**

更简单、命名得当的计算属性是这样的：

- **易于测试**

  当每个计算属性都包含一个非常简单且很少依赖的表达式时，撰写测试以确保其正确工作就会更加容易。

- **易于阅读**

  简化计算属性要求你为每一个值都起一个描述性的名称，即便它不可复用。这使得其他开发者 (以及未来的你) 更容易专注在他们关心的代码上并搞清楚发生了什么。

- **更好的“拥抱变化”**

  任何能够命名的值都可能用在视图上。举个例子，我们可能打算展示一个信息，告诉用户他们存了多少钱；也可能打算计算税费，但是可能会分开展现，而不是作为总价的一部分。

  小的、专注的计算属性减少了信息使用时的假设性限制，所以需求变更时也用不着那么多重构了。

#### 正例

``` js
computed: {
  basePrice: function () {
    return this.manufactureCost / (1 - this.profitMargin)
  },
  discount: function () {
    return this.basePrice * (this.discountPercent || 0)
  },
  finalPrice: function () {
    return this.basePrice - this.discount
  }
}
```

### 带引号的 attribute 值<sup data-p="b">强烈推荐</sup>

**非空 HTML attribute 值应该始终带引号 (单引号或双引号，选你 JS 里不用的那个)。**

在 HTML 中不带空格的 attribute 值是可以没有引号的，但这鼓励了大家在特征值里*不写*空格，导致可读性变差。

#### 正例

``` html
<input type="text">
```

``` html
<AppSidebar :style="{ width: sidebarWidth + 'px' }">
```

### 严格用指令缩写<sup data-p="b">强烈推荐</sup>

**指令缩写 (用 `:` 表示 `v-bind:`、用 `@` 表示 `v-on:` 和用 `#` 表示 `v-slot:`) 应该要么都用要么都不用。**


### 隐性的父子组件通信<sup data-p="b">强烈推荐</sup>

**应该优先通过 prop 和事件进行父子组件之间的通信，而不是 `this.$parent` 或变更 prop。**

一个理想的 Vue 应用是 prop 向下传递，事件向上传递的。遵循这一约定会让你的组件更易于理解。然而，在一些边界情况下 prop 的变更或 `this.$parent` 能够简化两个深度耦合的组件。

问题在于，这种做法在很多*简单*的场景下可能会更方便。但请当心，不要为了一时方便 (少写代码) 而牺牲数据流向的简洁性 (易于理解)。

