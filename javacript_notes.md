# Modern Javascript Tutorial Notes
## URL: [https://javascript.info](https://javascript.info)

## Tags
    <script></script>
    <script src="./myscript.js"></script>

If a the script tag have a src attribute, the content will be ignored.

## The modern mode, "use strict"

    "use strict";
    //this code works the modern way.

When ECMAScript 5 (ES5) appeared, It added new features to the language and modified some of the existing ones.  
To keep the old code working, most modifications are off by default. One need to enable then explicitly "use strict";  
When located at the top, the whole script works the modern way.  
Make sure that "use strict" is on the top of the script, otherwise the strict mode may not be enabled.  

## Variables
Declaration:

    let message; //single
    let user = 'John', age = 25, message = 'hello'; //multiple

Variables Naming:
1. Must contain only letters, digits, symbols $ and _
2. First character must not be digit.
3. When the name contains multiple words, camelCase is commonly used.
4. Is case-sensitive.

### Assignments with "use strict"
If modern javascript is used, (declared "user strict" at the top of the script),
variables must be declared before use.  
On old javacript is possible to use a variable without declaring.

    num = 5
    alert(num)

### Constants
    const name = "myname";

To declare a constant use const instead let.

## Data Types

### String
A string in JavaScript must be quoted.
The "+" concatenate string.

    let str = "Hello";
    let str2 = 'Single quotes are ok too';
    let phrase = `can embed ${str}`;

Double and single quotes are "simple quotes". There's no difference.
Backticks are "extended functionality" quotes. They allow emded variables and expressions into  
string by wrapping them in ${...}.

### typeof Operator
The typeof or typeof(x) operator returns the type of the argument.

    typeof true // "boolean"
    typeof "foo" // "string"

## Type conversions

### ToString
    let strVal = String(1+2);

### ToNumber
    let numVal = Number('12'); 

### ToBoolean
    let boolVal = Boolean(value);

* Values taht are intuitively "empty", like 0, empty string "", null, undefined and NaN becomes false.
* Other values become true.

## Interaction: alert, prompt, confirm

### alert
    alert("message");

### prompt(title[, default])
    let age = prompt('How old are you?', 100);

* Always supply a default, if not, in IE, the value will be set to undefined on the inputbox.

## confirm()
    let boolValue = confirm('question');

## Ternary Operator ?
    let result = condition ? value1 : value2;

## Switch statement

    switch(a){
        case 3 : 
            alert('3');
            break;

        case 4 : 
            alert('3');
            break;
          
        default : 
            alert('default');
    }

## Functions

### Default paramenter value
    function sayHello(from, text = 'no text given'){
        ...
    }

### Old style
    function sayHello(from, text){
        if(text === undefined){
            text = 'no text given';
        }
    }

### Naming
It's a widespread practice to start a function with a verbal prefix which vaguely describes the action
* get... - return a value,
* calc... - calculate something
* create... - create something
* check... - check something and resturn a boolean
* show... - show something

## Function Expression

### Assign to a variable
    let sayHi = function(){
        alert("Hello");
    }

    alert(sayHi); // Shows the value of the sayHi variable

    alert(sayHi()); //Executes function()

    sayHi(); //executes function

## Callback functions

    function ask(question, yes, no){
        if (confirm(question)) yes()
        else no();
    }

    function showOk(){
        alert("agree");
    }

    function showCancel(){
        alert("cancel");
    }

    //usage functions showOK, showCancel are passed as argument to ask
    ask("do you agree?", showOk, ShowCancel);

    //--------Shorter Way---------//
    ask(
        "Do you agree?",
        function(){ alert("agree"); },
        function(){ alert("cancel"); },
    )

## Arrow functions
    let func = (arg1, arg2, ..., argN) => expression

    let sum = (a, b) => a + b;
    /* The arrow function is a shorter form of:
        let sum = function(a, b){
            return a + b;
        }
    */

    alert (sum (1, 2));

This creates a function func that has arguments arg1 ... argN, avaluates the expression on theright side with their use and return its result.

## Automated testing with mocha

### Behavior Driven Development (BDD)

    describe("pow", function(){
        it("raises to n-th power", function(){
            assert.equal(pow(2,3), 8);
        });
    });

A spec has three main building blocks, taht you can see above:

* describe("title", function() {...})  
    What functionality we're describing.
* it("title", function() {...})  
    In the title of __it__ we in a human-redable way describe the particular use case,  
    and the second argument is a function that tests it.
* assert.equal(value1, value2)
    The code inside __it__ block, if the implementation is correct, should execute without errors.  
    Functions assert.* are used to check whether pow works as expected.

### The development flow
The flow of development usually looks like this:
1. An initial spec is written, with thests for the most basic functionality.
2. An initial implementation is created.
3. To check whether it works, we run the testing framwork [Mocha](https://mochajs.org/) taht runs the spec.  
    Errors are displayed. We make corrections until everything works.
4. Now we have a working initial implementation with tests.
5. We add more use cases to the spec, probably not yet supported by the implementations. Test start to fail.
6. Goto 3, update the implementaition till tests give no errors.
7. Repeat steps 4-6 till the functionality is ready.

So, the development is interative. We write the spec, implement it, make sure tests pass, then write more tests,  
make sure they work etc.

### Test Libraries

* [Mocha](https://mochajs.org/)
* [Chai](http://www.chaijs.com/)
* [Sinon](http://sinonjs.org/)

## Polyfills

### Babel
When we use modern features of the language, some engines may fail to support such code. Just as said,  
not all features are implemented everywhere.
[Babel](https://babeljs.io/) is a transpiler. It rewrites modern JavaScript code into the previous standard.

* First the developer runs the traspiller in his own computer. It rewrites the code into the older standard.  
    And then the code is delivered to the website for users. Modern project build system like [webpack](http://webpack.github.io/)  
    or [brunch](http://brunch.io/) that provide means to run transpiler automatically on every code change.

## Objects

### Creation
    let user = new Object();
    let user = {};

    let user = {
        propKey : 'propValue',
        propKey2 : 'value2'
    }

    //usage
    alert(user.propKey);

### Remove a property
    delete user.age;

### Multiword property name
    let user = {
        name : "John",
        age : 30,
        "likes birds" : true
    };

    
### Square brackets
To access multiword key:

    alert(user["likes birds"]);

Square brackets also provide a way to obtain the property name as the result of any expression  
as opposed to a literal string.

    // Example 1
    let key = "likes birds";
    user[key] = true;

    // Example 2
    let fruit = prompt("Which fruit to buy?", "apple");
    let bag = {
        [fruit] : 5;
    }

    alert( bag.apple );

### Property value shorthand
    function makeUser(name, age){
        return {
            name, //same as name : name
            age //same as age : age
        }
    }

### Existence check
    "key" in object
    alert( "age" in user ); //true if age exists in user

### for..in loop
To walk over all keys of an object.

    for(key in object){
        //executes the body for each key among object properties
    }

## Object methods, "this"

### Method shorthand
    let user = {
        name: "john",
        age: 35,
        sayhi(){
            alert("hello");
        }

        // is the same as
        sayhi : function(){
            ...
        }
    }