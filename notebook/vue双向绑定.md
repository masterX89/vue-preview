# React的单向绑定

> 单向绑定非常简单，就是把Model绑定到View，当我们用JavaScript代码更新Model时，View就会自动更新。
>
> 有单向绑定，就有双向绑定。如果用户更新了View，Model的数据也自动被更新了，这种情况就是双向绑定。
>
> 什么情况下用户可以更新View呢？填写表单就是一个最直接的例子。当用户填写表单时，View的状态就被更新了，如果此时MVVM框架可以自动更新Model的状态，那就相当于我们把Model和View做了双向绑定。

React是经典的数据单向绑定，以ant design的[Input组件](https://ant.design/components/input-cn/#header)为例，在`codesandbox`中打开，实现自己的`MInput.js`组件如下：

```js
import React, { Component } from "react";
import { Input } from "antd";

export default class MInput extends Component {
  state = {
    value: "default"
  };
  componentDidMount() {
    setTimeout(() => {
      this.setState({ value: "data from server" });
    }, 1000);
  }
  render() {
    let { value } = this.state;
    return <Input value={value}/>;
  }
}
```

修改`index.js`如下：

```js
import React from "react";
import ReactDOM from "react-dom";
import "antd/dist/antd.css";
import "./index.css";
import MInput from "./MInput";

ReactDOM.render(<MInput />, document.getElementById("container"));
```

这样就实现了一个渲染`MInput`组件的React工程，界面初识值为`default`，组件挂载后1s异步请求到数据变为`data from server`，此时无法修改`input`里的内容。

修改`MInput.js`内容为：

```js
import React, { Component } from "react";
import { Input } from "antd";

export default class MInput extends Component {
  state = {
    value: "default"
  };
  componentDidMount() {
    setTimeout(() => {
      this.setState({ value: "data from server" });
    }, 1000);
  }
  onChange = (e) => {
    this.setState({ value: e.target.value });
  };
  render() {
    let { value } = this.state;
    return <Input value={value} onChange={this.onChange} />;
  }
}

```

可以看到，在`Input`中添加了`onChange`属性，并指定为`this.onChange`方法后，实现双向绑定。

# Vue的默认双向绑定

vue的双向绑定一般存在于表单中，添加`v-model`属性完成双向绑定。

# Vue的自定义组件双向绑定

- [ ] 需要补充自定义组件双向绑定

# 参考文献

[1]: https://www.liaoxuefeng.com/wiki/1022910821149312/1109527162256416	"廖雪峰官网双向绑定解释"

