## Chunk Blocking

This is the most difficult step in Reading-Lodash.

You will analyze the trace-block from step 1 to identify meaningful chunks of code, and understand how those chunks fit together to create a unified strategy.

_Strategy_ is how behaviorally distinct chunks of code are used in combination to achieve a desired behavior.

___

1. Determine which lines of code form behaviorally distinct & meaningful chunks.  If you think a piece of your trace-block might be a chunk, ask yourself (white board is recommended):
    * What variables are used in this chunk?
    * What are their values before the chunk?
    * What are their values after the chunk?
    * How was each variable used before this chunk?
        * is it ... read? modified? used for decision making? contributing to another variable's value? holding an intermediate value?
    * How are they used inside this chunk?
    * How are they used after this chunk?
    * Does this variable profiling indicate that there is a meaningful change in state after this chunk is executed?
2. If the chunk passes your "behaviorally distinct & meaningful" test, turn it into a function and replace it with a function call in the trace-block
    1. Create an empty function in a "closure" object
    2. Give it a behaviorally meaningful name. (this is hard)
    3. Copy paste the chunk in to the function body
    4. Set up a "result" variable and return any values that are modified in, and used after, the chunk
    5. Replace the chunk with a call to the new "closure.function"
    6. Set all necessary variables as parameters and pass them as args in the block
    7. Refactor. Can you reduce the number of variables to 3 or less?

---

[__Before__](https://github.com/elewa-academy/reading-padStart/blob/master/1-padStart-trace-blocked.js)

```js
let padded_string;
{ // padStart(a, b, c)
    let args = {
        string: undefined,
        length: undefined,
        chars: undefined
    };
    let dep = {
        _createPadding: {[...]
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

[__After__](https://github.com/elewa-academy/reading-padStart/blob/master/2-padStart-chunk-blocked.js)

```js

let padded_string;
{ // padStart(a, b, c)
    let args = {[...]
    };
    let dep = {[...]
    }
    let closure = {
        cast_args: function (string, number) {
            let result = {};
            result.string = toString(string);
            result.number = toInteger(number);
            return result;
        },
        find_length: function (string, length) {
            let result;
            if (length) { 
                result = stringSize(string);
            } else {
                result = 0;
            };
            return result;
        },
        pad_check: function (real_len, desire_len) {
            let result;
            const step_1 = real_len < desire_len;
            result = desire_len && step_1;
            return result;
        },
        pad: function (pad_length, string, chars) {
            let result;
            const step_1 = createPadding(pad_length, chars);
            return step_1 + string;
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

___
___
### <a href="http://elewa.education/blog" target="_blank"><img src="https://user-images.githubusercontent.com/18554853/34921062-506450ae-f97d-11e7-875f-6feeb26ad72d.png" width="100" height="40"/></a>
