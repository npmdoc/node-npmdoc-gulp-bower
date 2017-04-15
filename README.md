# api documentation for  [gulp-bower (v0.0.13)](https://github.com/zont/gulp-bower#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp-bower.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp-bower) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp-bower.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp-bower)
#### Install Bower packages.

[![NPM](https://nodei.co/npm/gulp-bower.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/gulp-bower)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp-bower/build/screenCapture.buildCi.browser.apidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp-bower/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp-bower/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp-bower/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Alexander Zonov"
    },
    "bugs": {
        "url": "https://github.com/zont/gulp-bower/issues"
    },
    "dependencies": {
        "bower": "^1.3.12",
        "gulp-util": "^3.0.1",
        "inquirer": "^0.11.2",
        "through2": "0.6.2",
        "walk": "2.3.3"
    },
    "description": "Install Bower packages.",
    "devDependencies": {
        "chai": "^3.4.1",
        "event-stream": "^3.3.2",
        "gulp": "latest",
        "gulp-codecov.io": "^1.0.1",
        "gulp-istanbul": "^0.10.3",
        "gulp-jshint": "latest",
        "gulp-mocha": "^2.2.0",
        "jshint": "^2.9.1",
        "mocha": "^2.3.4",
        "rimraf": "^2.5.0",
        "sinon": "^1.17.2",
        "sinon-chai": "^2.8.0",
        "stream-assert": "^2.0.3"
    },
    "directories": {},
    "dist": {
        "shasum": "7ca4e3c5a599d08fada2b1c054cce8cde4e74235",
        "tarball": "https://registry.npmjs.org/gulp-bower/-/gulp-bower-0.0.13.tgz"
    },
    "engines": {
        "node": ">=0.8"
    },
    "gitHead": "ca2847d92310ee9fa61e2cc8f05097bb36c334c0",
    "homepage": "https://github.com/zont/gulp-bower#readme",
    "keywords": [
        "gulpplugin",
        "bower"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "alexander.zonov"
        }
    ],
    "name": "gulp-bower",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git://github.com/zont/gulp-bower.git"
    },
    "scripts": {
        "test": "node node_modules/gulp/bin/gulp.js post-coverage && node node_modules/gulp/bin/gulp.js lint"
    },
    "version": "0.0.13"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp-bower](#apidoc.module.gulp-bower)
1.  [function <span class="apidocSignatureSpan"></span>gulp-bower (opts, cmdArguments)](#apidoc.element.gulp-bower.gulp-bower)
1.  [function <span class="apidocSignatureSpan">gulp-bower.</span>toString ()](#apidoc.element.gulp-bower.toString)



# <a name="apidoc.module.gulp-bower"></a>[module gulp-bower](#apidoc.module.gulp-bower)

#### <a name="apidoc.element.gulp-bower.gulp-bower"></a>[function <span class="apidocSignatureSpan"></span>gulp-bower (opts, cmdArguments)](#apidoc.element.gulp-bower.gulp-bower)
- description and source-code
```javascript
function gulpBower(opts, cmdArguments) {
    opts = parseOptions(opts);

    log.info('Using cwd: ' + opts.cwd);
    log.info('Using bower dir: ' + opts.directory);

    cmdArguments = createCmdArguments(cmdArguments, opts);
    var bowerCommand = getBowerCommand(cmd);

    var stream = through.obj(function (file, enc, callback) {
        this.push(file);
        callback();
    });

    bowerCommand.apply(bower.commands, cmdArguments)
        .on('log', function (result) {
            log.info(['bower', gutil.colors.cyan(result.id), result.message].join(' '));
        })
        .on('prompt', function (prompts, callback) {
            if (enablePrompt === true) {
                inquirer.prompt(prompts, callback);
            } else {
                var error = 'Can\'t resolve suitable dependency version.';
                log.error(error);
                log.error('Set option { interactive: true } to select.');
                throw new gutil.PluginError(PLUGIN_NAME, error);
            }
        })
        .on('error', function (error) {
            stream.emit('error', new gutil.PluginError(PLUGIN_NAME, error));
            stream.emit('end');
        })
        .on('end', function () {
            writeStreamToFs(opts, stream);
        });

    return stream;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp-bower.toString"></a>[function <span class="apidocSignatureSpan">gulp-bower.</span>toString ()](#apidoc.element.gulp-bower.toString)
- description and source-code
```javascript
toString = function () {
    return toString;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
