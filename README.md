# jQuery Mobile demo 勝手に日本語化プロジェクト

jQuery Mobileの[デモ](http://jquerymobile.com/demos/)を勝手に日本語訳するプロジェクトです。  
[現存する日本語リファレンス](http://dev.screw-axis.com/doc/jquery_mobile/)はjQM1.1Finalに準じてい、現時点の最新版(1.4.2)に比べ古いものとなってしまっています。そのため、最新のjQueryMobileに対応できるものを作ろう、というのがこのプロジェクトです。

jQuery Mobile1.3以来、従来のdemoに加え、別途documentationが作られています。このプロジェクトで扱っているのはdemoです。なお、本家プロジェクト最新版に準拠しています。常に最新になっているわけではありませんが、出来るだけ本家の更新はマージしていく予定です。

## 現時点でのバージョン

jQuery Mobile 1.4.2+  
公開先 : http:// (仮)  



## このプロジェクトでは翻訳者を募集しています。

全ての翻訳を一度に出来るほど人間は器用ではありません。()
すこしでも早くこのデモを完成させるべく、またよりよい翻訳のため、協力してくれる方をお待ちしています。

このプロジェクトをForkして編集、コミットし、ご自身のリポジトリにPushしたものをPullReqしていただければ、当方で判断した後このプロジェクトに反映致します。


## 以下はjQuery MobileのREADMEになります。  

# jQuery Mobile [![Build Status](https://travis-ci.org/jquery/jquery-mobile.png?branch=master)](https://travis-ci.org/jquery/jquery-mobile) [![Coverage Status](https://coveralls.io/repos/jquery/jquery-mobile/badge.png?branch=master)](https://coveralls.io/r/jquery/jquery-mobile?branch=master)

This is the main repository for the jQuery Mobile project. From the [official website](http://jquerymobile.com):

> A unified, HTML5-based user interface system for all popular mobile device platforms, built on the rock-solid jQuery and jQuery UI foundation. Its lightweight code is built with progressive enhancement, and has a flexible, easily themeable design.

jQuery Mobile 1.4.x works with versions of jQuery core from 1.8.3 to 1.10.2 / 2.0.3. You can find more information about how the library works, and what it is capable of, by reading the [documentation](http://api.jquerymobile.com) and exploring the [demos](http://demos.jquerymobile.com/).

## Contributing

You can contribute to the project by reporting issues, suggesting new features, or submitting pull requests.
Please read our [Contributing Guidelines](https://github.com/jquery/jquery-mobile/blob/master/CONTRIBUTING.md) before submitting.


## Build/Customization

Currently the library is shipped on the jQuery CDN/download as a single monolithic JavaScript file that depends on jQuery Core (not included) and a similarly bundled CSS file. For users we support the following build targets:

* `js` - resolve dependencies, build, concat, and minify the JavaScript used for jQuery Mobile
* `css` - resolve dependencies, build, concat, and minify all the css, just the structure css, and just the theme css
* `demos` - build the js and css, and make the docs ready for static consumption
* `dist` (default target) - all of the above
* `lint` - Validates JavaScript files using [JSHint](http://jshint.com/)

### Download Builder

The easiest way to obtain a custom build is to use the [download builder](http://jquerymobile.com/download-builder/). With it, you can select the parts of the library you need and both the CSS and JavaScript dependencies will be resolved for you as a packaged/minified whole.

### Requirements

* [node.js](http://nodejs.org/) ~0.8.22
* [grunt-cli](http://gruntjs.com/)

### Commands

With node and grunt installed you can run the default target by simply issuing the following from the project root:

    npm install
    grunt

### JavaScript

As of version 1.1 the library uses dependency management in the JavaScript build by providing [AMD modules](https://github.com/amdjs/amdjs-api/wiki/AMD) which can be added or removed from the core mobile meta module `js/jquery.mobile.js`.

For example, if a user wished to exclude the form widgets to reduce the wire weight of their jQuery Mobile include they would first remove them from the meta module:

```diff
diff --git a/js/jquery.mobile.js b/js/jquery.mobile.js
index 6200fe6..3a4625c 100644
--- a/js/jquery.mobile.js
+++ b/js/jquery.mobile.js
@@ -19,12 +19,6 @@ define([
        './jquery.mobile.listview.filter',
        './jquery.mobile.listview.autodividers',
        './jquery.mobile.nojs',
-       './jquery.mobile.forms.checkboxradio',
-       './jquery.mobile.forms.button',
-       './jquery.mobile.forms.slider',
-       './jquery.mobile.forms.textinput',
-       './jquery.mobile.forms.select.custom',
-       './jquery.mobile.forms.select',
        './jquery.mobile.buttonMarkup',
        './jquery.mobile.controlGroup',
        './jquery.mobile.links',
```

And then run the build:

    grunt js

### CSS

To create a new theme:

1. Copy the `default` folder from CSS/Themes to a new folder named after your new theme (eg, `my-theme`).
2. Add customizations to the `jquery.mobile.theme.css` file.
3. From the project root run the following `grunt` command:

        THEME=my-theme grunt css

4. The output will be available in the `$PROJECT_ROOT/dist`

Again this assumes the theme css files are available in the `css/themes/$THEME/` directory relative to the project root, `css/themes/my-theme/` in the example.

## Development

The root of the repository is also the root of the documentation and, along with the test suite, acts as the test bed for bug fixes and features. You'll need to set up a server and get the test suite running before you can contribute patches.

### Server

Most of the documentation and testing pages rely on PHP 5+, and as a result Apache and PHP are required for development. You can install them using one of the following methods:

* one-click - [MAMP](http://www.mamp.info/en/downloads/index.html) for OSX, [XAMP](http://www.apachefriends.org/en/xampp.html) for OSX/Windows
* existing web server - eg, `~/Sites` directory on OSX.
* virtual machine - If [Vagrant](http://vagrantup.com) is installed you can add [this remote/branch](https://github.com/johnbender/jquery-mobile/tree/vagrant) and `vagrant up`

In addition to vanilla Apache the following modules are required:

* Rewrite (mod\_rewrite.so)
* Expire (mod\_expires.so)
* Header (mod\_headers.so)

Once you have your web server setup you can point it at the project directory.

### Testing

Automated testing forms the backbone of the jQuery Mobile project's QA activities. As a contributor or patch submitter you will be expected to run the test suite for the code your patches affect. Our continuous integration server will address the remainder of the test suite.

You can run all the test suites by running the following command:

    grunt test

You can choose to run only a subset of the tests by adding the `--suites` option like:

    grunt test --suites=button,slider

will only run the tests under `tests/unit/button/` and `tests/unit/slider/`.

You can also exclude some tests buy using `!`.  For instance:

    grunt test --type=integration --suites=!navigation

will run all the integration tests but the navigation suite.

You can also specify which versions of jQuery you want to test jQuery Mobile by using the `--jqueries` option:

    grunt test --jqueries=1.8.3,git

Additionally, jQuery Mobile's test suite is split between integration and unit tests. Where the unit tests are meant to focus on a single piece of the library (eg, a widget) and the integration tests require multiple pieces of the library to function. You can target either type by including the `--types` option when testing:

    grunt test --types=unit
    grunt test --types=integration
    grunt test --types=unit,integration # default, equivalent to 'grunt test'
