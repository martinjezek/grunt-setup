# Grunt - Setup

> A few thoughts how to set up Grunt - The JavaScript Task Runner.

- [Grunt.js][grunt.js]

## Install Grunt-CLI:

Install `grunt-cli` globally and you'll have access to the grunt command anywhere on your system.

- [npm grunt-cli][grunt-cli]
- `$ npm install grunt-cli -g`

## Install Grunt

- You're at `root` of your project
- If you don't have a `package.json` then run `$ npm init` and fill in your project info
- Else run `$ npm install`
- [Find out more][package.json] about `package.json`

```javascript
{
    "name": "grunt-setup",
    "version": "0.0.0",
    "description": "Basic setup of Grunt.js",
    "private": true,
    "scripts": {
        "test": "grunt test"
    },
    "dependencies": {}
}
```

- Install the latest grunt module and save it to devDependencies
- `$ npm install grunt --save-dev`

```javascript
{
    "name": "grunt-setup",
    "version": "0.0.0",
    "description": "Basic setup of Grunt.js",
    "private": true,
    "scripts": {
        "test": "grunt test"
    },
    "devDependencies": {
        "grunt": "~0.4.2",
    },
    "dependencies": {}
}
```

## Install JSHint

Validate files with JSHint.

- [npm grunt-contrib-jshint][grunt-contrib-jshint]
- `$ npm install grunt-contrib-jshint --save-dev`

```javascript
{
    "name": "grunt-setup",
    "version": "0.0.0",
    "description": "Basic setup of Grunt.js",
    "private": true,
    "scripts": {
        "test": "grunt test"
    },
    "devDependencies": {
        "grunt": "~0.4.2",
        "grunt-contrib-jshint": "~0.7.2",
    },
    "dependencies": {}
}
```

## Install Jasmine

Run jasmine specs headlessly through PhantomJS.

- [npm grunt-contrib-jasmine][grunt-contrib-jasmine]
- `$ npm install grunt-contrib-jasmine --save-dev`

```javascript
{
    "name": "grunt-setup",
    "version": "0.0.0",
    "description": "Basic setup of Grunt.js",
    "private": true,
    "scripts": {
        "test": "grunt test"
    },
    "devDependencies": {
        "grunt": "~0.4.2",
        "grunt-contrib-jshint": "~0.7.2",
        "grunt-contrib-jasmine": "~0.5.2"
    },
    "dependencies": {}
}
```

## Install Uglify

Minify files with UglifyJS.

- [npm grunt-contrib-uglify][grunt-contrib-uglify]
- `$ npm install grunt-contrib-uglify --save-dev`

```javascript
{
    "name": "grunt-setup",
    "version": "0.0.0",
    "description": "Basic setup of Grunt.js",
    "private": true,
    "scripts": {
        "test": "grunt test"
    },
    "devDependencies": {
        "grunt": "~0.4.2",
        "grunt-contrib-jshint": "~0.7.2",
        "grunt-contrib-jasmine": "~0.5.2",
        "grunt-contrib-uglify": "~0.2.7"
    },
    "dependencies": {}
}
```

## Add Gruntfile.js

- Add a new file `Gruntfile.js` to `root` of your project next to `package.json`

```javascript
'use strict';

module.exports = function(grunt) {

    // Project configuration
    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        jshint: {
            options: {
                jshintrc: '.jshintrc'
            },
            src: [
                'Gruntfile.js',
                'test/**/*.js',
                'public/js/**/*.js'
            ]
        },
        jasmine : {
            options : {
                specs : 'test/**/*.js'
            },
            src : 'public/js/**/*.js'
        },
        uglify: {
            options: {
                banner: '/*! <%= pkg.name %> - v<%= pkg.version %>' 
                + ' - <%= grunt.template.today("yyyy-mm-dd HH:MM:ss") %> */\n'
            },
            build: {
                src: 'public/js/myModule.js',
                dest: 'public/build/js/myModule.min.js'
            }
        }
    });

    // Load plugins
    grunt.loadNpmTasks('grunt-contrib-jshint');
    grunt.loadNpmTasks('grunt-contrib-jasmine');
    grunt.loadNpmTasks('grunt-contrib-uglify');

    // Tasks
    grunt.registerTask('test', ['jshint', 'jasmine']);
    grunt.registerTask('default', ['test']);
    grunt.registerTask('uglify', ['test', 'uglify']);
};
```
## Run Grunt Tasks

- Run test tasks by `$ grunt test` or `$ npm test` or just `$ grunt`
- Run uglify task by `$ grunt uglify`

[grunt.js]: http://gruntjs.com/
[package.json]: https://npmjs.org/doc/json.html

[grunt-cli]: https://npmjs.org/package/grunt-cli
[grunt-contrib-jshint]: https://npmjs.org/package/grunt-contrib-jshint
[grunt-contrib-uglify]: https://npmjs.org/package/grunt-contrib-uglify
[grunt-contrib-jasmine]: https://npmjs.org/package/grunt-contrib-jasmine