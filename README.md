### reusableBehaviors
###### Angular directives for simple behaviors
***

### Table of Contents
* [Motivation](#motivation)
* [Design Paradigm](#design-paradigm)
* [Usage](#usage)
* [Install](#install)



### <a name="motivation"></a>Motivation
reusableBehaviors is an AngularJS module containing directives which isolate and encapsulate interactive behaviors used throughout front end web development. By isolating the behaviors in their own directives, rb is completely agnostic of design choices made by the developer. These directives simply add a behavior to any element, freeing developers from the styling choices included in more restrictive front end libraries.

### <a name="design-paradigm"></a>Design Paradigm
* Directives are named in the typical angular fashion, beginning with a two-character mnemonic, followed by a single word which is descriptive of the behavior that the directive provides. (e.g. rb-toggle, rb-relay)
* Each directive exposes its API to the DOM using an attribute called [behavior]-api. (e.g. toggle-api, relay-api)
* APIs include both properties and methods, see the [demo page](https://sranderley.github.io) to view the directives along with their markup
* Some of the directives rely on additional attributes for configuration, see the [demo page](https://sranderley.github.io) for more details
* Some directives depend on services, please just go to the [demo page](https://sranderley.github.io) already

### <a name="usage"></a>Usage
These directives are meant for use with the ng-class directive and a strong knowledge of CSS and CSS transitions. They can be used to provide behaviors to standalone elements, or they can be wrapped up inside of other directives with styles already applied, providing behavior to the contents of the container directive.

####Example

This is the source code for the rb-toggle directive.
````javascript
angular
	.module('reusableBehaviors')
	.directive('rbToggle', rbToggle);

function rbToggle(){
	return {
		restrict: 'A',
		scope: {
			toggleApi: '='
		},
		link: function(scope, elem, attr){
			scope.toggleApi = {
				active: false,
				toggle: toggle
			};

			function toggle(){
				scope.toggleApi.active = !scope.toggleApi.active;
			}
		}
	}
}
````
And this is an example of the rb-toggle directive being used in the DOM
````
	<button ng-click="window.toggle()">Click me to open the window!</button>

	<div rb-toggle
		toggle-api="window"
		class="window"
		ng-class="{
			closed: !window.active,
			open: window.active
		}"
	>
		<div>Tons of cool stuff!</div>
	</div>
````

### <a name="install"></a>Install