

前端构建工具（Gulp）：

1.gulp 是什么？

​	前端自动化**流式**构建工具

​	编写机械化**任务**，即告诉它我们想要做什么，当需要做这件事情的时候，执行任务即可

**gulp 官网**

| 语音 | 地址                       |
| ---- | -------------------------- |
| 中文 | https://www.gulpjs.com.cn/ |
| 英文 | https://gulpjs.com         |

2.为什么要使用Gulp

提高开发效率 改善开发体验。

- 语法转换（es6、less ...）
- 文件保存，浏览器自动刷新
- 公共文件抽离再包含（类似php中的include）
- 项目上线，文件需要压缩合并



3.开始使用

3.1 初始化

```bash
  # 在当前目录自动生成一个package.json文件
  cnpm init -y
```

- 安装插件

  ```bash
  # 当前项目中安装gulp
  cnpm install gulp --save-dev
  # 压缩html的插件
  cnpm install gulp-htmlmin --save-dev
  # 压缩css的插件
  cnpm install gulp-cssmin --save-dev
  # 自动打开浏览器，并实时刷新插件(浏览器同步测试工具)
  cnpm install browser-sync --save-dev
  ```

- 配置文件

  在当前项目的**根目录**中创建一个**gulpfile.js**文件，如链接中文件

  [gulpfile.js](./code/gulpfile.js)

3.2下载 gulp 文件

```
npm install gulp@3.9.1 
```

​	新版4.0.0会有 anysc 和 await 的问题，必须返回一个 steam 对象或者返回一个 promise 对象，promise对象这个后面会讲

3.3新建  gulpfile.js   文件，文件名称可以更改，但是需要修改配置文件，这里不做阐述。

3.4 引用 gulp   

```
var gulp = require('gulp');
```

3.5 创建项目目录结构

​	创建一个 src 目录

​		src 里面创建 目录结构：js文件， css文件， images文件， view 文件

```javascript
// gulp.task('任务名称', 函数) 创建任务
// 任务名称的用处:在执行任务的时候需要指定任务名称
// 函数:要做的事情需要写在回调函数中 比如less解析 代码压缩...
gulp.task('first',function(){
    // gulp.src('文件路径') 获取文件
    // 获取任务要处理的文件
    gulp.src('./css/base.css')
    // pipe('怎样处理') 处理任务
    // gulp.dest('文件路径') 将处理好的文件放入参数路径中
        .pipe(gulp.dest('dist/css'))
});
```

3.6 执行 gulp 需要 gulp 命令行工具用于执行 gulp 任务

​	使用方法

```
gulp 任务名称
```

4、Gulp插件地址

- [gulp-htmlmin](https://www.npmjs.com/package/gulp-htmlmin) html文件压缩
- [gulp-less](https://www.npmjs.com/package/gulp-less) 将less转换为css
- [gulp-csso](https://www.npmjs.com/package/gulp-csso) 压缩css
- [gulp-autoprefixer](https://www.npmjs.com/package/gulp-autoprefixer) 自动添加css前缀
  - http://www.ydcss.com/archives/94 查看详细配置点这个
  - https://github.com/browserslist/browserslist#queries 想看官方文档点这个
- [gulp-babel](https://www.npmjs.com/package/gulp-babel) 将新的JavaScript语法转化浏览器能够认识的语法
- [browser-sync](http://www.browsersync.cn/docs/gulp/) 浏览器实时同步工具
- [gulp-clean](https://github.com/peter-vilja/gulp-clean) 清除文件
- [run-sequence](https://github.com/OverZealous/run-sequence) 使任务按顺序执行
- [gulp-rev](https://www.npmjs.com/package/gulp-rev) 生成文件指纹
- [gulp-rev-collector](https://www.npmjs.com/package/gulp-rev-collector) 替换文件指纹
- [gulp-rename](https://www.npmjs.com/package/gulp-rename) 更改文件名称
- [gulp-file-include](https://www.npmjs.com/package/gulp-file-include) 文件拆分
- [gulp-uglify](https://www.npmjs.com/package/gulp-uglify) JavaScript混淆压缩
- [gulp-concat](https://www.npmjs.com/package/gulp-concat) 文件合并
- [gulp-imagemin](https://www.npmjs.com/package/gulp-imagemin) 图片压缩