## ngPieChart

`ngPieChart` is an `Angular.js` lightweight plugin to render simple, animated and retina optimized pie charts.

* highly customizable
* very easy to implement
* independent resolution (retina optimized)
* uses `requestAnimationFrame` for smooth animations on modern devices
* works in all modern browsers, even in IE7+ with [excanvas](https://code.google.com/p/explorercanvas/wiki/Instructions)

## Features

* [Get started](#get-started)
    * [Installation](#installation)
    * [Angular.js](#angularjs)
* [Customize](#customize)
* [Events](#events)
* [Dynamic value](#dynamic-value)
* [Browser support](#browser-support)
* [License](#license)

## Get started

### Installation

Use [bower](http://www.bower.io) to install the component:

```
$ bower install --save angular-piechart
```

### Angular.js

To work, this plugin needs to be executed in an `Angular.js` application.

You need to include `css` and `javascript` files in your project.

```javascript
<html>
    <head>
        ...
        <script src="/path/to/bower/components/angular-piechart/dist/styles/angular-piechart.min.css"></script>
    </head>
    <body>
        ...
        <script src="/path/to/bower/components/angular/angular.min.js"></script>
        <script src="/path/to/bower/components/angular-piechart/dist/scripts/angular-piechart.min.js"></script>
    </body>
</html>
```

Once files loaded, you must include this plugin in your application:

```javascript
var app = angular.module('myApp', ['ngPieChart']);
```

Now, the directive is accessible in all `HTML` files of your application:

```javascript
<ngpiechart progression="35" total="100">
    <div>Content to display</div>
</ngpiechart>
```

Content to display will be centered in the middle of the pie chart. You can add as much content as you want until the limit size of your pie chart.

Add `CSS` for each line of your content to customize the view.

## Customize

You can add multiple attributes to the directive to set up a custom look and feel for that plugin.

| Attributes                  | Default       | Description
|:---------------------------:|:-------------:|:--------------
| **bar-color** | #ef1e25 | The color of the circular bar. You must write a valid `CSS` color string.
| **track-color** | #f2f2f2 | The color of the track. You must write a valid `CSS` color string or `false` to disable rendering.
| **scale-color** | #dfe0e0 | The color of the scale lines. You must write a valid `CSS` color string or `false` to disable rendering.
| **scale-length** | 5 | Length of the scale lines (reduces the radius of the chart).
| **line-cap** | butt | Defines how the ending of the bar line looks like. Possible values are: `butt`, `round` and `square`.
| **line-width** | 5 | Width of the chart line in `px`.
| **size** | 200 | Size of the pie chart in `px`. It will always be a square.
| **rotate** | 0 | Rotation of the complete chart in `degrees`.
| **animate** | true | `Boolean` for an animation of the bar growing.
| **animate-duration** | 1000 | Time in `milliseconds` for the animation duration. Only use if `animate === true`
| **display-pie** | true | Display pie chart for compatible browsers. If browsers are not compatible, to display only text, set value to `false`

## Events

All events will only be called if `animate === true`.

| Events                     | Attributes    | Description
|:---------------------------|:-------------:|:------------
| **onStart(from, to)** | **on-start** | Called at the `start` of any animation.
| **onStep(from, to, currentValue)** | **on-step** | Called `during` animations providing the current value.
| **onStop(from, to)** | **on-stop** | Called at the `end` of any animation.

Functions of events must be implemented in the application's controller:

```javascript
app.controller('PieChartController', ['$scope', function($scope)
{
    $scope.onStart = function(from, to)
    {
        console.log(from); // display `from` value
        console.log(to);   // display `to` value
    };

    $scope.onStep = function(from, to, currentValue)
    {
        console.log(from);           // display `from` value
        console.log(to);             // display `to` value
        console.log(currentValue);   // display `current` value
    };

    $scope.onStop = function(from, to)
    {
        console.log(from); // display `from` value
        console.log(to);   // display `to` value
    };
}]);
```

When implementations are done, you can insert attributes in the directive:

```javascript
<div ng-controller="PieChartController">
    <ngpiechart progression="35" total="100" on-start="onStart" on-step="onStep" on-stop="onStop">
        <div>Content to display</div>
    </ngpiechart>
</div>
```

You can only add events that you need.

## Dynamic value

To have a dynamic value in the pie chart, you must bind `progression` and `total` value in your controller:

```javascript
app.controller('PieChartController', ['$scope', function($scope)
{
    $scope.progression = 70;
    $scope.total = 100;
}]);
```

After that, add these attributes in the directive with binding values:

```javascript
<div ng-controller="PieChartController">
    <ngpiechart progression="progression" total="total">
        <div>Content to display</div>
    </ngpiechart>
</div>
```

Now, you can have, for example, an input text to change the value of the pie chart:

```javascript
<div ng-controller="PieChartController">
    <ngpiechart progression="progression" total="total">
        <div>Content to display</div>
    </ngpiechart>
    <input type="text" ng-model="progression" value="{{progression}}" />
</div>
```

Try it, it's magic.

**Note:**

**If `progression` and/or `total` are not defined, default values will be respectively `0` and `100`.**

## Browser support

Native support:

* Chrome
* Safari
* FireFox
* Opera
* Internet Explorer 9+
* Support for Internet Explorer 7 and 8 with [excanvas](https://code.google.com/p/explorercanvas/wiki/Instructions) polyfill.

## License
Copyright (c) 2014 Nicolas Jessel. Licensed under the [MIT license](https://github.com/njl07/angular-piechart/blob/master/LICENSE.md).
