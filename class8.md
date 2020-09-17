### Loop the Loop 150-151, 157 for and while loops; 170-173 and 176

### New vocabulary 
* loop 
* while 
* for 
* codition 
* increment
* decrement

### Comparison Operators: Evaluating conditions 
*  **== is equal to** this operator compares two values (numbers or strings, or Booleans) to see if they're the same; 'Hello' == 'Goodbye' returns false 
* **!= is not equal to** compares two values to see if they're not the same; 'hello' != 'goodbye' returns true 
* **=== strict equal to** compares two values to check that both data type and vlaue are the same 
* **!== strict not eqaul to** compare two values to check that both data type and value are not the same
* > greater than: 4 > 3 returns true
* < less than: 4 < 3 returns false 
* >= greater than or equal to: 4 <= 3 returns true
* <= less than or equal to: 4 <= 3 returns false
* && logical and- this operation test more than one condition: (2 < 5) && (3 >= 2) returns true
* || logical Or- test at least one condition: (2 < 5) || (2 < 1) returns true
* ! logical Not- take a single Boolean value and inverts it !(2 < 1) returns true
* Short-circuit evalutoin- logical expressions are evaluated left to right. If the first condition can provide enough information to get the answer, then there is no need to evaluate the second condition 
* false && anything - it has found a false  

### Loops 
* Loops check a condition. If it returns true, a code block will run. Then the condition will be checked again and if it still returns true, the code block will run again. It repeats until the condition returns false.. there are 3 common types of loops: 
* For - if you need to run code a specific number of times (most common loop) used the for loop. 
* While - if you do not know how many times teh codes should be run, you can use a while loop. 
* Do while - very similar to while loop, but has one key difference: it will always run the statements inside the curly braces at least once, even if the condition evaluates to false


### Loop Counters 
* a for loop uses a counter as a condition. This instructs the code to run a specific number of thimes.
* Initialization - create a variable and set it to 0. This variable is commonly called i, and act as the counter: var i (index)= 0; 
* Condition - the loop should conitnue to run until the counter reaches a specific number: i < 10; 
* Update - every time the loop has run teh statements in the curly braces, it adds on to the counter; i++
* Looping - The first time the loop is run, the variable i (the counter) is assigned to a value of zero.
Every time the loop is run, the condition is check. Is the variable i still less than 10? Then the code inside the loop (the statements between the curly brackets) is run. 
* for (var i = 0; i < 10; i++) {
    document.write(i);
}

* The variable i can be used inside the loop. Here it is used to write a number to the page. When the statments have finished, the variable i is incremented by 1. When the conditoin is no longer true, the loop ends. The script moves to the next line of code. 
        * is 8 < 10? add 1 to 8 and write to page: 8,  