# dom-delegator

<!--
    [![build status][1]][2]
    [![NPM version][3]][4]
    [![Coverage Status][5]][6]
    [![gemnasium Dependency Status][7]][8]
    [![Davis Dependency status][9]][10]
-->

<!-- [![browser support][11]][12] -->

Decorate elements with delegated events

`dom-delegator` allows you to attach an `EventHandler` to 
  a dom element.

When event of the correct type occurs `dom-delegator` will
  invoke your `EventHandler`

This allows you to seperate your event listeners from your
  event writers. Sprinkle your event writers in the template
  in one part of your codebase. Attach listeners to the event
  sources in some other part of the code base.

This decouples the event definition in the DOM from your event
  listeners in your application code.

Also see [`html-delegator`](https://github.com/Raynos/html-delegator)
  for the same idea using html `data-` attributes.

## Example

```js
var document = require("global/document")
var Delegator = require("dom-delegator")
var h = require("hyperscript")
var addEvent = require("dom-delegator/add-event")
var EventSinks = require("event-sinks/geval")

var delegator = Delegator(document.body)
var events = EventSinks(delegator.id, ["textClicked"])
var sinks = events.sinks
var elem = h("div.foo", [
    h("div.bar", "bar"),
    h("span.baz", "baz")
])
var bar = elem.querySelector(".bar")
var baz = elem.querySelector(".baz")
document.body.appendChild(elem)


// add individual elems. (in a different file?)
addEvent(bar, "click", sinks.textClicked, {
  type: "bar"
})
addEvent(baz, "click", sinks.textClicked, {
  type: "baz"
})

// add a listener, (in a different file?)
events.textClicked(function (tuple) {
    var value = tuple.value

    console.log("doSomething", value.type)
})
```

## Installation

`npm install dom-delegator`

## Contributors

 - Raynos

## MIT Licenced

  [1]: https://secure.travis-ci.org/Raynos/dom-delegator.png
  [2]: https://travis-ci.org/Raynos/dom-delegator
  [3]: https://badge.fury.io/js/dom-delegator.png
  [4]: https://badge.fury.io/js/dom-delegator
  [5]: https://coveralls.io/repos/Raynos/dom-delegator/badge.png
  [6]: https://coveralls.io/r/Raynos/dom-delegator
  [7]: https://gemnasium.com/Raynos/dom-delegator.png
  [8]: https://gemnasium.com/Raynos/dom-delegator
  [9]: https://david-dm.org/Raynos/dom-delegator.png
  [10]: https://david-dm.org/Raynos/dom-delegator
  [11]: https://ci.testling.com/Raynos/dom-delegator.png
  [12]: https://ci.testling.com/Raynos/dom-delegator
