---
title: gulp搭建
date: 2016-09-24 23:11:31
tags: 
---


## gulp是什么
  * gulp是前端开发过程中一种基于流的代码构建工具，是自动化项目的构建利器。
  * 能自动化地完成 javascript、coffee、sass、less、html/image、css 等文件的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成，并监听文件在改动后重复指定的这些步骤。


## gulp安装及搭建工作流程

 1. 创建一个工程文件夹
 打开cmd进入该文件夹目录，输入npm init初始化，之后会形成一个packa.json文件用来管理一些下载的依赖包。
 2. 下载gulp
 npm installgulp --save-dev.
 3. 手动建立一个gulpfiles.js,和开发用到的文件夹：*.css、*.js、*.html、*.img、*.fonts等。
 4. 下面所有的代码都需要写在gulpfiles.js文件夹里，主要的功能是压缩sass,js,html，监听等
 5. scss-->css并压缩
    (1) 下载gulp-sass用来将**sass转化成css**：npm install gulp-sass --save-dev
    (2) 下载gulp-cssnano用来将**css文件压缩**：npm install gulp-cssnano --save-dev
    (3) 然后再gulpfiles.js中写一下代码，后面有注释。
    ```
      python
        var gulp = require('gulp');         //下载gulp后需要引入gulp包
        var sass = require('gulp-sass');    //引入gulp-sass包
        var cssnano = reguire('gulp-cssnano')  //引包
        gulp.task('style',function(){       //task()是gulp里的一个方法
            gulp.src(css/*.scss)            //src()是写scss格式的路径
            .pipe(sass())               //然后执行sass()函数进行压缩
            .pipe(cssnano())
            .pipe(gulp.dest('dest("dist/css/")'))//dest()将压缩的css放到要发布的目录
        })
    ```

然后在cmd中执行: gulp style就可以看到目录中生成一个dest文件夹里面有*.css,而且是压缩过的
    6. 将js代码压缩并发送到要发布的文件：
   
* 将多个js合并的包gulp-concat:npm install --save-dev gulp-concat
* 将js压缩的包：gulp-uglify:npm install --save-dev gulp-uglify
* 然后再上面的基础上再添加如下代码：
```python
var concat = require('gulp-concat');
var uglify = reguire('gulp-uglify')
gulp.task('script',function(){
    gulp.src('js/*.js')
    .pipe(concat())
    .pipe(uglify())
    .pipe(gulp.dest('dist/js'))
})
```
* 在cmd中执行：gulp script就可以看到生成的js的文件
    7.对html进行压缩
* 下载htmlmin:npm install --save-dev htmlmin
```python
var htmlmin = require('gulp-htmlmin');
gulp.task('html',function(){
    var options = {
        collapseWhitespace:true,
        collapseBooleanAttributes:true,
        removeComments:true,
        removeEmptyAttributes:true,
        removeStyleLinkTypeAttributes:true,
    };
    gulp.src('*.js')
    .pipe(htmlmin(options))
    .pipe(gulp.dest('dist/'))
})
```
* 然后再cmd中执行：gulp html
**备注：**
1.collapseWhitespace:清除空格，压缩html
2.collapseBooleanAttributes:省略布尔属性的值
3.removeComments:清除html中注释的部分
4.removeEmptyAttributes:清除所有的空属性
还没写上的参数：
5.removeSciptTypeAttributes:清除所有script标签中的type="text/javascript"属性。
6.removeStyleLinkTypeAttributes:清楚所有Link标签上的type属性。
7.minifyJS:压缩html中的javascript代码。
8.minifyCSS:压缩html中的css代码。

        8. 将图片拷入到dist下：
```pathy
gulp.task('img',function(){
    pipe.src('img/*.*')
    .pipe(gulp.dest("dist/img"))
})
```
        9. 将fonts移入dist文件，同理，不在赘述。
        10. 构建服务器，这里用的是browser-syncbrowser-sync,下载npm install --save-dev browser-sync 
```pathy
var = require ('browser-sync');
gulp.task('serve',function(){
    browserSync.init({
        server:{baseDir:"dist/"}
    })
})
``` 
可以在在cmd中执行以下，gulp serve然后再自己本的浏览器输入本地地址。
        11.设置监听
```pathy
gulp.watch("*.html",["html"]);
gulp.watch("css/*.scss",["style"]);
gulp.watch("js/*js",["script"]);
gulp.watch("img/*.*",["img"]);
```    
12. 刷新前需要重载：
```pathy
var reload = browserSync.reload;

```   
13. 在每一个task中都需要添加这一句：
```pathy
    .pipe(reload({steam:true}))
```
呼啦啦,让我大喘气一下，写了好久啊，凭记忆和各种资料，终于完结。。