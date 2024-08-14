Gulp - умеет только создавать и организовывать задачи

__Основные методы GULP__ :
*  **gulp.task()**  - определить задачу 
*  **gulp.src()** - взять исходные файлы
*  **pipe()** - "закинуть в трубу" внутри которой применить плагин для обработки файлов
*  **gulp.dest()** - сохранить получивший результат
*  **gulp.parallel()** - запустить несколько задачь параллельно (одновременно)
*  **gulp.series()** - запустить несколько задачь последовательно
*  **gulp.watch()**  -  следить за файлами

__Task for css__ :
~~~javascript
gulp.task('sass', function (done) {
 return gulp
  .src('src/scss/*.scss')
  .pipe(sass())
  .pipe(groupMedia())
  .pipe(gulp.dest('dist/css'));
});
~~~
GULP plugins : sass() groupMedia()
**Запустить задачу: gulp sass**

#### Итоговый Task
~~~javascript
gulp.task('default', gulp.series(
 'clean',
 gulp.parallel('sass', 'includeFiles', 'copyImages'),
 gulp.parallel('startServer', 'watch')
));
~~~
Запустить сборку: gulp

#### __Пакеты__ 
Описание пакетов: 
* **gulp** - собственно Gulp
* **gulp-sass** - Сборка SASS / SCSS
* **sass** - Необходим для сборки SASS / SCSS 
* **gulp-file-include** - Подключение файдов друг в друга. HTML include
* **gulp-clean** - Удаление файлов
* **gulp-connect** - Сервер с автообновлением страницы
* **gulp-sourcemaps**  -  Исходные карты для CSS
* **gulp-plumber**  - Фикс ошибок при сборке
* **gulp-notify**  -  Нотификации
* **gulp-group-css-media-queries**   -  Группировка CSS медия запросов
* **webpack-stream style-loader css-loader** — сборка JS
* **gulp-babel @babel/core @babel/preset-env** — babel для JS
* **gulp-imagemin@7** — сжатие изображений
* **gulp-changed** — отслеживание изменений в файла
* **gulp-webp gulp-webp-html gulp-webp-css** — работа с webp

##### Команда для установки всех пакетов:
~~~bash
npm i gulp gulp-sass sass gulp-file-include gulp-clean gulp-server-livereload gulp-sourcemaps gulp-plumber gulp-notify gulp-group-css-media-queries --save-dev
~~~
gulpfile.js
INCLUDE html files in one file
~~~javascript
const gulp = require('gulp');
const fileInclude = require('gulp-file-include');

const fileIncludeSetting = {
  prefix: '@@',
  basepath: '@file',
};

gulp.task('includeFiles', function(){
 return gulp.src('./src/*.html')
  .pipe(fileInclude(fileIncludeSetting))
  .pipe(gulp.dest('./dist/'))
});
~~~

##### Task for copy scss in css
~~~javascript
const sass = require('gulp-sass')(require('sass'));

gulp.task('sass', function(){
 return gulp.src('./src/scss/*.scss')
  .pipe(sass())
  .pipe(gulp.dest('./dist/css/'))
});
~~~

##### Task for copy img
~~~javascript
gulp.task('copyImages', function(){
 return gulp.src('./src/img/**/*')
  .pipe(gulp.dest('./dist/img/'))
});
~~~

##### Task server livereload
~~~javascript
const connect = require('gulp-connect');

gulp.task('server', function () {
 connect.server({
  name: 'Dist App',
  root: 'dist',
  port: 3000,
  livereload: true
 });
});

html, scss
.pipe(connect.reload());
~~~

##### Task for clean dist
~~~javascript
const clean = require('gulp-clean');
const fs = require('fs');

gulp.task('clean', function(done){
 if (fs.existsSync('./dist/')){
  return gulp.src('./dist/', { read: false })
   .pipe(clean({ force: true}));
  }
  done();
});
~~~

##### Task watch files
~~~javascript
gulp.task('watch', function(){
 gulp.watch('./src/scss/**/*.scss', gulp.parallel('sass'));
 gulp.watch('./src/**/*.html', gulp.parallel('html'));
 gulp.watch('./src/img/**/*', gulp.parallel('images'));
});
~~~
##### Task sourceMaps
~~~javascript
const sourceMaps = require('gulp-sourcemaps');

// Используем внутри таска scss
gulp.task('sass', function(){
 return gulp.src('./src/scss/*.scss')
  .pipe(sourceMaps.init())
  .pipe(sass())
  .pipe(sourceMaps.write())
  .pipe(gulp.dest('./dist/css/'))
  .pipe(connect.reload());
});
~~~
Позваляет видеть путь к файлу scss

##### Task mediaquires
Позволяет собрать медия файла в один. Использовать для продакшена 
~~~javascript
const groupMedia = require('gulp-group-css-media-queries');

scss
.pipe(groupMedia())
~~~
##### Task plumber and notify
Помогают избежать зависание сборки во время возникновения ошибок
~~~javascript
const plumber = require('gulp-plumber');
const notify = require('gulp-notify');

const plumberHtmlConfig = {
 errorHandler: notify.onError({
  title: 'HTML',
  message: 'Error <%= error.message %>',
  sound: false
 })
};

html
.pipe(plumber(plumberHtmlConfig))

const plumberSassConfig = {
 errorHandler: notify.onError({
  title: 'Styles',
  message: 'Error <%= error.message %>',
  sound: false
 })
};

sass
.pipe(plumber(plumberSassConfig))
~~~
##### Task fonts and files copy
~~~javascript
gulp.task('fonts', function(){
 return gulp.src('./src/fonts/**/*')
  .pipe(gulp.dest('./dist/fonts/'))
});

gulp.task('files', function(){
 return gulp.src('./src/files/**/*')
  .pipe(gulp.dest('./dist/files/'))
});

watch
gulp.watch('./src/fonts/**/*', gulp.parallel('fonts'));
gulp.watch('./src/files/**/*', gulp.parallel('files'));
~~~

##### Task js
~~~javascript
const webpack = require('webpack-stream');

gulp.task('js', function() {
 return gulp.src('./src/js/*.js')
  .pipe(plumber(plumberNotify('JS')))
  .pipe(webpack(require('./webpack.config.js')))
  .pipe(gulp.dest('./dist/js'))
});

watch
gulp.watch('./src/js/**/*.js', gulp.parallel('js'));
~~~
##### Task babel for old browser
~~~javascript
const babel = require('gulp-babel');

js
.pipe(babel())
~~~
##### Task converter images
~~~javascript
const imagemin = require('gulp-imagemin');

images
.pipe(imagemin({ verbose: true }))
~~~















