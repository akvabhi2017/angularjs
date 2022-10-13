```
Module:
Create a module named myModule1 that depends on
myModule2 and myModule2:
angular.module(“myModule1”,[“myModule2”,
“myModule2”])
Get reference to the module myModule1
angular.module(“myModule1”)

Defining a Controller and using it:
i. With $scope:
angular.module(“myModule”).
controller(“SampleController”,
function($scope,){
 //Members to be used in view for binding
 $scope.city=”Hyderabad”;
});
In the view:
<div ng-controller=”SampleController”>
 <!-- Template of the view with binding
 expressions using members of $scope -->
 <div>{{city}}</div>
</div>
ii. Controller as syntax:
angular.module(“myModule”).
controller(“SampleController”, function(){
 var controllerObj = this;
 //Members to be used on view for binding
 controllerObj.city=”Hyderabad”;
});
In the view:
<div ng-controller=”SampleController as ctrl”>
 <div>{{ctrl.city}}</div>
</div>

Defining a Service:
angular.module(“myModule”).
service(“sampleService”, function(){
 var svc = this;
 var cities=[“New Delhi”, “Mumbai”,
 “Kolkata”, “Chennai”];
 svc.addCity = function(city){
 cities.push(city);
 };
 svc.getCities = function(){
 return cities;
 }
});
The members added to instance of the service are visible to the
outside world. Others are private to the service. Services are
singletons, i.e. only one instance of the service is created in the
lifetime of an AngularJS application.

Factory:
angular.module(“myModule”).
factory(“sampleFactory”, function(){
 var cities = [“New Delhi”, “Mumbai”,
 “Kolkata”, “Chennai”];
 function addCity(city){cities.push(city);}
 function getCities(){return cities;}
 return{
 getCities: getCities,
 addCity:addCity
 };
});
A factory is a function that returns an object. The members
that are not added to the returning object, remain private
to the factory. The factory function is executed once and the
result is stored. Whenever an application asks for a factory, the
application returns the same object. This behavior makes the
factory a singleton.

Value:
angular.module(“myModule”).value(“sampleValue”, {
 cities : [“New Delhi”, “Mumbai”, “Kolkata”,
 “Chennai”],
 addCity: function(city){cities.push(city);},
 getCities: function(){return cities;}
});
A value is a simple JavaScript object. It is created just once, so
value is also a singleton. Values can’t contain private members.
All members of a value are public.

Constant:
angular.module(“myModule”).
constant(“sampleConstant”,{pi: Math.PI});
A constant is also like a value. The difference is, a constant can
be injected into config blocks, but a value cannot be injected.

Provider:
angular.module(“myModule”).
provider(“samplePrd”, function(){
 this.initCities = function(){
 console.log(“Initializing Cities…”);
 };
 this.$get = function(){
 var cities = [“New Delhi”, “Mumbai”,
 “Kolkata”, “Chennai”];
 function addCity(city){
 cities.push(city);
 }
 function getCities(){return cities;}
 return{ getCities: getCities,addCity:addCity
 };
 }
});
A provider is a low level recipe. The $get() method of the
provider is registered as a factory. Providers are available
to config blocks and other providers. Once application
configuration phase is completed, access to providers is
prevented.
After the configuration phase, the $get() method of the
providers are executed and they are available as factories.
Services, Factories and values are wrapped inside provider with
$get() method returning the actual logic implemented inside
the provider.

Run block:
angular.module(“myModule”).run(function(<any
services, factories>){
 console.log(“Application is configured. Now inside run
 block”);
});
Run block is used to initialize certain values for further
use, register global events and anything that needs to run at
the beginning of the application. Run block is executed after
config block, and it gets access to services, values and factories.
Run block is executed only once in the lifetime of an Angular
application.

Filters:
angular.module(“myModule”).
filter(“dollarToRupeee”, function(){
 return function(val){
 return “Rs. “ + val * 60;
 };
});
Usage:
<span>{{price | dollarToRupee}}</span>
Filters are used to extend the behavior of binding expressions
and directives. In general, they are used to format values or to
apply certain conditions. They are executed whenever the value
bound in the binding expression is updated.

```
