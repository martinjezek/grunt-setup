# Grunt - Setup

A few thoughts how to set up Grunt - The JavaScript Task Runner.

- [Grunt: The JavaScript Task Runner][grunt.js]

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
        "grunt-contrib-uglify": "~0.2.7"
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
        "grunt-contrib-uglify": "~0.2.7",
        "grunt-contrib-jasmine": "~0.5.2"
    },
    "dependencies": {}
}
```

## Add Gruntfile.js

- Add a new file `Gruntfile.js` to `root` of your project next to `package.json`

```javascript
'use strict';

module.exports = function(grunt) {

    // Project configuration.
    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        jshint: {
            options: {
                jshintrc: '.jshintrc'
            },
            all: [
                'Gruntfile.js',
                'spec/**/*.js',
                'public/js/**/*.js'
            ]
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
        },
        jasmine : {
            options : {
                specs : 'spec/**/*.js'
            },
            all : 'public/js/**/*.js'
        }
    });

    // Load the plugins
    grunt.loadNpmTasks('grunt-contrib-jshint');
    grunt.loadNpmTasks('grunt-contrib-uglify');
    grunt.loadNpmTasks('grunt-contrib-jasmine');

    // Default tasks.
    grunt.registerTask('default', ['test', 'uglify']);

    // Test tasks.
    grunt.registerTask('test', ['jshint', 'jasmine']);
};
```
## Run Grunt Tasks

- Run default tasks by `$ grunt`
- Run specific tasks by `$ grunt test`

[grunt.js]: http://gruntjs.com/
[package.json]: https://npmjs.org/doc/json.html

[grunt-cli]: https://npmjs.org/package/grunt-cli
[grunt-contrib-jshint]: https://npmjs.org/package/grunt-contrib-jshint
[grunt-contrib-uglify]: https://npmjs.org/package/grunt-contrib-uglify
[grunt-contrib-jasmine]: https://npmjs.org/package/grunt-contrib-jasmine