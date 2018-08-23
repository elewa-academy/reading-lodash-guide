## Tracify Your Refactor

Introduce a non-breaking change to your function's specs that allows a developer to trace the behavior, chunk by chunk.  This will help with debugging, and allow them to understand the implementation without having to do a complete analysis of the source.

Different from the Trace-Log in Expansions, your tracified Lodash function will have no Strings and the trace will be embedded directly into the main function's execution.  It is also tracing  

_Non-Breaking API Changes_ are changes made to the arguments or return value of a function that would not force you to re-write code that used the old version.

In this case, we are adding an extra boolean argument called "trace". If this argument is passed, the function will behave differently.  If not, it behaves exactly as it did before this refactor.

___

* Add a "trace" parameter to your function
* Under each step in your solution, add an if statement to build the trace that records what changed
    * {chunk_function: return_value}
    * See the completed demo for an example to study
* Update the docs in the comments of 4-___-tracible.js
* Run it through your original tests. If it passes, Win.

---

[__Before__](https://github.com/elewa-academy/reading-padStart/blob/master/3-padStart-refactor.js)

```js
var createPadding = require('./node_modules/lodash/_createPadding'),
    stringSize = require('./node_modules/lodash/_stringSize'),
    toInteger = require('./node_modules/lodash/toInteger'),
    toString = require('./node_modules/lodash/toString');


/**[...]**/

function padStart(string, length, char) {
	let safe_args = cast_args(string, length);
	string = safe_args.string;
	length = safe_args.number;

	var strLength = find_length(string, length); 

	let needs_padding = pad_check(strLength, length);

	let result;

	if (needs_padding) {
		let pad_length = length - strLength;
		result = pad(pad_length, string, char);
	} else { 
		result = string;
	};

	return result;
};


module.exports = padStart;


function cast_args(string, number) {[...]
};
let cast_args_test_cases = [
	{input: [0, "e"], expected: {string: "0", number: NaN}, message: "[0, 'e'] -> {string: '0', number: NaN}"}
];

function find_length(string, desire_len) {[...]
};
let find_length_test_cases = [
	{input: ["ee", 3], expected: 2, message: "['ee', 3] -> 2"},
	{input: ["ee", NaN], expected: 0, message: "['ee', NaN] -> 0"}
];

function pad_check(real_len, desire_len) {[...]
};
let pad_check_test_cases = [
	{input: [0, 4], expected: 4, message: "[0, 4] -> 4"}
];

function pad(pad_length, string, chars) {[...]
};
let pad_test_cases = [
	{input: [4, "rolf", "+="], expected: "+=+=rolf", message: "[4, 'rolf', '+='] -> '+=+=rolf'"}
];
```

[__After__](https://github.com/elewa-academy/reading-padStart/blob/master/4-padStart-tracible.js)
```js
var createPadding = require('./node_modules/lodash/_createPadding'),
    stringSize = require('./node_modules/lodash/_stringSize'),
    toInteger = require('./node_modules/lodash/toInteger'),
    toString = require('./node_modules/lodash/toString');


/**[...]**/

function padStart(string, length, char, trace) {
	let result;
	if (trace) {
		result = {}
		result.args = {
			string,
			length,
			char
		}
	};

	let safe_args = cast_args(string, length);
	string = safe_args.string;
	length = safe_args.number;

	if (trace) {
		result.cast_args = safe_args;
	};

	var strLength = find_length(string, length); 

	if (trace) {
		result.find_length = strLength;
	};

	let needs_padding = pad_check(strLength, length);

	if (trace) {
		result.pad_check = needs_padding;
	};

	let final_string;
	if (needs_padding) {
		let pad_length = length - strLength;
		final_string = pad(pad_length, string, char);
	} else { 
		final_string = string;
	};

	if (trace) {
		result.result = final_string;
	} else {
		result = final_string;
	};

	return result;
};

console.log(padStart('abc', 6, " "));
console.log(padStart('abc', 6, " ", true));

module.exports = padStart;


function cast_args(string, number) {[...]
};
let cast_args_test_cases = [[...]
];

function find_length(string, desire_len) {[...]
};
let find_length_test_cases = [[...]
];

function pad_check(real_len, desire_len) {[...]
};
let pad_check_test_cases = [[...]
];

function pad(pad_length, string, chars) {[...]
};
let pad_test_cases = [[...]
];



```




___
___
### <a href="http://elewa.education/blog" target="_blank"><img src="https://user-images.githubusercontent.com/18554853/34921062-506450ae-f97d-11e7-875f-6feeb26ad72d.png" width="100" height="40"/></a>
