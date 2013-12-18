# Grunt - Setup

A few thoughts how to set up Grunt - The JavaScript Task Runner.

- [Grunt.js][grunt.js]

Install Grunt-CLI via NPM:

- `$ npm install grunt-cli -g`

Install Grunt to your project:

- you're at `root` of your project
- if you don't have a `package.json` then run `$ npm init` and fill in your project info
- find out more about [package.json][package.json]

```javascript
{
    "name": "grunt-setup",
    "version": "0.0.0",
    "description": "Basic setup of Grunt.js",
    "author": "Martin Jezek",
    "license": "MIT"
}
```

- install the latest grunt module and save it to devDependencies
- `$ npm install grunt --save-dev`
- install other great modules
- `$ npm install grunt-contrib-jshint --save-dev`
- `$ npm install grunt-contrib-uglify --save-dev`

```javascript
{
    "name": "grunt-setup",
    "version": "0.0.0",
    "description": "Basic setup of Grunt.js",
    "author": "Martin Jezek",
    "license": "MIT",
    "devDependencies": {
        "grunt": "~0.4.2",
        "grunt-contrib-jshint": "~0.7.2",
        "grunt-contrib-uglify": "~0.2.7"
    }
}
```

- add a new file 'Gruntfile.js' to 'root' of your project next to 'package.json'

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
                banner: '/*! <%= pkg.name %> - v<%= pkg.version %> - <%= grunt.template.today("yyyy-mm-dd") %> */\n'
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

- run default tasks by `$ grunt` or specific tasks by '$ grunt test'

[grunt.js]: http://gruntjs.com/
[package.json]: https://npmjs.org/doc/json.html