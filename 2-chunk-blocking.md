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



___
___
### <a href="http://elewa.education/blog" target="_blank"><img src="https://user-images.githubusercontent.com/18554853/34921062-506450ae-f97d-11e7-875f-6feeb26ad72d.png" width="100" height="40"/></a>
