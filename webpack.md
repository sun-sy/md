<!--
 * @Author: Do not edit
 * @Date: 2021-09-02 22:24:14
 * @LastEditors: sun
 * @LastEditTime: 2022-10-30 13:44:06
 * @FilePath: /md/webpack.md
-->
### 热更新：webpack-dev-server
##### WDS不刷新浏览器
##### WDS不输出文件，而是放在内存里
##### 使用HotModuleReplacementPlugin插件
``````javascript{.line-numbers}
{
  "name": "hello-webpack",
  "version": "1.0.0",
  "description": "Hello webpack",
  "main": "index.js",
  "script": {
    "build": "webpack",
    "dev": "webpack-dev-server --open"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
``````

