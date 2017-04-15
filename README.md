# api documentation for  [gulp.spritesmith (v6.4.0)](https://github.com/twolfson/gulp.spritesmith)  [![npm package](https://img.shields.io/npm/v/npmdoc-gulp.spritesmith.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-gulp.spritesmith) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-gulp.spritesmith.svg)](https://travis-ci.org/npmdoc/node-npmdoc-gulp.spritesmith)
#### Convert a set of images into a spritesheet and CSS variables via gulp

[![NPM](https://nodei.co/npm/gulp.spritesmith.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/gulp.spritesmith)

[![apidoc](https://npmdoc.github.io/node-npmdoc-gulp.spritesmith/build/screenCapture.buildCi.browser.apidoc.html.png)](https://npmdoc.github.io/node-npmdoc-gulp.spritesmith/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-gulp.spritesmith/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-gulp.spritesmith/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Todd Wolfson",
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
            "name": "twolfson"
        }
    ],
    "name": "gulp.spritesmith",
    "optionalDependencies": {},
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
1.  [function <span class="apidocSignatureSpan">gulp.</span>spritesmith (params)](#apidoc.element.gulp.spritesmith.spritesmith)
1.  [function <span class="apidocSignatureSpan">gulp.spritesmith.</span>toString ()](#apidoc.element.gulp.spritesmith.toString)



# <a name="apidoc.module.gulp.spritesmith"></a>[module gulp.spritesmith](#apidoc.module.gulp.spritesmith)

#### <a name="apidoc.element.gulp.spritesmith.spritesmith"></a>[function <span class="apidocSignatureSpan">gulp.</span>spritesmith (params)](#apidoc.element.gulp.spritesmith.spritesmith)
- description and source-code
```javascript
function gulpSpritesmith(params) {
  var imgName = params.imgName;
  var cssName = params.cssName;
  assert(imgName, 'An 'imgName' parameter was not provided to 'gulp.spritesmith' (required)');
  assert(cssName, 'A 'cssName' parameter was not provided to 'gulp.spritesmith' (required)');

  // If there are settings for retina, verify our all of them are present
  var retinaSrcFilter = params.retinaSrcFilter;
  var retinaImgName = params.retinaImgName;
  if (retinaSrcFilter || retinaImgName) {
    assert(retinaSrcFilter && retinaImgName, 'Retina settings detected. We must have both 'retinaSrcFilter' and ' +
      ''retinaImgName' provided for retina to work');
  }

  // Define our output streams
  var imgStream = through2.obj();
  var cssStream = through2.obj();

  // Create a stream to take in images
  var images = [];
  var onData = function (file, encoding, cb) {
    images.push(file);
    cb();
  };

  // When we have completed our input
  var onEnd = function (cb) {
    // If there are no images present, exit early
    // DEV: This is against the behavior of 'spritesmith' but pro-gulp
    // DEV: See https://github.com/twolfson/gulp.spritesmith/issues/17
    if (images.length === 0) {
      imgStream.push(null);
      cssStream.push(null);
      return cb();
    }

    // Determine the format of the image
    var imgOpts = params.imgOpts || {};
    var imgFormat = imgOpts.format || imgFormats.get(imgName) || 'png';

    // Set up the defautls for imgOpts
    imgOpts = _.defaults({}, imgOpts, {format: imgFormat});

    // If we have retina settings, filter out the retina images
    var retinaImages;
    if (retinaSrcFilter) {
      // Filter out our retina files
      // https://github.com/wearefractal/glob-stream/blob/v5.0.0/index.js#L84-L87
      retinaImages = [];
      var retinaSrcPatterns = Array.isArray(retinaSrcFilter) ? retinaSrcFilter : [retinaSrcFilter];
      images = images.filter(function filterSrcFile (file) {
        // If we have a retina file, filter it out
        var matched = retinaSrcPatterns.some(function matchMinimatches (retinaSrcPattern) {
          var minimatch = new Minimatch(unrelative(file.cwd, retinaSrcPattern));
          return minimatch.match(file.path);
        });
        if (matched) {
          retinaImages.push(file);
          return false;
        // Otherwise, keep it in the src files
        } else {
          return true;
        }
      });

      // If we have a different amount of normal and retina images, complain and leave
      if (images.length !== retinaImages.length) {
        var err = new Error('Retina settings detected but ' + retinaImages.length + ' retina images were found. ' +
          'We have ' + images.length + ' normal images and expect these numbers to line up. ' +
          'Please double check 'retinaSrcFilter'.');
        err.images = images;
        err.retinaImages = retinaImages;
        this.emit('error', err);
        imgStream.push(null);
        cssStream.push(null);
        return cb();
      }
    }

    // Prepare spritesmith parameters
    var spritesmithParams = {
      engine: params.engine,
      algorithm: params.algorithm,
      padding: params.padding || 0,
      algorithmOpts: params.algorithmOpts || {},
      engineOpts: params.engineOpts || {},
      exportOpts: imgOpts
    };
    var that = this;

    // Construct our spritesmiths
    var spritesmith = new Spritesmith(spritesmithParams);
    var retinaSpritesmithParams;
    var retinaSpritesmith;
    if (retinaImages) {
      retinaSpritesmithParams = _.defaults({
        padding: spritesmithParams.padding * 2
      }, spritesmithParams);
      retinaSpritesmith = new Spritesmith(retinaSpritesmithParams);
    }

    // In parallel
    async.parallel([
      // Load in our normal images
      function generateNormalImages (callback) {
        spritesmith.createImages(images, callback);
      },
      // If we have retina images, load them in as well
      function generateRetinaSpritesheet (callback) {
        if (retinaImages) {
          retinaSpritesmith.createImages(retinaImage ...
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.gulp.spritesmith.toString"></a>[function <span class="apidocSignatureSpan">gulp.spritesmith.</span>toString ()](#apidoc.element.gulp.spritesmith.toString)
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
