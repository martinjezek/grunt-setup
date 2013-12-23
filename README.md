# Grunt - Setup

A few thoughts how to set up Grunt - The JavaScript Task Runner.

- [Grunt: The JavaScript Task Runner][grunt.js]

## Install Grunt-CLI:

Install `grunt-cli` globally and you'll have access to the grunt command anywhere on your system.
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
    "private": true
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
    "devDependencies": {
        "grunt": "~0.4.2",
    }
}
```

## Install JSHint

- `$ npm install grunt-contrib-jshint --save-dev`

```javascript
{
    "name": "grunt-setup",
    "version": "0.0.0",
    "description": "Basic setup of Grunt.js",
    "private": true,
    "devDependencies": {
        "grunt": "~0.4.2",
        "grunt-contrib-jshint": "~0.7.2",
    }
}
```

## Install Uglify

- `$ npm install grunt-contrib-uglify --save-dev`

```javascript
{
    "name": "grunt-setup",
    "version": "0.0.0",
    "description": "Basic setup of Grunt.js",
    "private": true,
    "devDependencies": {
        "grunt": "~0.4.2",
        "grunt-contrib-jshint": "~0.7.2",
        "grunt-contrib-uglify": "~0.2.7"
    }
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
            files: ['Gruntfile.js', 'public/js/**/*.js'],
            options: grunt.file.readJSON('.jshintrc')
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

    // Load the plugins
    grunt.loadNpmTasks('grunt-contrib-jshint');
    grunt.loadNpmTasks('grunt-contrib-uglify');

    // Default tasks.
    grunt.registerTask('default', ['jshint', 'uglify']);

    // Test tasks.
    grunt.registerTask('test', ['jshint']);
};
```
## Run Grunt Tasks

- Run default tasks by `$ grunt`
- Run specific tasks by `$ grunt test`

[grunt.js]: http://gruntjs.com/
[package.json]: https://npmjs.org/doc/json.html