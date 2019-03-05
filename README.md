# Basic Gulp workflow for websites

## Objectives
- Find out how to setup a workflow with Gulp
- Spin up a web server
- Browser refresh whenever file is saved
- Optimize all assets (CSS, JS, fonts, and images) for production
- Learn how to chain together different tasks

## Notes
### Setup
First, we'll create a folder called `project`
Run the `npm init` command from inside that directory
Install Gulp into the project $ `npm install gulp --save-dev`
Create folder structure
...app/
......css/
......fonts/
......images/
......js/
......scss/
......index.html
...dist/
...node_modules/
...gulpfile.js
...package.json



### Preprocessing with Gulp
Install `gulp-sass` plugin $ `npm install gulp-sass --save-dev`

```javascript
var gulp = require('gulp');
// Requires the gulp-sass plugin
var sass = require('gulp-sass');

gulp.task('sass', function(){
  return gulp.src('source-files')
    .pipe(sass()) // Using gulp-sass
    .pipe(gulp.dest('destination'))
});
```

### Globbing in Node
Globs are matching patterns for files that allow you to add more than one file into `gulp.src`. It's like regular expressions, but specifically for file paths.

Most workflows with Gulp tend to only require 4 different globbing patterns:
1. `*.scss`: The `*` pattern is a wildcard that matches any pattern in the current directory. In this case, we’re matching any files ending with `.scss` in the root folder (`project`). 
2. `**/*.scss`: This is a more extreme version of the `*` pattern that matches any file ending with `.scss` in the root folder and any child directories.
3. `!not-me.scss`: The `!` indicates that Gulp should exclude the pattern from its matches, which is useful if you had to exclude a file from a matched pattern. In this case, `not-me.scss` would be excluded from the match.
4. `*.+(scss|sass)`: The plus `+` and parentheses `()` allows Gulp to match multiple patterns, with different patterns separated by the pipe `|` character. In this case, Gulp will match any file ending with `.scss` or `.sass` in the root folder.

```javascript
gulp.task('sass', function() {
  return gulp.src('app/scss/**/*.scss') // Gets all files ending with .scss in app/scss and children dirs
    .pipe(sass())
    .pipe(gulp.dest('app/css'))
})
```

### Watching Sass files for changes
Gulp provides us with a watch method that checks to see if a file was saved. 
```javascript
// Gulp watch syntax
gulp.watch('files-to-watch', ['tasks', 'to', 'run']); 
// Gulp watch syntax for sass
gulp.watch('app/scss/**/*.scss', ['sass']); 
```
More often though, we'll want to watch more than one type of file at once. To do so, we can group together multiple watch processes into a watch task:
```javascript
gulp.task('watch', function(){
  gulp.watch('app/scss/**/*.scss', ['sass']); 
  // Other watchers
})
```

### Live-reloading with Browser Sync
Browser Sync helps make web development easier by spinning up a web server that helps us do live-reloading easily. $ `npm install browser-sync --save-dev`

To use Browser Sync, we'll have to require Browser Sync.
```javascript
var browserSync = require('browser-sync').create();
```









