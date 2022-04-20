## 1、概述

1. sass 从第三代开始，放弃了缩进式风格，完全向下兼容普通的 CSS 代码，这一代的 sass 被称为 scss 。

2. 中文教程： [Sass教程 Sass中文文档 | Sass中文网](https://www.sass.hk/docs/) 

3. sass、less 与 stylus 的区别

   1. 编译环境不一样
      1. sass 需要 ruby 环境
      2. less 需要 less.js
      3. stylus 需要 node
   2. 变量符不一样
      1. sass 为 $
      2. less 为 @
      3. stylus 无符号，用赋值语法
   3. 难易程度
      1. less 容易上手
      2. sass、stylus 更为强大

4. 安装

   1. 安装 vsCode 扩展， Live Sass Compiler，并修改 setting.json

      ```javascript
      {
          "liveSassCompile.settings.formats":[{
              /*
              nested:嵌套
              expanded:展开
              compact：紧凑
              compressed：压缩
              */
              "format": "compact",
              "extensionName": ".css",
              "savePath": "~/../css"
          }],
      
          // 排除目录
          "liveSassCompile.settings.excludeList": [
              "**/node_modules/**",
              ".vscode/**"
          ],
          // 是否生成对应的map
          "liveSassCompile.settings.generateMap": true,
          // 是否添加兼容前缀
          "liveSassCompile.settings.autoprefix": [
              "> 1%",
              "last 2 versions"
          ],
          "explorer.confirmDelete": false
      }
      ```

## 2、CSS 功能拓展

### 1）嵌套规则





































