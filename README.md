##### 설치하기
    sudo npm install -g gulp-cli

##### 빌드하기
    gulp [task명]

##### 프로젝트 설정
    npm init (all enter)
    .gitignore 파일 생성
        - node_modules 등록
    npm install gulp --save-dev

##### 기본 폴더 설정
    app (빌드)
         css
         scss
         src
         index.html
    dist (배포)
    gulpfile.js

##### 걸프 플러그인
    npm install gulp-sass --save-dev
    npm install gulp-uglify --save-dev
    npm install gulp-concat --save-dev
    npm install gulp-coffee --save-dev
    npm install gulp-htmlmin --save-dev
    npm install gulp-webserver --save-dev
    npm install gulp-file-include --save-dev
    npm install jshint gulp-jshint --save-dev
    npm install gulp-babel babel-preset-es2015 --save-dev
    npm install gulp-browserify --save-dev

##### gulp-sass
```javascript
/**
 * 정의한  Task
 * @name scss
 * SCSS 파일을 빌드한다.
 *
 */
gulp.task('scss', function(){
    return gulp.src('app/scss/styles.scss') /* 해당 주소지 파일을 */
        .pipe(sass())
        /* 파이프를 통해 sass() 메서드를 호출
           즉 sass - > css 파일로 변환
        */
        .pipe(gulp.dest('app/css'))
        /* 해당 주소지에 반환값이 담긴다.
           즉 변환된 styles.css 파일이 생성
        */
});
```

##### gulp-uglify
```javascript
/**
 * 정의한  Task
 * @name uglify
 * 파일의 소스를 압축한다.
 *
 */
gulp.task('uglify', function(){
    return gulp.src('app/src/*.js')
        .pipe(uglify())
        .pipe(gulp.dest('dist'))
});
```

##### gulp-concat
```javascript
/**
 * 정의한  Task
 * @name concat
 * 파일들을 합친다.
 *
 */
gulp.task('concat', function(){
    return gulp.src('app/src/*.js')
        .pipe(concat('all.js'))
        .pipe(gulp.dest('dist'))
});
```

##### gulp-coffee
```javascript
/**
 * 정의한  Task
 * @name coffee
 * 커피스크립트를 js파일로 변환한다.
 *
 */
gulp.task('coffee', function(){
    return gulp.src('app/src/*.coffee')
        .pipe(coffee())
        .pipe(gulp.dest('dist'))
});
```

##### gulp / watch
```javascript
/**
 * 정의한  Task
 * @name watch
 * 특정 폴더를 바라보게하고 수정이 되었을 때 Task를 실행한다.
 *
 */
gulp.task('watch', function(){
    return gulp.watch('app/src/*{js, coffee}', ['coffee-js-min'])
});
```

##### gulp-htmlmin
```javascript
/**
 * 정의한  Task
 * @name htmlmin
 * html파일의 소스를 압축한다.
 *
 */
gulp.task('htmlmin', function(){
    return gulp.src('app/*.html')
        .pipe(htmlmin({collapseWhitespace: true}))
        .pipe(gulp.dest('dist'));
});
```

##### gulp-webserver
```javascript
/**
 * 정의한  Task
 * @name webserver
 * 웹서버처럼 동작하게 한다.
 * 옵션 : https://www.npmjs.com/package/gulp-webserver
 * 
 */
gulp.task('webserver', function() {
  gulp.src('app')
    .pipe(webserver({
      fallback: 'index.html', /* 루트 페이지 지정 */
      port : 4187, /* 포트 지정 */
      livereload: true, /* 파일이 수정되면 리로드 */
      directoryListing: true /* 폴더 목록 표시 */
    }));
});
```

##### gulp-file-include
```javascript
/**
 * 정의한  Task
 * @name fileinclude
 * 파일을 인클루드 한다.
 *
 */
gulp.task('fileinclude', function(){
    return gulp.src('app/fileinclude/index.html')
        .pipe(fileinclude({
            prefix: '@@',
            basepath: '@file'
        }))
        .pipe(gulp.dest('dist'));
});
```

##### gulp-jshint
```javascript
/**
 * 정의한  Task
 * @name lint
 * 지정파일에 js lint를 돌린다.
 *
 */
gulp.task('lint', function(){
    return gulp.src('app/src/*.js')
        .pipe(jshint())
        .pipe(jshint.reporter('default'));
});
```

##### gulp-babel
```javascript
/**
 * 정의한  Task
 * @name babel
 * es6를 es5 구문으로 호환시킨다.
 *
 */
gulp.task('babel', function(){
    return gulp.src('app/es6/sum.js')
        .pipe(babel({
            presets: ['es2015']
        }))
        .pipe(gulp.dest('dist'));
});
```

##### gulp-browserify
```javascript
/**
 * 정의한  Task
 * @name browserify
 * browserify(브라우저리파이)를 통해 번들 작업을 거친다.
 *
 */
gulp.task('browserify', function() {
    return gulp.src('app/bundle/browserify-bundle.js')
        .pipe(browserify({
            insertGlobals : true,
            debug : !gulp.env.production
        }))
        .pipe(gulp.dest('dist'))
});
```