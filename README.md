### reusableBehaviors
###### Angular directives for simple behaviors
***

### Table of Contents
* [Motivation](#motivation)
* [Behaviors](#behaviors)
* [Design Paradigm](#design-paradigm)
* [Usage](#usage)
* [Install](#install)
* [License](#license)

### <a name="motivation"></a>Motivation
reusableBehaviors is an AngularJS module containing directives which isolate and encapsulate interactive behaviors used throughout front end web development. By isolating each behavior in its own directive, rb is completely agnostic of design choices made by the developer. These directives simply add a behavior to any element, freeing developers from the styling choices included in more restrictive front end libraries.

### <a name="behaviors"></a>Behaviors
* [Toggle](https://sranderley.github.io/#/demos/rb-toggle) - Exactly what you'd expect
* [Relay](https://sranderley.github.io/#/demos/rb-relay) - This is similar to a toggle, but relays are grouped and only one member of each group can be 'active' at a time
*

### <a name="design-paradigm"></a>Design Paradigm
* Directives are named in the typical angular fashion, beginning with a two-character mnemonic, followed by a single word which is descriptive of the behavior that the directive provides. (e.g. rb-toggle, rb-relay)
* Each directive exposes its API to the DOM using an attribute called [behavior]-api. (e.g. toggle-api, relay-api)
* APIs include both properties and methods, see the [demos page](https://sranderley.github.io) to view the directives along with their markup
* Some of the directives rely on additional attributes for configuration, see the [demos page](https://sranderley.github.io) for more details
* Some directives depend on services, please just go to the [demos page](https://sranderley.github.io) already

### <a name="usage"></a>Usage
These directives are meant for use with Angular's native ng-class and ng-show directives, as well as a strong knowledge of CSS and CSS transitions. Each directive can be used to provide behaviors to standalone elements in the DOM, or within templates of other directives, providing behaviors to the elements in the container directive.

####Example

This is the source code for the rb-toggle directive.
````javascript
angular
	.module( 'reusableBehaviors' )
	.directive( 'rbToggle', rbToggle );

function rbToggle () {
	return {
		restrict: 'A',
		scope: {
			toggleApi: '=',
			disabled: '=?'
		},
		link: function( scope, elem, attr ){
			scope.toggleApi = {
				active: false,
				toggle: toggle
			};

			function toggle () {
				scope.toggleApi.active = scope.disabled ? scope.toggleApi.active : !scope.toggleApi.active;
			}
		}
	}
}
````
And this is an example of the rb-toggle directive being used in the DOM
````HTML
<button
	rb-toggle
	toggle-api="window"
	ng-click="window.toggle()">
	Click me to open the window!
</button>

<div
	class="window"
	ng-class="{
		closed: !window.active,
		open: window.active
	}">
	<div>The Great Outdoors</div>
</div>
````
In this example, the directive is instantiated on the button and its API is defined as "window". This API is then used by the `<button>` element, which invokes the directive's toggle method whenever it is clicked. The result of invoking the toggle method is that the boolean `window.active` changes its state.

The following CSS applies a transition whenever `window.toggle` is invoked.
````CSS
.window {
	width: 100%
	background-color: #B4D455
	transition: height 0.1s
}

.window.closed {
	height: 0;
}

.window.open {
	height: 100%
}
````
The rest of the directives follow a very similar usage pattern. They expose an API to the current scope of the DOM, which is used to access the behaviors that the directive provides. Check out the [demos page](https://sranderley.github.io) to see working examples along with the code that links everything together.

### <a name="install"></a>Install
Installation is very simple.
* Include rb.js or rb.min.js file in your project directory
* Inside of your index.html, include a `<script>` tag which points to rb.js or rb.min.js
* In the declaration of your angular app, pass 'reusableBehaviors' as a dependency, like:
````javascript
angular.module('myApp', [ 'reusableBehaviors' ]);
````

### <a name="license"></a>License
MIT License can be viewed [here](/LICENSE)