### "Why Angular?" in Terms of Directives
HTML is great for declaring static documents, but it falters when we try to use it for declaring dynamic views in web applications. AngularJS lets you extend HTML vocabulary for your application. The resulting environment is extraordinarily expressive, readable and quick to develop.

##### Typical Angular HTML
```
<ol>
    <list-item ng-repeat="item in list.items"></list-item>
</ol>
```
### Directive
Marker on a DOM elemet that tells Angular's HTML compiler to attach a specified behavior to that DOM element.
* The compiler can even transform / change the DOM elements and its children.
* A marker can be attribute, element name, comment or CSS class.

### Steps to Create Directive
#### Step 1: Register Directive
```
angular.module('app', [])
.controller('MyCtrl', MyCtrl)
.directive('myTag', MyTag);
```
`'myTag'` - normallized name that will appear in HTML
`MyTag` - Factory function, that returns DDO (Directive Definition Object)

#### Step 2: Define Factory Function
```
MyTag.$inject = [...];
function MyTag(...){
    var ddo = {
        template: 'Hello World!'
    };

    return ddo;
}
```
`MyTag.$inject = [...];` - inject other sercices, controller, etc. as usual

#### Step 3: Use In HTML
`<my-tag></my-tag>` - note that the name is __not__ myTag, but my-tag

***
#### _Summary_
* Directive is a marker in HTML that Angular complies into some behavior.
    * It can also change the HTML elements themselves.
* Register name of directive using (normallized) camelCase.
* Registered factory function must return a DDO.
    * The factory function gets invoked only once.
* With custom directives, our HTML coding becomes
    * reusable;
    * semantically relevant to the actual web app we're building. 
***

### Restricting Directive To Element or Attribute
```
function MyDirective(){
    var ddo = {
        restrict: 'AE',
        ...
    };
    return ddo;
} 
```
`restrict: 'AE'` - Default: 'A' - attribute, 'E' - element

`restrict: 'A'` - Best Practice: restrict to attribute if directive is extending behavior, e.g., `ng-repeat` 

`restrict: 'E'` - Best Practice: restrict to element if directive is defining a component with an associated template, e.g., `<list-item>`
***
#### _Summary_
* The DDO's restrict property determines what AngularJS compiler should look for to detect your custom directive.
* Using directive as a different restrict type than defined will cause the compiler to simply ignore it.
* Best Practice: use 'E' for element when directive has content along with possible behavior.
* Best Practice: use 'A' for attribute when directive has no content and only extends the behavior of host element.
* Class and comment directives are possible, but not used.
***
