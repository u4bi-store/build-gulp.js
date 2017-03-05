##### 설치하기
    sudo npm install -g gulp-cli

##### 프로젝트 설정
    npm init (all enter)
    .gitignore 파일 생성
        - node_modules 등록
    npm install gulp --save-dev

##### 기본 폴더 설정
    app (빌드)
         css
         scss
            styles.scss
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