# api documentation for  [gulp.spritesmith (v6.4.0)](https://github.com/twolfson/gulp.spritesmith)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp.spritesmith.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp.spritesmith) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp.spritesmith.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp.spritesmith)
#### Convert a set of images into a spritesheet and CSS variables via gulp

[![NPM](https://nodei.co/npm/gulp.spritesmith.png?downloads=true)](https://www.npmjs.com/package/gulp.spritesmith)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp.spritesmith/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-gulp.spritesmith_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp.spritesmith/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-gulp.spritesmith/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "Todd Wolfson",
        "email": "todd@twolfson.com",
        "url": "http://twolfson.com/"
    },
    "bugs": {
        "url": "https://github.com/twolfson/gulp.spritesmith/issues"
    },
    "dependencies": {
        "async": "~2.1.5",
        "gulp-util": "~3.0.8",
        "minimatch": "~3.0.3",
        "spritesheet-templates": "~10.2.0",
        "spritesmith": "~3.1.0",
        "through2": "~2.0.3",
        "underscore": "~1.8.3",
        "url2": "~1.0.4"
    },
    "description": "Convert a set of images into a spritesheet and CSS variables via gulp",
    "devDependencies": {
        "foundry": "~4.3.2",
        "foundry-release-git": "~2.0.2",
        "foundry-release-npm": "~2.0.2",
        "gulp": "~3.9.1",
        "gulp-csso": "~3.0.0",
        "gulp-imagemin": "~3.1.1",
        "js-yaml": "~3.8.2",
        "jscs": "~3.0.7",
        "jshint": "~2.9.4",
        "merge-stream": "~1.0.1",
        "mocha": "~3.2.0",
        "phantomjssmith": "~1.0.0",
        "pngparse": "~2.0.1",
        "rimraf": "~2.6.1",
        "twolfson-style": "~1.6.0",
        "vinyl-buffer": "~1.0.0"
    },
    "directories": {},
    "dist": {
        "shasum": "12cf0556d266bc49bc8fcd2016d453e493cc5786",
        "tarball": "https://registry.npmjs.org/gulp.spritesmith/-/gulp.spritesmith-6.4.0.tgz"
    },
    "engines": {
        "node": ">= 0.10.0"
    },
    "foundry": {
        "releaseCommands": [
            "foundry-release-git",
            "foundry-release-npm"
        ]
    },
    "gitHead": "0bf41c6f4c72da816b0c38d6266a881eaedd86d8",
    "homepage": "https://github.com/twolfson/gulp.spritesmith",
    "keywords": [
        "gulpplugin",
        "spritesmith",
        "sprite",
        "spritesheet"
    ],
    "license": "Unlicense",
    "main": "lib/gulp-spritesmith",
    "maintainers": [
        {
            "name": "twolfson",
            "email": "todd@twolfson.com"
        }
    ],
    "name": "gulp.spritesmith",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/twolfson/gulp.spritesmith.git"
    },
    "scripts": {
        "lint": "twolfson-style lint docs/ lib/ test/",
        "precheck": "twolfson-style precheck docs/ lib/ test/",
        "pretest": "twolfson-style install",
        "test": "npm run precheck && cd test && mocha . --timeout 60000 && cd .. && npm run lint"
    },
    "version": "6.4.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module gulp.spritesmith](#apidoc.module.gulp.spritesmith)



# <a name="apidoc.module.gulp.spritesmith"></a>[module gulp.spritesmith](#apidoc.module.gulp.spritesmith)



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
