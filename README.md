# deep-in-fusion-next

非常核心的三个库是 saas-mapper / saas-tracker 

## 使用 saas-tracker

### 第一个重点是如何将 node 的包放到 html 文件中

在 `scripts/server/loaders/theme/config.js:22` 中获取到`saas-tracker` 文件

```js
trackerJS: getTrackerJS(),
  
function* getTrackerJS() {
    const trackerJSPath = require.resolve('@alifd/sass-tracker');

    return yield fs.readFile(trackerJSPath, 'utf8');
}  
```

获取到文件后，然后放到 ejs 中的变量中去

```js
Object.assign(
  locals,
  yield {
    varEnums: getVariableEnums(),
    trackerJS: getTrackerJS(),
  }
);

// const cofigTplPath = path.resolve(__dirname, '../../tpls/config.ejs'); 
const html = yield renderFile(cofigTplPath, locals);
```

在`config.ejs` 中将 tracker 的代码加载进来

```js
<script>
  <%- trackerJS %>
</script>
```

### 第二个重点是如何展示每个组件的 demo 

写好了组件之后，如何展示组件的每一种配置下的 demo，以及配置好demo 后，如何点击当前 demo 获取到对应的配置



