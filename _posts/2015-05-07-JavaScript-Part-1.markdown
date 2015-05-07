---
layout: post
title:  "Beginning JavaScript, Part 1"
date:   2015-05-07 21:02:03
categories: Posts 2
---
This is part 1, my overview of JavaScript. I will not be digging to deeply on the features I cover, I will do this with subsequent posts later, this way I can dedicate posts to higher level concepts of JS. Let's begin.

Javascript is a dynamically typed language, this generally means it does not require pre-compiling before running, the browser does this for us (woohoo). The language has been in existence for 20 years, and runs in all modern browsers. JavaScript was created by Brendan Eich at Netscape in 1995. Although it was only since around the year 2000, has it been taken seriously by most developers, this could be down to it's dominance in the browser now being seen as the standard language of the web, or the fact that people are finally realizing it is a good language for it's purpose and being made better with each new year (I can't have much say as I have only been programming for about 1.5 years now). Not only does JS run in the browser, it has made it's way over to the server with the help of NodeJS.

To begin using JavaScript all you really need is a simple text editor and a browser. If your reading about JavaScript I will assume you have knowledge of writing HTML & CSS, I hope you do. Save one file as main.js, and another file as index.html. Above the last body tag of the index.html inside script tags, reference your main.js file with the src attribute.

There are many other parts of a html page, but this is enough to get you going. There are also more performant ways to inject JavaScript to the page, but this is more advanced and for another time.
Start writing code, save and your away. Another easier and awesome way to write JS and how we debug our code is through the JS console. I always use Google Chrome and by pressing alt + cmd + j will bring up the console, here you can write JS directly into the browser and get a response. This is in fact how you will also view code you write in the main.js file.

When I first started to learn programing in JS, summing up the obvious helped me to to keep a good understanding of what I was actually trying to achieve (apart from becoming the worlds best programmer of course ;) ). We are trying to create, store, manipulate and move data. Data being something we create in our programs or some other data retrieved from another source. Our language of choice helps us coerce the data with structured commands. An important but basic assistant for this in JS is a variable.

Variables are the containers for our data. By using a variable, we are accessing the data.

<code>
var ourVarName = 'Hello World';
console.log(ourVarName);
<code>

Above I created a variable call 'ourVarName', we know it's a variable due to the var keyword. Inside I stored a String primitive with the text 'Hello World'. JavaScript has a console.log command to print JS to the console. If you have done the same in your main.js file, fire up the console and take a look.

JavaScript is weakly typed so we don't have to specify the type of value a variable contains. Variables can hold any type of data, and they can be overwritten. However, this does mean we have to check our variables at some point with type checking so we don't accidentally end up with an unexspected value.

<code>
console.log(typeof(ourVarName));
<code>

At this point it's customary to say that programmers accustomed to a more statically typed language may not like this, and are now recoiling in horror.
As you can see above, the 'var' keyword is used to declare the variable, then we specify the name we choose typed with camel casing. Camel casing is a typing convention JS programmers tend stick to.
If we don't use the 'var' keyword a global variable is created and this is bad, we don't want global variables, I'll get into how we can avoid this later.
Some other conventions and rules for creating variables are; no spacing in the name, and it must start with an underscore a letter or a number. I tend to stick to a semantic camel-cased name.
We can declare multiple variable names with a single 'var' keyword, the names are separated by commas and we end with semi-colon, and don't forget indenting. The variables may be predefined for later use for example.

<code>
var firstVar,
  secondVar,
  thirdVar;
<code>

Consistency is good, try to keep your code nicely laid out and indented, it's easier to read and will help other people on your team understand your code. Another benefit of being dynamically typed as I mentioned earlier is being able to change a variables type as and when. Declaring an already existing variable to equal a new value will immediately overwrite the value inside. But again as said before this will create a global variable because we have not stated the 'var' keyword. Now let's look at the types of data we can store.

*Data Types*
Being loosely typed, there are not many types. The primary data types in JavaScripts are known as primitives; Number, Sting, Boolean, Undefined and Null.

<code>
var myNumber = 32,
  myBool = true,
  myString = 'a string';
<code>

Notice how with a number we do not place any quotation marks around it, if we did it would become a string. Number can hold any positive or negative decimal. The number can be no less than 5e-324 or greater than 1.7976931348263157e+308. They are a 64-bit floating value.

<code>
console.log(Number.MAX_VALUE);
console.log(Number.MIN_VALUE);
<code>

NaN means not a number, this is an actual value in JS, although NaN's are not even equal to them self's, get used to it and except it. To check if a value is not a number we can use the isNan( ) method.

String - characters enclosed within quotes, either single quotes or double quotes but try and be consistent. A string can concatenate with another string with the  + operator. Actual quote marks can be placed in strings if we escape them with a backslash.

<code>
var myLongString = "This is me saying \ "Hi \" to you" ;
<code>

Boolean - True and False.
Boolean was created by George Boole (2 November 1815 – 8 December 1864) an English mathematician, philosopher and logician, and is now best known as the author of The Laws of Thought.

"No general method for the solution of questions in the theory of probabilities can be established which does not explicitly recognise ... those universal laws of thought which are the basis of all reasoning" - "George Boole (1815–1864)". Kerryr.net. Retrieved 2013-04-22.

We refer to Boolean values as either Falsey or Truthy values. False, 0, '', null, undefined and NaN are all falsey values. All other values are truethy.
Number, String and Booleans are known as primary data types out of the five primitives. The other two are special data types - Undefined and Null. Undefined is a variable that has not yet been assigned a value and is of the type undefined. Null is a data type used in place of other data types, it is a JavaScript literal representing null or an empty value. Common user cases for these types are when we check conditions.

Composite types - Arrays, Objects.
Array's are containers for values, the values they hold have a zero based index, this means to access an arrays first value we would look at the index 0 and the second value would be held at index location 2. Arrays and Objects both have methods we can use to help with manipulating data, I will get into more detail about these later in other posts.
Objects are another type of container for values. The structure of an object is key value pairs. More than one pair can be placed inside of an object separated with a comma, the key and value are separated with a colon. The value of an object can be any data type, strings, numbers, booleans, functions (known as methods when in an object) arrays and even other objects.

<code>
var myArray = ["string", 45, true];
var myObject = { name: "philip", location: "GB" };
<code>

So we now have the data stored in a container, how do we access it?
For Arrays this is where the zero based indexing comes in. An Array like all our other data is to be held in a variable and defined with square brackets as shown above, the square brackets means we are creating an array. These square brackets come into use again to access each value our Array by stating the array name and the index of the value we want contained in square brackets.

<code>
console.log(myArray[1]); // 45
console.log(myObject.name); // philip

var useMe = "location";
console.log(myObject[useMe]); // GB
<code>

To access an Objects data we use dot notation, or bracket notation. Bracket notation is useful when accessing the properties from the object with a variable keyword. Accessing the objects values with names rather than number index like arrays, in other languages this is known as associative arrays, this is because we are associating the given name with our stated value.
Dot notation is the form of concatenating the name of the object with a property of the object with a full stop(dot) name.name, this can go as deep as needed to access the depth of an object.

Operators
JavaScript like all other programming language has the normal arithmetic operators.
+ - Addition, - for Subtraction, * - Multiplication, / - Division and  % - Modulous to find the remainder.
++ can increment,  -- can decrement. Not a lot we can really say about this, it's Math, but one thing you may notice + is used for concatenation and addition. The Modulous is handy for finding odd or even numbers, as the remainder will either be 0 for even or a value for odd.

Increment and decrement can be pre or post fixed  ++var, var++. You will come across this most often in loops. Loops are constructs for looping over the same statements of code as many times as defined and an increment is used to increase a counter to said amount of times to break the loop. Post-fixing returns the original value and then increments, where as pre-fix increment does not suffer from this issue, the value is incremented and then returned. A good reason to consider this is due to off by 1 errors. These errors can offer back unwanted values. Another way to combat this is to avoid using increment operators, and use assignment operators. += 1, - = 1, this is the same as using increment operator but with no confusion. += or -= will take the current value and add 1 or any other value you specify, * = 2; ,  / = 2.5 or even % = ;
I hope we all remember our Math teachings, I talk of the acronym PEMDAS, parenthesis, exponent, multiplication, division, addition and subtraction. This is known as operator precedence - the order in which the operand is evaluated. For example;

1 + 4 * 2 will not be 14. The 4 * 2 would get calculated first and then + 1, it will evaluate to 9. Where as ( 1 + 4 ) x 2 would be evaluate to 14.

Comparison operators
At some point while writing your JavaScript you will need to compare some values. Comparison operators can help us with this. There are two types, regular or strict comparison. This is easily noticed by either seeing two or three signs, 1 == true this is a regular comparison and it equals true. 1 === true, this as a strict comparison and equals false. Notice there are either two equal signs or three equal signs, two will compare if the values are the same, JS will also try it's best to help figure this out with cohersion if you say try to compare the string '2' with the number 2. But three equal signs will strictly compare the type and comparing a string with a number will be false. It's best to stick with strict comparing.

<code>
var numberTwo = 2;
var stringTwo = '2';
numberTwo == stringTwo = true
numberTwo === stringTwo = false
<code>

Continuing on with operators, here we have a selection of unary operators. Unary operators are operators with only one operand, i.e. a single input.
Because true is equal to binary 1, +true will equal 1. And the opposite is as expected, -true = -1
Using the a single bang operand is the same as saying not! So !true = false
Then we have delete operand, this will delete an object, a property of an object or an  element of an array index.
typeof will help us to find out the type of operand we are dealing with. typeof gets the type in string form.
Some examples;
typeof 1 = 'number'
typeof 'hello' = string
typeof true = boolean
typeof [ ] = object. Yes that's right, an Array is an Object!
typeof null = object. Being a primitive we would expect null, but a bug that has long been in JavaScript gives us object. It exists still so backward compatibility can be maintained.

&& operator. When using the && ( which means 'and') all values must be truthy to return true. This is because of something called short circuit operators, the second operand value will return based on the first operand value.
| | operator (which means 'or') returns true if any operand returns true. short circuit looks for first true and stops.
You will use these short circuit operands as conditions to check a value passes two specified checks

<code>
var myNumber = 4;
if (myNumber > 3 && myNumber <= 8 {
	console.log('short-circuit');
	}
<code>

A better look at Objects.
Objects are comma separated, key value pairs contained in curly braces. The key and value are known as properties of the object. The identifier of the property is the key, and the value is the value/data. Any data type, even arrays, objects and functions, which are known as methods when a property of an object can be stored as the value. We create object literals with a simple, var newValue = { }; the curly braces signify we have created an object. Once an object is created, properties/variables can be set to the object, as well as methods/functions. Furthermore we can use the 'new' key word to create an instance of the object just created. This way, you can have a default set of values for a generic object ready to use and expand on when needed. To access and use the objects, we use what's know as dot notation.

Square brackets can be used to access values in an object
and you can update with square bracket notation. this is useful to use a variable as a key to access a value.

<code>
function getThingByValue(value) {
	var things = {
		red: 'a red thing',
		blue: 'a blue thing',
		green: 'a green thing'
		};
	return things[value] || 'this alternate message';
}
getThingByValue(red); = a red thing
<code>

You can also easily add to an object, by using the assignment operator = obj.prop = 'value'

Functions, functions functions.
A logical grouping of expressions, invoked as we need them, what could be better?
These group of logical expression are reusable code, there is a term in programming known as DRY this stands for Don't Repeat Yourself. If you find that you are repeating a similar piece of code, then you have probably found a good case to write a function.

Once a function is created and ready to use we can invoked the function with its name and a set of parenthesis. Inside the parenthesis we can place arguments also known as parameters, these are treated as variables. Think of these variables as place holders for data that you may want to pass into your function when you invoke it. A function will always returns a value, even if this value is undefined. In addition, the return statement is used to return said value, or break/stop the function.
There are two ways to define a function, a function expression and a function declaration.

<code>
function thisNewFunction() {
  // statements
}

var myNewFunc = function() {
  // statements
}
<code>

JavaScript functions are higher order functions, this means you can pass functions as arguments, and invoked said function through the arguments in the function, this is known as callback functions (when we want another function to execute after the first function).

At runtime (when the code runs) variables are procced before any other code, so it is a good idea to place them at the top of their scope, If they are not JavaScript Hoists them to the top anyway, this is known as 'Hoisting'. Placing your code in the wrong place and experiencing hoisting can cause code not to run as expected. You may get reference errors, undeclared variable. Function declarations are also hoisted, function expressions however are not hoisted which is why they are preferred by some programmers. You can immediately invoke a function with an IFFE, or by starting the function with a unary declaration ! Leading bang syntax.

<code>
function add(a, b) {
  return a + b;
}

var meNumber = add(2, 2);
console.log(meNumber); // 4
<code>

Scope
Scope is a simple feature and is in most languages. Scope defines the visibility of our variables throughout the code. With ES6 we have better ways of defining our scope, but it is still an important feature to understand. The Global scope is the JavaScript top level scope, typically the window object.
Contaminating the global scope with lots of variables is very bad, this is due to naming conflicts, with our own code and if we use other developers code. Another down side to global variables is they are automatically added as properties to window object. It is good practice to contain our code keeping the scope of our variables in safe places where they cannot harm anyone else.

The window object is not all bad and to be avoided, it has many useful properties we can use, finding out the url is one of them by using the location object which is a prop of window object.
href in turn is a property of location, this is a good example how we access and use objects with dot notation as I mentioned earlier,  window.location.href. Writing that in your console will print your current URL.
Back to scope, the global scope contains all other scopes (when I scopes I mean anywhere a group of code exists), we can create new private scope with functions or Immediately invoked function expressions, 'IFFE' for short. A IFFE will invoke itself, immediately in fact creating new scope for our variables to be contained in and not letting them leak out unless we say so.

<code>
(function() {
  // private code
  }());
<code>

JavaScript has function scope, but ES6 (ES6 is the latest release of JavaScript) lets us define block scope, I shall not be going into ES6 in this post. What's the difference between block scope and function scope I hear you ask? A variable defined inside a function is only accessible within that function, unless returned by the function. The variable cannot be updated from outside of its scope either. Block scope however has the same sort of traits but the scope is set between the curly braces. To summarize, if you were to define a 'for' loop with a function, the loop syntax uses a new set of curly braces, any variables created inside this loop is accessible with the function it was created in, with block scope this would not happen. I previously mentioned a common user case for using scope to our advantage, the IIFE.

This
An unusual concept and one that can get tricky to explain is 'this'. This can get interesting to read when explaining this on this blog post as this can easily get this out of context, hahaha a little joke.
'this' normally refers to an object but it can be different values depending where it is used, when I say where it is used I literally mean using the keyword 'this' as a reference. The value of 'this' inside a new immediately invoked function expression is undefined as it is not set to anything. However if we are inside a function that is the property of an object, 'this' will point toward that object. Outside of the function, 'this' points to the global window object, this is because defining a function in global scope automatically makes it a property of the window object. We can use functions to create instances of objects, in this case, 'this' points to the instantiated object. 'this' is also different with events, when the ui creates an event, 'this' points toward the element that triggers the event, if a button is clicked for example the button is 'this'. The methods .call and .apply can help us to point 'this' in different directions, we will see more on these methods another time.

When creating your variables and functions name, we need to consider reserved words, also known as keywords. To avoid conflicting with JS and it's API's try to make your identifiers unique and semantic to your project. Most browsers or IDE's will alert you to the fact you are trying to use a keyword, like 'window' for example. As you learn JS better, you will come to realize what names not to use. JSlint or JShint can also help us to pick up error in our code, these perform static analysis on our code and inform us of mistakes. however key words could be used as property key names inside objects because we can wrap them in quotes, and then use bracket notation to access the properties. I prefer to stick with unique naming.

I hope you have found this post useful, it was not intended for JavaScript experts, but as a high level overview of some features JavaScript has to offer for the beginner coder. This is part 1 and part two is being worked on to finish up and show even more of this dynamic language! Thanks for reading.
