
Ionic-Cli
=========

The Ionic Framework command line utility makes it easy to start, build, run, and emulate [Ionic](http://ionicframework.com/) apps.

## Installing

```bash
$ npm install -g ionic
```

## Starting an Ionic App

```bash
$ ionic start myapp [template]
```

__Named template starters:__

* [tabs](https://github.com/driftyco/ionic-starter-tabs) (Default)
* [sidemenu](https://github.com/driftyco/ionic-starter-sidemenu)
* [maps](https://github.com/driftyco/ionic-starter-maps)
* [salesforce](https://github.com/driftyco/ionic-starter-salesforce)
* [complex-list](https://github.com/driftyco/ionic-starter-complex-list)
* [blank](https://github.com/driftyco/ionic-starter-blank)

## Adding a platform target

```bash
$ ionic platform ios android
```

## Testing in a Browser

```bash
$ ionic serve [options]
```

### Live Reload App During Development

__Command-line flags/options for `run` and `emulate`:__

    [--livereload|-l] .......  Live Reload app dev files from the device (beta)
    [--consolelogs|-c] ......  Print app console logs to Ionic CLI (live reload req.)
    [--serverlogs|-s] .......  Print dev server logs to Ionic CLI (live reload req.)
    [--port|-p] .............  Dev server HTTP port (8100 default, live reload req.)
    [--livereload-port|-i] ..  Live Reload port (35729 default, live reload req.)
    [--all|-a] ..............  Specify to run on all addresses, 0.0.0.0, so you can view externally
    [--browser|-w] ..........  Specifies the browser to use (safari, firefox, chrome)
    [--browseroption|-o] ....  Specifies a path to open to (/#/tab/dash)
    [--debug|--release]

While the server is running for live reload, you can use the following commands within the CLI:

    restart or r to restart the client app from the root
    goto or g and a url to have the app navigate to the given url
    consolelogs or c to enable/disable console log output
    serverlogs or s to enable/disable server log output
    quit or q to shutdown the server and exit

## Building your app

```bash
$ ionic build ios
```

## Emulating your app

Deploys the Ionic app on specified platform emulator. This is simply an alias for `run --emulator`.

```bash
$ ionic emulate ios [options]
```

## Running your app

Deploys the Ionic app on specified platform devices. If a device is not found it'll then deploy to an emulator/simulator.

```bash
$ ionic run ios [options]
```

### Icon Source Image

```bash
$ ionic resources --icon
```

### Splash Screen Source Image

```bash
$ ionic resources --splash
```
### Generating Icons and Splash Screens

To generate both icons and splash screens, follow the instructions above and run:

```bash
$ ionic resources
```

### Platform Specific Resource Images

One source image can be used to generate images for each platform by placing the file within the `resources` directory, such as `resources/icon.png`. To use different source images for individual platforms, place the source image in the respective platform's directory. For example, to use a different icon for Android, it should follow this path: `resources/android/icon.png`, and a different image for iOS would use this path: `resources/ios/icon.png`.

### Generating Exact Platform Resources

```bash
$ ionic resources ios
```





## Advanced serve options

__LiveReload__

By default, LiveReload will watch for changes in your `www/` directory,
excluding `www/lib/`.  To change this, you can specify a `watchPatterns`
property in the `ionic.project` file located in your project root to watch
(or not watch) for specific changes.

```json
{
  "name": "myApp",
  "app_id": "",
  "watchPatterns": [
    "www/js/*",
    "!www/css/**/*"
  ]
}
```

For a reference on glob pattern syntax, check out
[globbing patterns](http://gruntjs.com/configuring-tasks#globbing-patterns) on
the Grunt website.

__Gulp Integration__

When running `ionic serve`, you can have Ionic run any Gulp tasks you specify by putting them into your `ionic.project` as a `gulpStartupTasks` property as follows:

```json
{
  "name": "SmoothRiders",
   "gulpStartupTasks": [
    "watch"
  ]
}

```

Now, when you run `ionic serve`, it will run the `watch` task while starting the Ionic server.

If you would like to disable gulp from running during serve, pass the `--nogulp` option.

NOTE:

```bash
$ ionic setup sass
```

will add a `watchPatterns` propery with the default values to your `ionic.project`
file that you can then edit, in addition to the `gulpStartupTasks` property
described in the [Using Sass](https://github.com/driftyco/ionic-cli/blob/master/README.md#using-sass) section.


__Service Proxies:__

The `serve` command can add some proxies to the http server. These proxies are useful if you are developing in the browser and you need to make calls to an external API. With this feature you can proxy request to the external api through the ionic http server preventing the `No 'Access-Control-Allow-Origin' header is present on the requested resource` error.

In the `ionic.project` file you can add a property with an array of proxies you want to add. The proxies are object with the following properties:

* `path`: string that will be matched against the beginning of the incoming request URL.
* `proxyUrl`: a string with the url of where the proxied request should go.
* `proxyNoAgent`: (optional) true/false, if true opts out of connection pooling, see [HttpAgent](http://nodejs.org/api/http.html#http_class_http_agent)

```json
{
  "name": "appname",
  "email": "",
  "app_id": "",
  "proxies": [
    {
      "path": "/v1",
      "proxyUrl": "https://api.instagram.com/v1"
    }
  ]
}

```

Using the above configuration, you can now make requests to your local server at `http://localhost:8100/v1` to have it proxy out requests to `https://api.instagram.com/v1`

For example:

```js
angular.module('starter.controllers', [])
.constant('InstagramApiUrl', '')
// .contant('InstagramApiUrl','https://api.instagram.com')
//In production, make this the real URL

.controller('FeedCtrl', function($scope, $http, InstagramApiUrl) {

  $scope.feed = null;

  $http.get(InstagramApiUrl + '/v1/media/search?client_id=1&lat=48&lng=2.294351').then(function(data) {
    console.log('data ' , data)
    $scope.feed = data;
  })

})
```

See also [this gist](https://gist.github.com/jbavari/d9c1c94058c4fdd4e935) for more help.

__Command-line flags/options:__

    [--consolelogs|-c] ......  Print app console logs to Ionic CLI
    [--serverlogs|-s] .......  Print dev server logs to Ionic CLI
    [--port|-p] .............  Dev server HTTP port (8100 default)
    [--livereload-port|-i] ..  Live Reload port (35729 default)
    [--nobrowser|-b] ........  Disable launching a browser
    [--nolivereload|-r] .....  Do not start live reload
    [--noproxy|-x] ..........  Do not add proxies
    [--address] .............  Serves in the browser at the specified address
    [--lab] .................  Serves both iOS and Android in the browser
    [--nogulp] ..............  Serve without running gulp tasks
    [--platform|-t] .........  Serve the platform specific styles in the browser (ios/android)

## Using Ionic Labs

We've extended the serve command to open the new Lab UI that features iOS and Android side-by-side.

```bash
$ ionic serve --lab
```

If you've used the serve command before, you'll feel right at home with this one. Just like serve, it opens your app in a browser, but now it shows you what your app will look like on a phone, with both iOS and Android side by side.

And of course, it supports Live Reload and all the other goodies we've added over the last couple of months.

## Serving an alternate document root

If you'd like to test your app in the browser and you use a folder other than the default of `www`, you can specify this folder in your `ionic.project` file.

You might also want to have the document root be created if you use some sort of build system, we suggest using `createDocumentRoot` for that so that `ionic serve` will create that folder for you.

It is also advised you specify the watch patterns for this document root as well, as follows:

```json
{
  "name": "SmoothRiders",
   "gulpStartupTasks": [
    "watch"
  ],
  "documentRoot": "app",
  "createDocumentRoot": "app",
  "watchPatterns": [
    "app/js/*",
    "!app/css/**/*"
  ]
}

```

## Update Ionic lib

Update Ionic library files, which are found in the `www/lib/ionic` directory. If bower is being used
by the project, this command will automatically run `bower update ionic`, otherwise this command updates
the local static files from Ionic's CDN.

```bash
$ ionic lib update
```
*Note: Using bower? This command does not update Ionic's dependencies. Run `bower update` to update Ionic and all of it's dependencies defined in `bower.json`.*

## Packaging an app (beta)

Using Ionic's service, you can compile and package your project into an app-store ready app without
requiring native SDKs on your machine.

```bash
$ ionic package debug android
```

The third argument can be either `debug` or `release`, and the last argument can be either `android` or `ios`.


## Cordova Commands

Ionic uses Cordova underneath, so you can also substitute Cordova commands to prepare/build/emulate/run, or to add additional plugins.

*Note: we occasionally send anonymous usage statistics to the Ionic team to make the tool better.*

## Working around proxies

If you have a proxy you need to get around, you can pass that proxy with the default `http_proxy` [node environment variable](https://www.npmjs.org/doc/misc/npm-config.html#proxy) or an environment variable `proxy`.

A few ways to set up and use the environment variable:

```bash
export http_proxy=internal.proxy.com
# Or
export PROXY=internal.proxy.com

ionic start my_app

# Additionally, pass in line
PROXY=internal.proxy.com ionic start my_app
```


## Using Sass

By default, starter projects are hooked up to Ionic's precompiled CSS file, which is found in the project's `www/lib/ionic/css` directory, and is linked to the app in the head of the root `index.html` file. However, Ionic projects can also be customized using [Sass](http://sass-lang.com/), which gives developers and designers "superpowers" in terms of creating and maintaining CSS. Below are two ways to setup Sass for your Ionic project (the `ionic setup sass` command simply does the manual steps for you). Once Sass has been setup for your Ionic project, then the `ionic serve` command will also watch for Sass changes.

#### Setup Sass Automatically

    ionic setup sass


#### Setup Sass Manually

1. Run `npm install` from the working directory of an Ionic project. This will install [gulp.js](http://gulpjs.com/) and a few handy tasks, such as [gulp-sass](https://www.npmjs.org/package/gulp-sass) and [gulp-minify-css](https://www.npmjs.org/package/gulp-minify-css).
2. Remove `<link href="lib/ionic/css/ionic.css" rel="stylesheet">` from the `<head>` of the root `index.html` file.
3. Remove `<link href="css/style.css" rel="stylesheet">` from the `<head>` of the root `index.html` file.
4. Add `<link href="css/ionic.app.css" rel="stylesheet">` to the `<head>` of the root `index.html` file.
5. In the `ionic.project` file, add the JavaScript property `"gulpStartupTasks": ["sass", "watch"]` (this can also be customized to whatever gulp tasks you'd like).


# Ionic.io services

The CLI supports operations to use backend services for your Ionic app. To get started, [visit the ionic.io homepage](http://ionic.io) and [sign up there](https://apps.ionic.io/signup).

There are a few things you can utilize the CLI for to support ease of development.

## Login

Type `ionic login` to get logged in the CLI.

### Login without prompt

You can pass the email and password to login without being prompted for email and password.

`ionic login --email user@ionic.io --password somepass`

### Login with environment variables

The CLI also supports settings environment variables to read off the email and password for the user.

Set `IONIC_EMAIL` and `IONIC_PASSWORD` as variables to have the CLI read these instead of being prompted for them.

## Upload your Ionic app

Use the `ionic upload` command to take your current application you are developing and upload it to the Ionic.io servers. 

Now you can use [the ionic view app](http://view.ionic.io/) to view that application or have others view the application.

After uploading the application, you will see a message:


```
Uploading app....

Successfully uploaded (f23j9fjs)
```

This indicates you uploaded the application correctly, and the App ID is set to `f23j9fjs`.

You can then view that App ID from the View app or the application listing on ionic.io.

### Adding a note with your upload

To add a note to your build, pass the `--note` option as follows: 

`ionic upload --note "This version of the application fixes the menu selections"`.

## Set your Ionic Project App ID manually

Use the `ionic link <appId>` command to set your Ionic App ID to continue working with the same app with the Ionic platform across development enviroments.

## Share the application with another user

Use the `ionic share <email>` command to have an email sent to another person to have them view the Ionic application you are using. Note: You must have an ionic.io account as well as the user you are sharing with.

# Ionic Docs

To get Ionic documentation from the Ionic CLI, try using the `ionic docs` command. The command will look up your currently used Ionic version and open the docs specific for that version. Ex: RC0, RC1, etc.

To view all docs, `ionic docs ls`.

To get help with a doc you may not remember, just type the name close enough: `ionic docs list` and you will be prompted for suggestions that may match.


# Ionic Hooks

Ionic provides some default hooks for you to use in your Cordova application. In versions prior to 1.3.18, these hooks were automatically installed via the `ionic platform` command. 

In 1.3.18, the hooks were automatically removed due to some errors users were having with Crosswalk and other plugins with variables. 

If you were a user who would still like to use those hooks, you can re-install these hooks with the `ionic hooks add` command.

If you would like to remove these hooks yourself, use `ionic hooks remove` to get rid of them.


# Ionic State

Ionic now provides a command to help you manage the state of your Ionic application. Previously Cordova hooks were used to save platforms and plugins to your `package.json` file.

Now when using `ionic platform add`, `ionic platform rm`, `ionic plugin add`, or `ionic plugin rm`, the state command will automatically be used to save the platform or plugin state to the `package.json` file.

If you would like to avoid saving plugins or platforms to the `package.json` file - pass in the `--nosave` option. (`ionic plugin add org.apache.cordova.file --nosave`).

Your package.json file might look something like the following:

```json
"cordovaPlatforms": [
  "ios",
  {
    "android": {
      "id": "android",
      "locator": "https://github.com/apache/cordova-android.git"
    }
  }
],
"cordovaPlugins": [
  "org.apache.cordova.device",
  "org.apache.cordova.console",
  "com.ionic.keyboard",
  "org.apache.cordova.splashscreen",
  {
    "locator": "https://github.com/MobileChromeApps/cordova-crosswalk-engine.git",
    "id": "org.cordova.croswalk"
  },
  {
    "locator": "/path/to/cloned/phonegap-facebook-plugin",
    "id": "",
    "variables": {
        "APP_ID": "some_id",
        "APP_NAME": "some_name"
    }
  }
]
```

## ionic state save

The `ionic state save` command does some lookup in your platforms and plugins to save the current state of your cordova application. 

First it looks in your platforms folder to see which platforms are installed, and saves the name and version in your `package.json` file under the `cordovaPlatforms` attribute.

Second it looks at your plugins `fetch.json` file to save the plugins installed both from the Cordova registry, locally installed plugins, as well as remote plugins from github or a remote HTTP url.

## ionic state restore

The `ionic state restore` command looks at the `cordovaPlugins` and `cordovaPlatforms` attributes in your `package.json` file to restore your application with those platforms and plugins.

In the package.json file, `cordovaPlugins` will be stored as just their `ID` if they are installed from the Cordova registry. However, if they are local or remote, they will be stored as an object with those properties. Also to note, variables are stored for plugins with variables like the Facebook connect plugin.

The `cordovaPlatforms` follow the same convention of either an `ID` for the platform name, if they are local or remote, they will be stored as an object with those properties.

If you'd like, you can populate the `cordovaPlugins` and `cordovaPlatforms` by hand, then use the `ionic state restore` command to get your app ready to go.

## ionic state clear

The `ionic state clear` method will clear out your platforms and plugins directories, as well as removing the `cordovaPlugins` and `cordovaPlaforms` attributes in your `package.json` file.

## ionic state reset

The `ionic state reset` method will first remove your platforms and plugins folders. Then it will look at your `package.json` file to re-install the platforms and plugins as specified there.

This command can be helpful for you to reinstall your plugins and platforms to get a fresh start.


# ionic.project file

The ionic.project is a configuration for an ionic project that stores the following:

* `app_id` - the associated app ID in ionic.io.  
* `browsers` - the installed browsers (CrossWalk).  
* `createDocumentRoot` - boolean setting stating to create the designated.document root upon serve (for CI, using `app` folder, and compiling)  
* `defaultBrowser` - the browser they prefer to use with `ionic serve`. Chrome, Firefox, etc.  
* `documentRoot` - the associated document root with HTML/JS/CSS files.  
* `gulpDependantTasks` - gulp tasks that are run before `ionic serve` launches. Think of `gulp build`, `gulp sass`, etc.  
* `gulpStartupTasks` - gulp tasks that are run and kept alive during `ionic serve`.  
* `imagePaths` - paths relative to document root that specify the release feature to compress images.  
* `proxies` - designated proxies to use during `ionic serve`.  
* `name` - the name of the application.  
* `sass` - the setting to watch sass during `ionic serve`.  
* `watchPatterns` - the patterns to watch and live reload during `ionic.serve`.  
