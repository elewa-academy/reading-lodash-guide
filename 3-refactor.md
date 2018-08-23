## Refactor

De-trace-block your step 2, turn your chunk-block into a working JS file.  You will know you have successfully completed this step when ./3-___-refactor.js passes all of your original test cases.

_Refactoring_ is modifying your source code without changing it's behavior. 

___


* Replace your "dep" object with require statements
* Remove your chunk functions from their "closure" object and place them at the bottom of your file.
* Write test cases for you chunk functions and put them along-side
* De-trace-block the main function & export it (above the chunk functions)
* Copy paste the docs from the original file
* Test it using your original test cases.  If everything is green, win.  Else, go back and fix.

---


[__Before__](https://github.com/elewa-academy/reading-padStart/blob/master/2-padStart-chunk-blocked.js)

```js

let padded_string;
{ // padStart(a, b, c)
    let args = {[...]
    };
    let dep = {[...]
    }
    let closure = {
        cast_args: function (string, number) {[...]
        },
        find_length: function (string, length) {[...]
        },
        pad_check: function (real_len, desire_len) {[...]
        },
        pad: function (pad_length, string, chars) {[...]
        } 
    }

    let ret_val;
    padStart: {
        let safe_args = closure.cast_args(args.string, args.length);
        string = safe_args.string;
        length = safe_args.number;

        var strLength = closure.find_length(args.string, args.length); 

        let needs_padding = closure.pad_check(strLength, args.length);

        if (needs_padding) {
            let pad_length = args.length - strLength;
            ret_val = pad(pad_length, args.string, args.chars);
        } else { 
            ret_val = args.string;
        };

        break padStart;
    };

} 

```

[__After__](https://github.com/elewa-academy/reading-padStart/blob/master/3-padStart-refactor.js)

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




___
___
### <a href="http://elewa.education/blog" target="_blank"><img src="https://user-images.githubusercontent.com/18554853/34921062-506450ae-f97d-11e7-875f-6feeb26ad72d.png" width="100" height="40"/></a>
