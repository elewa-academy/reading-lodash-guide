## Trace Blocking

The objective of this step is to inspect how Lodash implements their behavior.  You will expand your function into a trace-block illustrating where each variable derives it's value, and how those variables are used step-by-step detail.

_Implementation_ is the exact steps used to implement a behavior.

___

1. Trace-block your function in ./1-___-trace-blocked.js
    * Indicate where each variable derives it's value
    * Include the specs for each dependency
    * Expand any expression taking 3 or more values into it's own trace-block
2. Fill out the Part-Task section of the README.  Put any part-task exercises you made in the ./exercises folder, they can be designed for the browser or Node

---

[__Before__](https://github.com/elewa-academy/reading-padStart/blob/master/0-padStart.js)

```js
var createPadding = require('./node_modules/lodash/_createPadding'),
    stringSize = require('./node_modules/lodash/_stringSize'),
    toInteger = require('./node_modules/lodash/toInteger'),
    toString = require('./node_modules/lodash/toString');

/**[...]

function padStart(string, length, chars) {
  string = toString(string);
  length = toInteger(length);

  var strLength = length ? stringSize(string) : 0;
  return (length && strLength < length)
    ? (createPadding(length - strLength, chars) + string)
    : string;
}

module.exports = padStart;
```
[__After__](https://github.com/elewa-academy/reading-padStart/blob/master/1-padStart-trace-blocked.js)

```js
let padded_string;
{ // padStart(a, b, c)
	let args = {
		string: undefined,
		length: undefined,
		chars: undefined
	};
	let dep = {
		_createPadding: {
			args: {
				number: "The padding length"
				string: "The string used as padding"
			},
			returns: {
				string: "the padding for `string`"
			} 
			behavior: "Creates the padding for `string` based on `length`. The `chars` string is truncated if the number of characters exceeds `length`."
		},
		_stringSize: {[...]
		},
		toInteger: {[...]
		},
		toString: {[...]
		}
	}

	let ret_val;
	padStart: {
		args.string = dep.toString(args.string);
		args.length = dep.toInteger(args.length);

		var strLength; 
		if (args.length) { 
			strLength = dep.stringSize(args.string);
		} else {
			strLength = 0;
		};

		let condition;
		{
			const step_1 = strLength < args.length;
			const step_2 = args.length && step_1;
			condition = step_2;
		};

		if (condition) {
			const step_1 = args.length - strLength;
			const step_2 = dep.createPadding(step_1, args.chars);
			ret_val = step_2 + args.string;
		} else { 
			ret_val = args.string;
		};

		break padStart;
	};

} 
```





___
___
### <a href="http://elewa.education/blog" target="_blank"><img src="https://user-images.githubusercontent.com/18554853/34921062-506450ae-f97d-11e7-875f-6feeb26ad72d.png" width="100" height="40"/></a>
