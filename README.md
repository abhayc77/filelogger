Cordova File Logger
==========

Logger module for Cordova/Ionic projects.

When you run your application in device the Logger writes in the local filesystem (with cordova-plugin-file) and the system logs (with console.log).

When you run your application in browser with „ionic serve” the Logger uses browsers localStorage and the browser console (with console.log).

## Dependencies

- [ngCordova](http://ngcordova.com/)
- [org.apache.cordova.file](https://github.com/apache/cordova-plugin-file)

## Installation

Install manually, or from bower:

```bash
$ bower install filelogger
```

Include *filelogger.min.js* and ng-cordova.js or *ng-cordova.min.js* in your index.html file before cordova.js and after your AngularJS / Ionic file (since ngCordova depends on AngularJS).

```html
<script src="lib/ngCordova/dist/ng-cordova.min.js"></script>
<script src="lib/filelogger/dist/filelogger.min.js"></script>
<script src="cordova.js"></script>
```

## Usage

### $fileLogger.log()

General logger method. The first parameter is the log level (debug, info, warn, error). The following parameters are the message parts.
You can put here any javascript type (string, number, boolean, object, array).

In the logfile every item starts with the current UTC timestamp, followed by the log level and the message.

### $fileLogger.setStorageFilename()

You can set the local filename (default messages.log). It requests one parameter, the filename (type string).

### $fileLogger.getLogfile()

You can read the whole logfile from the filestore. This method returns a promise.

### $fileLogger.deleteLogfile()

You can delete the logfile from the filestore. This method returns a promise.



### Example use

```js
var app = angular.module('starter', ['ionic', 'fileLogger']);

app.controller('mainCtrl', ['$scope', '$fileLogger', function($scope, $fileLogger) {

  function testing() {

    $fileLogger.setStorageFilename('myLog.txt');

    $fileLogger.log('debug', 'message');
    $fileLogger.log('info', 'message');
    $fileLogger.log('warn', 'message');
    $fileLogger.log('error', 'message');

    $fileLogger.log('error', 'error message', { code: 1, meaning: 'general' });

    $fileLogger.log('info', 'message', 123, [1, 2, 3], { a: 1, b: '2' });

    $fileLogger.getLogfile().then(function(l) {
      console.log('Logfile content');
      console.log(l);
    });

    $fileLogger.deleteLogfile().then(function() {
      console.log('Logfile deleted');
    });

  }

}]);
```


## Author

#### Peter Bakondy

- https://github.com/pbakondy


## LICENSE

Cordova File Logger is licensed under the MIT Open Source license. For more information, see the LICENSE file in this repository.
