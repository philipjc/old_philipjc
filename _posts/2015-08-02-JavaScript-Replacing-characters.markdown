---
layout: post
title:  "JavaScript, changing String characters"
date:   2015-08-02 17:53:05
categories: Posts 3
---
Getting good at something takes a lot of time and effort. Learning JavaScript is no exception.
I have recently taken up using the site [CodeWars] to practice my JS. [CodeWars] generates different programming problems for you to solve and earn point, once you finish one you can move to the next, I am aiming to do at least one every day. [CodeWars] also offer other language you can practice, Ruby, Python, C# and Java.
I recently solved one said problem, and thought I'd share the result. This specific problem had me digging into many JS methods from the String prototype and Array prototype and really had me thinking. Until Boom! Solved, what a great feeling. It was not the most elegant or succinct solution, but it was my solution and I solved it. Once completed I was also able to see the higher ranked solutions, which was another great learning experience. So, without further adieu.

### The problem.
Create a function that takes a single value, a String. The String will be made up of
{%highlight js%}
[A]|[T]|[G]|[C]
{% endhighlight %}
(This is basic Regular expression for A or T or G or C).
With this String if the character is A change it to T, and perform similar functionality with the rest, T to A, G to C and C to G. Some examples of possible arguments were ['AAAA'], ['AATT'], ['ATGC'].

This is the setup, time to think.
{%highlight js%}
function DNAStrand(dna) {
  // code here

  return dna
}
{% endhighlight %}

My initial thought was I'm dealing with a String and will need to check each character in the String for its value. This is where the Array Method .forEach would be handy, but forEach loops through an Array not a String? I will need to split this String up! Time for the String.split() method. String.split() will do exactly as in sounds, split up a Sting, also it return the new split String inside an Array. Awesome!

{%highlight js%}
function DNAStrand(dna) {
  // code here
  var dna = dna;

  dna = dna.split(',');

  console.log(dna);
  // ['A','A','A','A']

  return dna;
}
DNAStrand('AAAA');
{% endhighlight %}

Okay, nice. So now I have an Array with each individual character ready to loop over.
Array.forEach() will loop through its attached Array and execute a passed function on each element it loops over once. The function passed into forEach also takes the index argument which returns the index value of the current element looped over (this comes in handy later).

{%highlight js%}
function DNAStrand(dna) {
  // code here
  var dna = dna;

  dna = dna.split(',');

  dna.forEach(function (letter, index) {
      console.log(letter);
      // A * 4
  });

  return dna;
}
DNAStrand('AAAA');
{% endhighlight %}

So now that I am looping through each element, I need to check each letter for what its value is. Time for some conditional IF statements!

{%highlight js%}
function DNAStrand(dna) {
  // code here
  var dna = dna;

  dna = dna.split(',');

  dna.forEach(function (letter, index) {

    if (letter === 'A') {
      console.log('I'm an A!);
      // I'm an A! * 4
    }
  });

  return dna;
}
DNAStrand('AAAA');
{% endhighlight %}

This condition currently returns TRUE for each letter, so we should see the console-log four times. If I were to pass a different String like 'AATT' we would only see two console-logs.

Okay, so now I have an Array of characters and I'm checking each one. So I guess now I should change the character to be the desired value. At this point I read up on a fair few different methods, indexOf(), charAt(), replace() and searched some more. I decided to go for a procedural approach and wrote out some sudo code to help me think.

{%highlight js%}
// Loop over each value
// Check each each value
// IF value is === something
// Store its index for reference
// Remove it from the Array
// Convert the value to the new value
// Return the value to the existing Array
// Return the Array
{% endhighlight %}

Woh! There is a fair bit to do here, I'll explain each part and what Method I chose to use for each step. We have already performed the first three steps, time to store the index. Here is where the forEach index argument helps.

{%highlight js%}
function DNAStrand(dna) {
  // code here
  var dna = dna;

  dna = dna.split(',');

  dna.forEach(function (letter, index) {

    if (letter === 'A') {
      var position = index;
    }
  });

  return dna;
}
DNAStrand('AAAA');
{% endhighlight %}

Now we have stored the index of the element we are working with, we can remove it from the Array ready to change its value. Time for some splice()! Some Array methods return a copy of an Array after an execution, like slice for example, you can slice a portion of an Array as a copy, not effecting the original Array. But I would like to actually mutate the Array I am working with. Array.splice() can be used to add or remove and element at an index depending on how many arguments you pass in. Three for adding and two for removing.

{%highlight js%}
var anArray = [1, 2, 3, 4]

anArray.splice(2, 1);

console.log(anArray);
// [1,2,4]
{% endhighlight %}
This removes one(1) element at the given index of 2

{%highlight js%}
anArray.splice(3, 0, 5);

console.log(anArray);
// [1,2,4,5]
{% endhighlight %}
This adds a value(5) at the given index of 3 and removes 0 values.

Lets splice our values using the saved index! Don't forget we need to splice out of the Array, not each Array item in the forEach loop. Also we need to save the spliced element in a variable.

{%highlight js%}
function DNAStrand(dna) {
  // code here
  var dna = dna;

  dna = dna.split(',');

  dna.forEach(function (letter, index) {

    if (letter === 'A') {
      var position = index;
      var character = dna.splice(i, 1);
      // splice 1 letter at its index.
      console.log(character);
      // ['A']
    }
  });

  return dna;
}
DNAStrand('AAAA');
{% endhighlight %}

Awesome, not much more to go. Splice returns the chosen amount of elements in a new Array, cool. But I wanted to change the value, how do I get the value out of the Array? I could pop it out. Array.pop() is another Array method that removes the last index of an Array, you can save the popped value into a variable.

{%highlight js%}
function DNAStrand(dna) {
  // code here
  var dna = dna;

  dna = dna.split(',');

  dna.forEach(function (letter, index) {

    if (letter === 'A') {
      var position = index;
      var character = dna.splice(i, 1);
      character = character.pop();
      console.log(character);
      // 'A'
    }
  });

  return dna;
}
DNAStrand('AAAA');
{% endhighlight %}

Here I saved the variable character to equal itself, but the popped version. And now we have our single character String value ready for change. Because we have a specific target for each character to equal (A - T, T - A and so on...) we know we need to make 'A' values equal a 'T'.

{%highlight js%}
function DNAStrand(dna) {
  // code here
  var dna = dna;

  dna = dna.split(',');

  dna.forEach(function (letter, index) {

    if (letter === 'A') {
      var position = index;
      var character = dna.splice(i, 1);
      character = character.pop();

      var changedChar = character.toString();
      changedChar = 'T';
    }
  });

  return dna;
}
DNAStrand('AAAA');
{% endhighlight %}

First of all I wanted to make sure the popped value was a String, so I parsed it with the toString() method. Then I just made the variable equal a new value 'T'. Now that our current character is the desired result, time to splice it back in with the three argument .splice() method.

{%highlight js%}
function DNAStrand(dna) {
  // code here
  var dna = dna;

  dna = dna.split(',');

  dna.forEach(function (letter, index) {

    if (letter === 'A') {
      var position = index;
      var character = dna.splice(i, 1);
      character = character.pop();

      var changedChar = character.toString();
      changedChar = 'T';

      dna.splice(index, 0, changedChar);
      // add changedChar at index and remove 0 elements
    }
  });

  return dna;
}
DNAStrand('AAAA');
{% endhighlight %}

Yay, our elements are looped through, the index saved, spliced out, popped, changed and spliced back into the Array! Let's see what we return.

{%highlight js%}
function DNAStrand(dna) {
  // code here
  var dna = dna;

  dna = dna.split(',');

  dna.forEach(function (letter, index) {

    if (letter === 'A') {
      var position = index;
      var character = dna.splice(i, 1);
      character = character.pop();

      var changedChar = character.toString();
      changedChar = 'T';

      dna.splice(index, 0, changedChar);
      // add changedChar at index and remove 0 elements
    }
  });

  return dna;
}
var firstTry = DNAStrand('AAAA');
console.log(firstTry);
// ['A', 'A', 'A', 'A']
{% endhighlight %}

Wait! The elements are still split! Ahah! I need to join them. Array.join() is another Array method for joining all values of an Array into a String (the opposite of split()).

{%highlight js%}
function DNAStrand(dna) {
  // code here
  var dna = dna;

  dna = dna.split(',');

  dna.forEach(function (letter, index) {
    if (letter === 'A') {
      var position = index;
      var character = dna.splice(i, 1);
      character = character.pop();
      var changedChar = character.toString();
      changedChar = 'T';
      dna.splice(index, 0, changedChar);
    }
  });
  dna.join('');

  return dna;
}
var firstTry = DNAStrand('AAAA');
console.log(firstTry);
// ['AAAA']
{% endhighlight %}

Woop! It worked. So what about other character values? We can repeat the IF statement and change the letters in the IF and inside the forEach where we set changedChar. After writing this code (just to get it to work) I thought it was pretty verbose and not very DRY (dont repeat yourself) so I decided to move the repeated code out into a separate function.

{% highlight js%}
function flippy(newDna, dnaPiece, newLetter, index) {
    var pos = index;
    var c = newDna.splice(index, 1);
    c = c.pop();
    var t = c.toString();
    t = newLetter;
    newDna.splice(index, 0, t);
    return newDna;
}

function DNAStrand(dna){

    if (!dna) return;
    var newDna = dna.split('');
    newDna.forEach(function (eachDna, index) {
        var eachDna = eachDna;
        if (eachDna === 'A') {
            flippy(newDna, eachDna, 'T', index);
        }
        if (eachDna === 'T') {
            flippy(newDna, eachDna, 'A', index);
        }
        if (eachDna === 'C') {
            flippy(newDna, eachDna, 'G', index);
        }
        if (eachDna === 'G') {
            flippy(newDna, eachDna, 'C', index);
        }
    });
  newDna = newDna.join('');
  return newDna;
}
console.log(DNAStrand('ATTGC'));
{% endhighlight %}

After multiple test cases my functions were working. I clicked run inside the [CodeWars] editor and passed all three test cases! I was super happy!
Not only did I pass, but as I mentioned at the start I got see the better solutions.
The result I took away from the experience was very satisfying, it was my solution and I worked it out, and at the same time got to know better some JS Methods. I also understand the more experienced solution and have learned from it, here it is.

{% highlight js%}
var pairs = {'A':'T','T':'A','C':'G','G':'C'};

function DNAStrand(dna){
  return dna.split('').map(function(v){ return pairs[v] }).join('');
}
{% endhighlight %}

Return the result of a key value from an Object! So easy once you see it :)

Well I hope you have enjoyed reading this experience of mine, until next time!

All of these Methods are attached to their prototype Objects, Sting.prototype, Array.prototype.
Thanks to the great website of [MDN] I have access to all of this knowledge and references to JavaScript.

You will notice I have not used the newer ES6 syntax in this post. I feel more people are still familiar with ES5 way of writing and this would be more understandable to a wider audience.

[CodeWars]: http://www.CodeWars.com
[MDN]: https://developer.mozilla.org
