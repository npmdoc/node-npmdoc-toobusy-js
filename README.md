# api documentation for  [toobusy-js (v0.5.1)](https://github.com/STRML/node-toobusy)  [![npm package](https://img.shields.io/npm/v/npmdoc-toobusy-js.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-toobusy-js) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-toobusy-js.svg)](https://travis-ci.org/npmdoc/node-npmdoc-toobusy-js)
#### Don't fall over when your Node.JS server is too busy. Now without native dependencies!

[![NPM](https://nodei.co/npm/toobusy-js.png?downloads=true)](https://www.npmjs.com/package/toobusy-js)

[![apidoc](https://npmdoc.github.io/node-npmdoc-toobusy-js/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-toobusy-js_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-toobusy-js/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-toobusy-js/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-toobusy-js/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "bugs": {
        "url": "https://github.com/strml/node-toobusy/issues"
    },
    "dependencies": {},
    "description": "Don't fall over when your Node.JS server is too busy. Now without native dependencies!",
    "devDependencies": {
        "mocha": "1.7.0",
        "pre-commit": "^1.0.5",
        "should": "1.2.1"
    },
    "directories": {},
    "dist": {
        "shasum": "5511f78f6a87a6a512d44fdb0efa13672217f659",
        "tarball": "https://registry.npmjs.org/toobusy-js/-/toobusy-js-0.5.1.tgz"
    },
    "engines": {
        "node": ">=0.9.1"
    },
    "gitHead": "ce714acb8562dd4803334c5ac0a152bf79efcf48",
    "homepage": "https://github.com/STRML/node-toobusy",
    "license": "WTFPL",
    "maintainers": [
        {
            "name": "strml",
            "email": "samuel.trace.reed@gmail.com"
        }
    ],
    "name": "toobusy-js",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/strml/node-toobusy.git"
    },
    "scripts": {
        "test": "mocha tests"
    },
    "version": "0.5.1"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module toobusy-js](#apidoc.module.toobusy-js)
1.  [function <span class="apidocSignatureSpan">toobusy-js.</span>interval (newInterval)](#apidoc.element.toobusy-js.interval)
1.  [function <span class="apidocSignatureSpan">toobusy-js.</span>lag ()](#apidoc.element.toobusy-js.lag)
1.  [function <span class="apidocSignatureSpan">toobusy-js.</span>maxLag (newLag)](#apidoc.element.toobusy-js.maxLag)
1.  [function <span class="apidocSignatureSpan">toobusy-js.</span>onLag (fn, threshold)](#apidoc.element.toobusy-js.onLag)
1.  [function <span class="apidocSignatureSpan">toobusy-js.</span>shutdown ()](#apidoc.element.toobusy-js.shutdown)
1.  [function <span class="apidocSignatureSpan">toobusy-js.</span>smoothingFactor (newFactor)](#apidoc.element.toobusy-js.smoothingFactor)
1.  [function <span class="apidocSignatureSpan">toobusy-js.</span>started ()](#apidoc.element.toobusy-js.started)



# <a name="apidoc.module.toobusy-js"></a>[module toobusy-js](#apidoc.module.toobusy-js)

#### <a name="apidoc.element.toobusy-js.interval"></a>[function <span class="apidocSignatureSpan">toobusy-js.</span>interval (newInterval)](#apidoc.element.toobusy-js.interval)
- description and source-code
```javascript
interval = function (newInterval) {
  if (!newInterval) return interval;
  if (typeof newInterval !== "number") throw new Error("Interval must be a number.");

  newInterval = Math.round(newInterval);
  if(newInterval < 16) throw new Error("Interval should be greater than 16ms.");

  toobusy.shutdown();
  interval = newInterval;
  start();
  return interval;
}
```
- example usage
```shell
...
var toobusy = require('toobusy-js');

// Set maximum lag to an aggressive value.
toobusy.maxLag(10);

// Set check interval to a faster value. This will catch more latency spikes
// but may cause the check to be too sensitive.
toobusy.interval(250);

// Get current maxLag or interval setting by calling without parameters.
var currentMaxLag = toobusy.maxLag(), interval = toobusy.interval();

toobusy.onLag(function(currentLag) {
  console.log("Event loop lag detected! Latency: " + currentLag + "ms");
});
...
```

#### <a name="apidoc.element.toobusy-js.lag"></a>[function <span class="apidocSignatureSpan">toobusy-js.</span>lag ()](#apidoc.element.toobusy-js.lag)
- description and source-code
```javascript
lag = function (){
  return Math.round(currentLag);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.toobusy-js.maxLag"></a>[function <span class="apidocSignatureSpan">toobusy-js.</span>maxLag (newLag)](#apidoc.element.toobusy-js.maxLag)
- description and source-code
```javascript
maxLag = function (newLag){
  if(!newLag) return highWater;

  // If an arg was passed, try to set highWater.
  if (typeof newLag !== "number") throw new Error("MaxLag must be a number.");
  newLag = Math.round(newLag);
  if(newLag < 10) throw new Error("Maximum lag should be greater than 10ms.");

  highWater = newLag;
  return highWater;
}
```
- example usage
```shell
...
before we consider the process *too busy*.
'interval' - The check interval for measuring event loop lag, in ms.

'''javascript
var toobusy = require('toobusy-js');

// Set maximum lag to an aggressive value.
toobusy.maxLag(10);

// Set check interval to a faster value. This will catch more latency spikes
// but may cause the check to be too sensitive.
toobusy.interval(250);

// Get current maxLag or interval setting by calling without parameters.
var currentMaxLag = toobusy.maxLag(), interval = toobusy.interval();
...
```

#### <a name="apidoc.element.toobusy-js.onLag"></a>[function <span class="apidocSignatureSpan">toobusy-js.</span>onLag (fn, threshold)](#apidoc.element.toobusy-js.onLag)
- description and source-code
```javascript
onLag = function (fn, threshold) {

  if (typeof threshold === "number") {
    lagEventThreshold = threshold;
  } else {
    lagEventThreshold = toobusy.maxLag();
  }

  eventEmitter.on(LAG_EVENT, fn);
}
```
- example usage
```shell
...
// Set check interval to a faster value. This will catch more latency spikes
// but may cause the check to be too sensitive.
toobusy.interval(250);

// Get current maxLag or interval setting by calling without parameters.
var currentMaxLag = toobusy.maxLag(), interval = toobusy.interval();

toobusy.onLag(function(currentLag) {
  console.log("Event loop lag detected! Latency: " + currentLag + "ms");
});
'''

The default maxLag value is 70ms, and the default check interval is 500ms.
This allows an "average" server to run at 90-100% CPU
and keeps request latency at around 200ms.
...
```

#### <a name="apidoc.element.toobusy-js.shutdown"></a>[function <span class="apidocSignatureSpan">toobusy-js.</span>shutdown ()](#apidoc.element.toobusy-js.shutdown)
- description and source-code
```javascript
shutdown = function (){
  currentLag = 0;
  checkInterval = clearInterval(checkInterval);
}
```
- example usage
```shell
...
});

var server = app.listen(3000);

process.on('SIGINT', function() {
  server.close();
  // calling .shutdown allows your process to exit normally
  toobusy.shutdown();
  process.exit();
});
'''

## tunable parameters

The library exposes a few knobs:
...
```

#### <a name="apidoc.element.toobusy-js.smoothingFactor"></a>[function <span class="apidocSignatureSpan">toobusy-js.</span>smoothingFactor (newFactor)](#apidoc.element.toobusy-js.smoothingFactor)
- description and source-code
```javascript
smoothingFactor = function (newFactor){
  if(!newFactor) return smoothingFactor;

  if (typeof newFactor !== "number") throw new Error("NewFactor must be a number.");
  if(newFactor <= 0 || newFactor > 1) throw new Error("Smoothing factor should be in range ]0,1].");

  smoothingFactor = newFactor;
  return smoothingFactor;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.toobusy-js.started"></a>[function <span class="apidocSignatureSpan">toobusy-js.</span>started ()](#apidoc.element.toobusy-js.started)
- description and source-code
```javascript
started = function () {
  return !!checkInterval;
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
