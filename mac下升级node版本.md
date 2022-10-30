<!--
 * @Author: Do not edit
 * @Date: 2021-09-24 00:10:18
 * @LastEditors: sun
 * @LastEditTime: 2022-10-30 13:42:53
 * @FilePath: /md/mac下升级node版本.md
-->
### mac升级node版本
``````bash{.line-numbers}
sudo npm cache clean -f //清除nodejs的cache：
sudo npm install -g n //使用npm安装n模块
npm view node versions // node所有版本
sudo n latest // 升级到最新版本
sudo n stable // 升级到稳定版本
sudo n xx.xx // 升级到具体版本号
``````
### mac升级npm版本
``````bash{.line-numbers}
sudo npm install npm@latest -g //升级到最新版
sudo npm install npm@xx -g //升级到指定版本
npm version // 查看版本详情
npm view npm version // npm最新版本
npm view npm versions // npm所有版本
npm list //  插件清单
``````