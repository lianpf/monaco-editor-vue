# @lianpf/monaco-editor-vue

> [Monaco Editor](https://github.com/lianpf/monaco-editor-vue) for Vue.

[![NPM version][npm-image]][npm-url]
[![Downloads][downloads-image]][npm-url]

[![monaco-editor-vue](https://nodei.co/npm/@lianpf/monaco-editor-vue.png)](https://npmjs.org/package/@lianpf/monaco-editor-vue)

[npm-url]: https://www.npmjs.com/package/@lianpf/monaco-editor-vue  
[downloads-image]: http://img.shields.io/npm/dm/@lianpf/monaco-editor-vue.svg
[npm-image]: http://img.shields.io/npm/v/@lianpf/monaco-editor-vue.svg


## Installation

```bash
npm install @lianpf/monaco-editor-vue --save
npm install monaco-editor-webpack-plugin --save
```

## Using with Webpack

```js
<template>
  <div id="app">
    <MonacoEditor
      width="800"
      height="500"
      theme="vs-dark"
      language="javascript"
      :options="options"
      @change="onChange"
    ></MonacoEditor>
  </div>
</template>

<script>
import MonacoEditor from 'monaco-editor-vue';
export default {
  name: "App",
  components: {
    MonacoEditor
  },
  data() {
    return {
      options: {
        //Monaco Editor Options
      }
    }
  },
  methods: {
    onChange(value) {
      console.log(value);
    }
  }
};
</script>
```

添加 [Monaco Webpack plugin](https://github.com/Microsoft/monaco-editor-webpack-plugin) `monaco-editor-webpack-plugin` 到你项目中的 `webpack.config.js`:

```js
const MonacoWebpackPlugin = require('monaco-editor-webpack-plugin')
module.exports = {
  plugins: [
    new MonacoWebpackPlugin({
      // available options are documented at https://github.com/Microsoft/monaco-editor-webpack-plugin#options
      languages: ['javascript']
    })
  ]
}
```

如果你项目中使用的是 [Vue CLI](https://cli.vuejs.org) 而不是webpack, 你需要配置 `vue.config.js`:

```js
const MonacoWebpackPlugin = require('monaco-editor-webpack-plugin')

module.exports = {
  chainWebpack: config => {
    config.plugin('monaco-editor').use(MonacoWebpackPlugin, [
      {
        // Languages are loaded on demand at runtime
        languages: ['json', 'javascript', 'html', 'xml']
      }
    ])
  }
}
```

## Properties

如果你指定 `value` 属性, 组件则以受控模式运行。否则，它是非受控模式。

* `width`：editor 的宽度, 默认为`100%`
* `height`：editor 的高度，默认为 `100%`.
- `value`：editor 中可以自动创建 model 的值(value of the auto created model in the editor)
- `original`：editor 中可以自动创建 original model 的值(value of the auto created original model in the editor).
- `language`：编辑器中自动创建模型的初始语言，默认为 `javaScript`.
- `theme`：编辑的主题，默认为 `vs`.
- `options`：参考 [Monaco interface IEditorConstructionOptions](https://microsoft.github.io/monaco-editor/api/interfaces/monaco.editor.ieditorconstructionoptions.html).
- `editorBeforeMount(monaco)`：在 editor 加载安装好之前调用的 function (类似于 Vue 中的 `beforeMount`).
- `editorMounted(editor, monaco)`：在 editor 加载安装好后调用的 function (类似于 Vue 中的 `mounted`).
- `change(newValue, event)`：当前 model 的内容发生更改时所触发的事件

## Events & Methods

参考 [Monaco interface IEditor](https://microsoft.github.io/monaco-editor/api/interfaces/monaco.editor.ieditor.html).

### Use multiple themes

[Monaco only supports one theme](https://github.com/Microsoft/monaco-editor/issues/338).

### How to use the diff editor

```js
<template>
  <div id="app">
    <MonacoEditor
      :diffEditor="true"
      original="..."
      //...
    ></MonacoEditor>
  </div>
</template>
```
