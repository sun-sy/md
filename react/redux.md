<!--
 * @Author: Do not edit
 * @Date: 2022-10-30 13:48:16
 * @LastEditors: sun
 * @LastEditTime: 2022-10-30 16:57:18
 * @FilePath: /md/react.md
-->
##Redux
*react的集中状态管理工具*
*1.安装*
```bash{.line-number}
npm install --save redux
```
*在`src`下创建`index.js`文件*
```javascript{.line-number}
// 引入redux
import { createStore } from 'redux';
//创建一个状态管理者
import Reducer from './reducer';

//注册管理者
const store = createStore(reducer);
export default store;
```
*reducer.js*
``` javascript{.line-numbers}
const defaultState = {};

export default (state = defaultState, action) => {
  if (action.type === 'change') {
    return { ...state, value: action.value };
  }
  // 必须返回一个新的state；
  return state;
};
```
*在外部组件中必须引入store*
```javascript{.line-numbers}
import store from './store';

// 获取state数据
store.getState();
// 修改state数据
store.dispatch({
  type: 'change',
  value: '',
});
```
####*redux-thunk中间件*
*1.安装*
``````bash{.line-numbers}
npm install --save redux-thunk
``````
*2.配置*
在 `store`中`index.js`引入
```javascript{.line-numbers}
/*
**applyMiddleware：添加中间件方法
**compose：函数的串联调用，将最后一个函数从尾部拿出执行并将返回作为参数传入相邻函数依次执行
*/
import { createStore, applyMiddleware, compose } from 'redux';
import reducer from './reducer';
import thunk from 'redux-thunk';

/**
 * 安装reduxDevTools插件后需要在createStore时执行该方法并传入__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({})才能在控制台中使用
 * createStore(reducer, window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__())
*/
const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}) : compose;
const enhancer = composeEnhancers(applyMiddleware(thunk));

//createStore只接收两个参数
const store = createStore(reducer, enhancer);
```
*组件中调用*
```javascript{.line-number}
/*
**猜测：
****中间件重写了redux.protoType.dispatch方法，当传入参数为函数时，执行此函数，并将原dispatch作为参数传入函数，以此实现在组件和store中添加中间件，实现方法的统一维护，以达到代码整洁的目的
*/
componentDidMount() {
  const action = getTodoList(); // 返回回调函数axios请求
  store.dispatch(action); // 被重写的dispatch方法
},
```
####*redux-saga中间件*
*1.安装*
``````bash{.line-numbers}
npm install --save redux-saga
``````
*2.安装*
在 `store`中`index.js`引入
```javascript{.line-numbers}
import { createStore, applyMiddleware, compose } from 'redux';
import reducer from './reducer';
import createSagaMiddleware from 'redux-sa ga';
import mySaga from './saga';

const sagaMiddleware = createSagaMiddleware;
const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}) : compose;
const enhancer = composeEnhancers(applyMiddleware(sagaMiddleware));

//createStore只接收两个参数
const store = createStore(reducer, enhancer);
sagaMiddleware.run(mySaga);
```
*saga.js*
```javascript{.line-numbers}
/*
** takeEvery: 监听函数
** methodName: actions.type
** callBack()
*/
import { takeEcery, put } from 'redux-saga/effects';

function* mySaga() {
  yield takeEvery('getMyList', getList);
}
/**
 * 当我们调用store.dispath({type: ’getMyList‘})时，takeEvery会监听到此方法，
 * 并执行回调函数，当回调函数执行完毕，使用put({ type：’getMyList‘，data });
 * 进入reducer中
 */
function* getList() {
  const data = {};
  put({ type: 'getMyList', data })
  console.log();
};
```
###react-redux
*1.安装*
```bash{.line-number}
npm install --save react-redux
npm install --save redux
```
*index.js*
```javascript{.line-numbers}
import React from 'react';
import ReactDOM from 'react-dom';
import SList from './SList';
// 提供器
import { Provider } from 'react-redux';
import store from './store';

// 提供器声明要包裹的组件
const App = (
  <Provider store = {store}>
    <SList></SList>
  </Provider>
);
ReactDOM.render(App, document.getElementById('root'));
```
*SList.js*
```javascript{.line-numbers}
// 连接器
import { cnnect } from 'react-redux';
// 映射store在props中可以直接通过this.props.value访问到
const stateToProps = (state) => {
  return {
    value: state.value;
  };
};
// 将方法映射在props中可以直接通过this.props.handlerChange调用到
const dispatchToProps = (dispatch) => {
  return {
    handlerChange (e) {
      const action  = {
        type: 'change',
        value: e.target.value,
      };
      dispatch(action);
    }
  }
}
export default connect(stateToProps, dispatchToProps)(SList);
```

