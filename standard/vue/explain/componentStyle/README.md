<!-- 项目大标题 -->
# VUE组件相关的代码规范
<!-- 项目说明 -->
这里描述了项目组件的相关规范，其中包含组件放的位置，组件建设的标准等。


## 基础规范

#### 只要有能够拼接文件的构建系统，就把每个组件单独分成文件

当你需要编辑一个组件或查阅一个组件的用法时，可以更快速的找到它

#### 单文件组件的文件名应该要么始终是单词大写开头 (PascalCase)
```js
|- SearchButtonClear.vue
```

#### 组件名应该以高级别的 (通常是一般化描述的) 单词开头，以描述性的修饰词结尾


```js
  components/
|- SearchButtonClear.vue
|- SearchButtonRun.vue
|- SearchInputQuery.vue
```

## 结构规范

#### 涉及到当前业务逻辑并包含全局状态（vuex store）的组件放到项目内

如果组件业务逻辑只跟当前模块相关的，并且包含全局状态（vuex store）的业务逻辑，将组件放在src/views/内的模块中

#### 没有强数据交互的组件或者纯展示组件，放到components内

展示类的、无逻辑的或无状态的组件统一放到src/componets内

#### 公共组件内包含全局状态和数据处理，放到components/app内

公共模块，很多地方都可以调用的并且包含全局状态和接口调用等的，放到src/componets/app里（尽量不要出现这类组件）

#### 多项目可以共用的公共组件，放到components/global内

公共组件里，如果包含公司全项目共用，或者封装的UI框架可以多项目共用的，放到components/global内

