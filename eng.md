# Easy JavaScript Documentation with YUIDocs and Grunt.js

Documenting code is a rough, but necessary evil. Having a well maintained and
documented code base can ease new developers into your code base and also help
keep tabs on certain pieces of your application.

## YUIDoc

YUIDoc is a node app that assists in parsing certain JavaScript comments out to
generate API documentation. Here are some of the basics of the syntax for
documentation.

It allows you to tag pieces of your application to be processed for later 
documentation.

For example if you were documenting something like jQuery you could something 
similar to...

    /**
    * The main jQuery class.
    * @class jQuery
    * @param {String} selector The selector for an element.
    * @param {String} [context] The context for the search.
    */
    jQuery = /* ... */

Then you can document methods also...

    /**
    * Use AJAX to retrieve data
    * @method ajax
    * @param {Object} options The request options
        @param {String} options.url The url of the request.
        @param {String} [options.type=get] The request type, defaults to `GET`.
    * @example
    This accepts markdown syntax!

        jQuery.ajax({ 
            url: 'foo/'
        });

    * @return {jQuery.Deferred}
    */ 
    jQuery.ajax = /* ... */

There are many other features in YUIDoc such as:

* `@extend` Specify what class this class inherits from
* `@for` Change the context of a given method in case it's being documented 
separately from it's class
* `@event` Document your application's events
* `@constructor` Specifies that this class can create an instance
* `@static` Specifies that this is a static class or method
* Many more!

Checkout the [syntax][1] for the other options.

## Building the documentation with Grunt

[Gruntjs][2] is a task runner for NodeJS. With it you can do run many tasks on 
your code such as JSHint, Concatenation, Minification, etc. There are hundereds 
of tasks written for Grunt.

There is a task for YUIDoc called [grunt-contrib-yuidoc][3]. To use YUIDoc in
your project, go through the basics of setting up a grunt project via
http://gruntjs.com/getting-started. Next, run the following command...

    npm install grunt-contrib-yuidoc --save

Next update your `Gruntfile.js` with the following...

    grunt.initConfig({
        pkg: grunt.file.readJSON('package.json'),
        yuidoc: {
            all: {
                name: '<%= pkg.name %>',
                description: '<%= pkg.description %>',
                version: '<%= pkg.version %>',
                url: '<%= pkg.homepage %>',
                options: {
                    paths: ['path/to/your/scripts'],
                    outdir: './docs/'
                }
            }
        }
    });

    grunt.loadNpmTasks("grunt-contrib-yuidoc");

    grunt.registerTask("docs", ["yuidoc"]);

Now you can run `grunt docs` and VOILA, you're documentation will be generated
and output to the `outdir` location.

## Conclusion

Documentation is very important in a project. While it can be tedious, it is
well worth it in the end. Most of the better open source libraries out there
became popular because of their documentation. Whether or not your project is
open source or not though, good documentation is crucial to the maintainability
of your app.

[1]: http://tech.pro/tutorial/1729/easy-javascript-documentation-with-yuidocs-and-gruntjs
[2]: http://gruntjs.com/
[3]: https://github.com/gruntjs/grunt-contrib-yuidoc