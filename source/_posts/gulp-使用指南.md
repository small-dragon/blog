---
title: Gulp 使用指南
date: 2016-07-14 08:30:42
tags: [tools]
---

By gxh

-------

> Gulp 基础使用，文章以 `static-pages` 项目为例

-------

## 安装
* 全局安装 `gulp`:
```
$ npm i -g gulp
```

* 进入项目根目录，安装 `node依赖`
```
$ npm install
```

## 启动
* 根目录启动 `gulp` 命令,启动后，`gulp` 会自动 `watch` 文件的变化，后进行需要的文件注入及 less 解析工作
```
$ gulp
```

## 配置介绍
* 依赖库内容：
```javascript
// pakage.json
"devDependencies": {
  "gulp": "^3.9.1",     // gulp
  "gulp-file-include": "^0.13.7",  // 文件注入
  "gulp-less": "^3.1.0",  // less解析器
  "gulp-sourcemaps": "^1.6.0", // sourcemaps
  "less-plugin-autoprefix": "^1.5.1", // less前缀补全
  "stream-combiner2": "^1.1.1"  // 文件流控制
}
```

* `gulp` 的启动需要读取 `gulpfile.js` 文件内配置，so，let me see see 如何配置 `gulpfile`，下面将以功能 `less解析` 为例
```javascript
// gulpfile.js
var gulp = require('gulp');  // 引入 gulp
var less = require('gulp-less');  // 引入less解析器

// 声明一个名字为 “less” 的 gulp任务，可通过命令 `gulp less` 直接调用
gulp.task('less',  () => {  
  // 通过 gulp.src 读取对应位置内的文件流信息
  return gulp.src('./less/**/*.less')  
    // 通过 pipe 将上一层的文件流传递给括号内的方法里
    .pipe(less({       
      // less解析器的基本配置，设置如何出来less文件流（具体参数查看文档）
      .......       
    }))
    // 接收less输出stream，并通过 gulp.dest 输出文件到指定位置
    .pipe(gulp.dest('./css'));  
});

// 声明一个名字为 "watch" 的 gulp 任务，可通过命令 `gulp watch` 直接调用
gulp.task('watch', () => {   
    // 通过 gulp.watch 监听指定目录下的文件改动，只要文件一经修改，则会启动数组里面的 less 任务进行解析
    gulp.watch('./less/**/*.**', ['less']);
});

// 声明一个名字为 "default" 的 gulp 任务，直接启动命令 `gulp` 会启动此任务，并会先执行数组里面的任务
gulp.task('default', ['less','watch']);
```

## End
`gulp` 的介绍大概是这样了，大家可以先研究下项目内的 `gulpfile` 配置，琢磨一下这个脚手架的功能再进行任务开发，之后可以尝试自己写一个自己专属的脚手架，分分钟上手~
