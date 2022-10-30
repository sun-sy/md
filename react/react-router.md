<!--
 * @Author: Do not edit
 * @Date: 2022-10-30 22:22:58
 * @LastEditors: sun
 * @LastEditTime: 2022-10-31 00:24:32
 * @FilePath: /md/react/react-router.md
-->
### React-Router
*1.安装*
```bash{.line-numbers}
npm install --save react-router-dom
```
*index.js*
```js{.line-number}
import React from 'react';
import ReactDOM from 'react-dom';
import AppRouter from './AppRouter';

ReactDOM.render(<AppRouter />, document.getElementById('root'));
```
*AppRouter.js*
```js{.line-numbers}
import React from 'react';
import { BrowserRouter as Router, Route, Link } from 'react-router-dom';

function Login() {
  return (<img />);
};
function Home() {
  // 路由传参
  // this.props.match.params.id
  return (<img />);
}
function AppRouter() {
  const routerConfig = [
    { path: '/', exact: true, component: Login, name: '登录' },
    { path: '/home/:id', exact: true, component: Login, name: '首页' },
  ];
  return (
    <Router>
      <ul>
        this.routerConfig.map(item => {
          const { path, component, name } = item;
          return (
            <li key={path}><Link path={ path }>{ name }</Link></li>
          )
        })
      </ul>
      {/* exact精确匹配 */}
      this.routerConfig.map(item => {
        const { path, exact, component, name } = item;
        return (
          <Route path={ path } exact={ exact } component={ component }></Route>
        );
      });
    </Router>
  )
};
export default AppRouter;
```
*Redirect 重定向*
*index.js*
```js{.line-numbers}
/**
 * Redirect 重定向
 * 当存在redirect时页面默认会重定向到指定路径下
 */
import { Redirect } from 'react-router-dom';

function Login() {
  return (
    <Redirect to="/home/"></Redirect>
  );
};
function Home() {
  return (<h1></h1>);
}
```
*编程式重定向*
```js{.line-numbers}
import React, { Component } from 'react';

class Login extends Component {
  constructor(props) {
    super(props);
    // 编程式重定向
    this.props.history.push('/home/');
  };
};
```