# React-datalist

[![testling badge](https://ci.testling.com/asbjornenge/react-datalist.png)](https://ci.testling.com/asbjornenge/react-datalist)

React-datalist is an attempt at making a [<code>\<datalist></code>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/datalist) polyfill as a reusable [react](http://facebook.github.io/react/) module.  

Feedback in the form of [issues](https://github.com/asbjornenge/react-datalist/issues) and [pull-requests](https://github.com/asbjornenge/react-datalist/pulls) is very much appreciated!

Check out the [**DEMO**](http://www.asbjornenge.com/react-datalist/)

## Install

	npm install react-datalist

## Use

	var React = require('react')
	var ReactDatalist = require('react-datalist')

	var options = ['apple','orange','pear','pineapple','melon']
	React.renderComponent(ReactDatalist({list:'fruit', options:options}), document.body)

## Props

	list            * - <datalist id="list"> and <input list="list">
	options         * - the available options
	placeholder       - a placeholder for the input field
	forcePoly         - always use the polyfill                   (default false)
	blurTimeout       - timeout after blur before hinding opts    (default 200ms)
	autoPosition      - automatically position the options list   (default true)
	initialFilter     - set the initial input value               (default '')
	hideOptionsOnEsc  - hide options on esc                       (default true)
	hideOptionsOnBlur - hide options on input blur                (default true)
	onOptionSelected  - callback triggered when option is considered selected
	getController     - pass a function to collect a controller object (see below)

	* = required

### getController

The getController property is there to enable external control of the component's inner state - while keeping the state in sync. It takes a function that will return a controller object.

    getController : function(controller) { /* ... */ }

The controller offers the following

	controller.setFilter(string, callback)  - sets the value of the input
	controller.toggleOptions(callback)      - toggle show/hide of options. shown bool passed to callback.
	controller.getState()                   - gets the current inner state
	controller.setState(newState, callback) - set a new inner state

## !TLDR;

React-datalist includes both a ***input*** and a ***datalist*** element. In order to stay fairly simple to use, align with react and avoid native events and other trickery, this was necessary. The structure is as follows:

	// Native

	<div class="react-datalist-container">
		<input class="react-datalist-input">
		<datalist class="react-datalist">
			<option value="values">
		</datalist>
	</div>

	// Polyfill

	<div class="react-datalist-container">
		<input class="react-datalist-input">
		<div class="react-datalist">
			<div class="react-datalist-option">values</div>
		</div>
	</div>

If you need to interact with the input element, attach listeners like **onInputChange**, **onInputBlur**, etc. (Note to self: expose additional input events. Note to others: encourage by creating issues)

#### Styling

There is also some (quite useful) styling you can/should use. You can find it under *node_modules/react-datalist/react-datalist.styl*. If you don't use stylus it's pretty small and easy to copy. I might include it if I pack up a UMD module for React-datalist. Anyone want that? Create an issue :-)

(Note to self: Convert styling to plain css)  
(Idea: Should I pack a commonjs module that include the styling?)

#### JSX

The module itself does not make us of **JSX** as not to impose restrictions on the user.

#### Features

For a full feature list check out the [spec](https://github.com/asbjornenge/react-datalist/blob/master/test/spec.js).

## Changelog

### 1.2.0

* Added *hideOptionsOnEsc* for the ability to opt out of hiding options when user hits esc
* Added *controller.getState* for a sneak peak at the inner state
* Added *controller.setState* for improved external control

### 1.1.0

* Bumped the blurTimeout up to 200ms (people were having issues)
* Added the ability to specify *blurTimeout* via props
* Added *hideOptionsOnBlur* for the ability to opt out of hide-options-on-blur

### 1.0.0

* Removed setFilter support
* Added a more generic getController prop that returns an object with functions for external control
* Added setFilter to controller
* Added toggleOptions to controller

### 0.2.0

* Added support for externally controlling the filter state via the ***setFilter*** property.

### 0.1.2

* Minor improvement to help testing (test are too fast for my timeouts :-P)

### 0.1.1

* Increased hide-options timeout on blur (more time to make click register)
* Supporting placeholder property for input

### 0.1.0

* Added support for passing initial input value via the ***initialFilter*** property.

### 0.0.1

* Initial release! YaY :-D

enjoy.
