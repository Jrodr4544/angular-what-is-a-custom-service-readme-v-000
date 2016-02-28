# What is a Service?

## Overview

We've used Angular's built-in services already, but wouldn't it be cool if we could create our own? We can!

## Objectives

- Describe custom Services
- Create a custom Service
- Bind the Service to the module
- Inject the Service into Controller
- Use custom Service

## Custom Services

Angular allows us, much like controllers, to create custom services. These are very powerful and can do a lot for us, such as communicating with APIs or manipulating data. We can inject these into any controller we'd like too, meaning we won't be repeating ourselves.

This fits into our "MVVM" pattern. We can create services (our helpers) to do all the "dirty" work for us (communicate with APIs, etc), and we can then utilise them in our controllers. This keeps our controllers thin and all the business logic inside our services.

## .service()

Our services follow the same setup as our custom controllers. We use `.service` to create them! This is the basic setup of a service:

```js
function SomeService() {
	this.someFunction = function () {

	};
}

angular
	.module('app')
	.service('SomeService', SomeService);
```

Very easy! With services, much like our controllers (when using controllerAs), we attach all of our functions to `this`. These will be publicly accessible by anyone who injects the service. We can also create private functions by using normal functions, as such:

```js
function SomeService() {
	function privateMethod() {

	}

	this.publicMethod = function () {
		privateMethod();
	};
}

angular
	.module('app')
	.service('SomeService', SomeService);
```

## Injecting our services

Much like when we used `$timeout`, we can inject our custom services into our controllers by using their name. To inject our `SomeService` above, we just add `SomeService` as an argument to our controller:

```js
function SomeController(SomeService) {
	SomeService.publicMethod();
}

angular
	.module('app')
	.controller('SomeController', SomeController);
```

Simple!