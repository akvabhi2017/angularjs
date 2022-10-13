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
