Ionic CLI

The Ionic Framework command line utility makes it easy to start, build, run, and emulate apps.

## Installing

```bash
$ npm install -g ionic
```

## Starting

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

## Add a Platform Target

```bash
$ ionic platform ios android
```

### Live Reload Application During Development

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

## Building

```bash
$ ionic build ios
```

## Emulating

Deploys the Ionic app on specified platform emulator. This is simply an alias for `run --emulator`.

```bash
$ ionic emulate ios [options]
```

## Running

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

## Serve

```bash
$ ionic serve [options]
```

### Options

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

#### Using Ionic Labs

We've extended the serve command to open the new Lab UI that features iOS and Android side-by-side.

```bash
$ ionic serve --lab
```

## Packaging

Using Ionic's service, you can compile and package your project into an app-store ready app without
requiring native SDKs on your machine.

```bash
$ ionic package debug android
```

The third argument can be either `debug` or `release`, and the last argument can be either `android` or `ios`.


# File ionic.project

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
