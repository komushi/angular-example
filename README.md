# `angular-example` — based on the seed for AngularJS apps

[Original Angular Seed](https://github.com/angular/angular-seed.git)

### Prerequisites
* Node.js and its package manager (npm) installed.

## 1. Clone `angular-example`

Clone the `angular-example` repository using git:

```
git clone https://github.com/komushi/angular-example.git
cd angular-example
```

## 2. Install Dependencies

We have two kinds of dependencies in this project: tools and Angular framework code. The tools help
us manage and test the application.

* We get the tools we depend upon via `npm`, the [Node package manager][npm].
* We get the Angular code via `bower`, a [client-side code package manager][bower].

```
$ npm install
```

### Directory Layout

```
app/                    --> all of the source files for the application
  app.css               --> default stylesheet
  bower_components/     --> all vendor specific modules
  components/           --> all app specific modules
    version/              --> version related components
      version.js                 --> version module declaration and basic "version" value service
      version_test.js            --> "version" value service tests
      version-directive.js       --> custom directive that returns the current app version
      version-directive_test.js  --> version directive tests
      interpolate-filter.js      --> custom interpolation filter
      interpolate-filter_test.js --> interpolate filter tests
  view1/                --> the view1 view template and logic
    view1.html            --> the partial template
    view1.js              --> the controller logic
    view1_test.js         --> tests of the controller
  view2/                --> the view2 view template and logic
    view2.html            --> the partial template
    view2.js              --> the controller logic
    view2_test.js         --> tests of the controller
  app.js                --> main application module
  index.html            --> app layout file (the main html template file of the app)
```

## 3. Run the Application Locally

We have preconfigured the project with a simple development web server. The simplest way to start
this server is:

```
$ npm start
```

Now browse to the app at [`localhost:8000`][local-app-url].

## 4. Run the Application on S3

## 4-1. Upload ./app to your S3 bucket

```
$ aws s3 sync ./app s3://<bucket-name>/
```

## 4-2. Add Bucket Policy
```
{
  "Version":"2012-10-17",
  "Statement":[{
  "Sid":"PublicReadForGetBucketObjects",
        "Effect":"Allow",
    "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::<bucket-name>/*"
      ]
    }
  ]
}
```

## 4-3. Test your website
```
http://<bucket-name>.s3-website-<region>.amazonaws.com
```


For more information on Setting Up a Static Website please check out [s3-static-website][s3-static-website].

# Use $routeProvider to switch between different views
```
angular.module('myApp', [
  'ngRoute',
  ...
]).
config(['$locationProvider', '$routeProvider', function($locationProvider, $routeProvider) {
  $routeProvider
    .when("/", {redirectTo: '/view1'})
    .when("/view1", {templateUrl: "view1/view1.html", controller: "View1Ctrl"})
    .when("/view2", {templateUrl: "view2/view2.html", controller: "View2Ctrl"})
    .otherwise({redirectTo: '/view1'});
}]);
```

For more information on Angular Routing please check out [angular-routing][angular-routing].

[angularjs]: https://angularjs.org/
[bower]: http://bower.io/
[node]: https://nodejs.org/
[npm]: https://www.npmjs.org/
[s3-static-website]: https://docs.aws.amazon.com/AmazonS3/latest/dev/HostingWebsiteOnS3Setup.html
[angular-routing]: https://www.w3schools.com/angular/angular_routing.asp
