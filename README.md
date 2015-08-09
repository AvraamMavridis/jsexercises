###EX 1

Description:

In order to stop too much communication from happening, your overlords declare that you are no longer allowed to use certain functionality in your code!

Disallowed functionality:

Strings
Numbers
Regular Expressions
Functions named "Hello", "World", "HelloWorld" or anything similar.
Object keys named "Hello", "World", "HelloWorld" or anything similar.
Without using the above, output the string "Hello World!" to prove that there is always a way.

**My solution:**

```javascript
var p = (function () {
  var base = +(true);
  var ena = +(true);
  var dio = +(true) + (+(true));
  var tria = (+(true)) + (+(true)) + (+(true));
  var tessera = (+(true)) + (+(true)) + (+(true)) + (+(true));
  var pente = (+(true)) + (+(true)) + (+(true)) + (+(true)) + (+(true));
  base = ++base * ++base + (+(true)) + (+(true));
  base = base * base + (+(true)) + (+(true));
  var _ = base + (dio * tria);
  var __ = base + (tria);
  var ___ = base + (dio * pente);
  var ____ = ___ + tria;
  var _____ = ____ + tria;
  var ______ = _____ + pente;
  var _______ = base + dio;
  var H = String.fromCharCode(_);
  var E = String.fromCharCode(__);
  var L = String.fromCharCode(___);
  var O = String.fromCharCode(____);
  var W = String.fromCharCode(______);
  var R = String.fromCharCode(_____);
  var D = String.fromCharCode(_______);
  var space = String.fromCharCode(Math.floor(base/dio) - ena)
  var exclamationmark = String.fromCharCode(base/dio)
  return H + E.toLowerCase() + L.toLowerCase() + L.toLowerCase() + O.toLowerCase() + space + W + O.toLowerCase() + R.toLowerCase() + L.toLowerCase() + D.toLowerCase() + exclamationmark;
})

var helloWorld = p;

```

###EX 2

Description:

One of the services provided by an operating system is memory management. The OS typically provides an API for allocating and releasing memory in a process's address space. A process should only read and write memory at addresses which have been allocated by the operating system. In this kata you will implement a simulation of a simple memory manager.

JavaScript has no low level memory API, so for our simulation we will simply use an array as the process address space. The memory manager constructor will accept an array and will allocate blocks of indices from that array rather than memory pages.

Memory Manager Contract

allocate

allocate accepts an integer and returns an integer pointer which should be the index of the beginning of a sequential block of indices of length size in the array passed to the constructor. If there is no such sequential block available this method should throw an exception.

release

release accepts an integer which must be a pointer previously returned from allocate and releases the block beginning at that pointer. If the released block is adjacent to another free block, the two blocks should be merged to form a larger free block. Releasing an unallocated block should cause an exception.

write

To support testing this simulation our memory manager needs to enforce read/write restrictions. Only indices within allocated blocks may be written to. The write method accepts an index integer and a value. If the index is within an allocated block, the value should be stored to the backing array; otherwise, this method should throw an exception.

read

This method is the counterpart to write. Only indices within allocated blocks may be read. The read method accepts an index integer. If the index is within an allocated block, the method should return the value from the backing array at that index; otherwise, this method should throw an exception.

**My solution:**

```javascript
function fix(arr, memory){
  for(var i = 0; i<memory.length; i++){
    memory[i] = arr[i][2];
  }
}

/**
 * @constructor Creates a new memory manager for the provided array.
 * @param {memory} An array to use as the backing memory.
 */
function MemoryManager(memory){
  this.arr = Array.apply(null, memory).map(function(){return 0;});
  this.memory = memory;
  fix(this.arr, this.memory);
}

/**
 * Allocates a block of memory of requested size.
 * @param {number} size - The size of the block to allocate.
 * @returns {number} A pointer which is the index of the first location in the allocated block.
 * @throws If it is not possible to allocate a block of the requested size.
 */
MemoryManager.prototype.allocate = function(size){
  var pointer = this.arr.indexOf(0);
  if(this.arr.length - pointer >= size){
    this.arr[pointer] = [true, size, 0];
    for(var i = pointer + 1; i<size; i++){
      this.arr[i] = [false, size, undefined];
    }
    fix(this.arr, this.memory);
    return pointer;
  }
  else{
   throw Error('No space');
  }
};

/**
 * Releases a previously allocated block of memory.
 * @param {number} pointer - The pointer to the block to release.
 * @throws If the pointer does not point to an allocated block.
 */
MemoryManager.prototype.release = function(pointer){
  if(this.arr[pointer] == 0 || !this.arr[pointer][0]){
    throw Error();
  }
  else{
    var blocksize = this.arr[pointer][1];
    for(var i = pointer; i <= blocksize; i++){
      this.arr[i] = 0;
    }
   fix(this.arr, this.memory);
   return pointer;
  }
};

/**
 * Reads the value at the location identified by pointer
 * @param {number} pointer - The location to read.
 * @returns {number} The value at that location.
 * @throws If pointer is in unallocated memory.
 */
MemoryManager.prototype.read = function(pointer){
  if(this.arr[pointer] == 0 || !this.arr[pointer][1]){
    throw Error();
  }
  else{
    fix(this.arr, this.memory);
    return this.arr[pointer][2];
  }
}

/**
 * Writes a value to the location identified by pointer
 * @param {number} pointer - The location to write to.
 * @param {number} value - The value to write.
 * @throws If pointer is in unallocated memory.
 */
MemoryManager.prototype.write = function(pointer, value){
  if(this.arr[pointer] == 0){
    throw Error();
  }
  else{
    this.arr[pointer] = [this.arr[pointer][0], this.arr[pointer][1], value]
    fix(this.arr, this.memory);
  }
}
```

###EX 3

Description:

A bomb has been set to go off! You have to find the wire and cut it in order to stop the timer. There is a global var that holds the numeric ID to which wire to cut. Find that and then you can Bomb.CutTheWire(wireKey);

**My solution:**

```javascript
(function(a){
  var keys = Object.keys(a);
  for(var k of keys){
   if(typeof a[k] === 'object'){
   }
   else{
    if(!isNaN(a[k])){
     Bomb.CutTheWire(a[k]);
     return;
    }
   }
  }
})(this);
```

###EX 4

Description:

Complete the method (or function in Python) to return true when its argument is an array that has the same nesting structure as the first array.

For example:

```javascript
 // should return true
[ 1, 1, 1 ].sameStructureAs( [ 2, 2, 2 ] );
[ 1, [ 1, 1 ] ].sameStructureAs( [ 2, [ 2, 2 ] ] );

 // should return false
[ 1, [ 1, 1 ] ].sameStructureAs( [ [ 2, 2 ], 2 ] );  
[ 1, [ 1, 1 ] ].sameStructureAs( [ [ 2 ], 2 ] );  

// should return true
[ [ [ ], [ ] ] ].sameStructureAs( [ [ [ ], [ ] ] ] );

// should return false
[ [ [ ], [ ] ] ].sameStructureAs( [ [ 1, 1 ] ] );
```

For your convenience, there is already a function `isArray(o)` declared in the JS version that returns true if its argument is an array, false otherwise.

**My solution:**

```javascript
Array.prototype.sameStructureAs = function (other) {
    Array.prototype.status = Array.prototype.status || true;
    if(this.length != other.length){
      Array.prototype.status = false;
      return false;
    }


    for(var index = 0; index < this.length; index++)
    {

      var val = this[index];
       if(isArray(val) && isArray(other[index])){
          if(val.length != other[index].length){
            [].sameStructureAs([1,2,3])
            Array.prototype.status = false;
            break;
          }
          else{
            Array.prototype.status = true;
            val.sameStructureAs(other[index]);
          }
       }
       else if (!isArray(val) && !isArray(other[index])){
         Array.prototype.status = true;
       }
       else{
         Array.prototype.status = false;
         [].sameStructureAs([1,2,3])
         break;
       }
    }
    return Array.prototype.status;
};
```

###EX 5

Description:

Given an array of positive or negative integers

`I= [i1,..,in]`

you have to produce a sorted array P of the form

[ [p, sum of all ij of I for which p is a prime factor (p positive) of ij] ...]

P will be sorted by increasing order of the prime numbers. The final result has to be given as a string in Java or C# and as an array of arrays in other languages.

Example:

```javascript
I = [12, 15]
result = [[2, 12], [3, 27], [5, 15]]
```
[2, 3, 5] is the list of all prime factors of the elements of I, hence the result.

Note: It can happen that a sum is 0 if some numbers are negative!

Example: I = [15, 30, -45] 5 divides 15, 30 and (-45) so 5 appears in the result, the sum of the numbers for which 5 is a factor is 0 so we have [5, 0] in the result amongst others.

```javascript

function isPrime(a){

  this.results = this.results || {};
  if(typeof this.results[a] != 'undefined'){
    return this.results[a];
  }

   if(a === 2){
    this.results[a] = true;
    return true;
   }

  for(var i=3; i <a; i = i+2){
   if(a%i == 0){
    this.results[a] = false;
    return false;
   }
  }
  this.results[a] = true;
  return true;
}



function sumOfDivided(I){
  var time = process.hrtime()
  var k = I.map(function(r){ return Math.abs(r)});
  var max = Math.max.apply(this, k);
  var arr = [];

  var dev = I.filter(function(l){ return l%2 == 0});
  if(dev.length){
   arr.push([2, dev.reduce(function(sum, n){ return sum + n;}, 0)]);
  }

  for(var i=3; i<max; i = i+2){
    if(isPrime(i)){
      var dev = I.filter(function(l){ return l%i == 0});
      if(dev.length){
       arr.push([i, dev.reduce(function(sum, n){ return sum + n;}, 0)]);
      }
    }
  }
  return arr;
}
```

###EX 6

Description:

Create any card game!

Create a Card Game library of classes which could be used to create any number of basic card games. You'll need at least a Deck class and a Card class.

Deck functionality

A deck has a public attribute:

cards: array of remaining cards in the deck.

...and three public methods:

count(): count of remaining cards in the deck.

shuffle(): randomize the order of the remaining cards in the deck.

draw(n): remove the last n cards from the deck and return them in an array.

Upon initialization, a deck is filled with 52 cards (13 from each of 4 suits).

Card functionality

A card has these public attributes:

suit: a symbol representing the suit of the card.
rank: an integer from 1 to 13. ("ace" is 1, "king" is 13)
Javascript: face_card: is this card a face card? (> 10)
...and these methods:

Ruby: face_card?: is this card a face card? (> 10)
to_s (JS:toString()) : human-readable string representation of the card (e.g. "Ace of Spades", "10 of Clubs", "Queen of Hearts")
Cards must be Comparable to other cards. Compare the ranks of the cards only.

Since this is a low level layer to build card games above, all test input will be valid. All ranks will be between 1 and 13 and all suits will be one of

Ruby: :hearts, :diamonds, :spades, :clubs
Javascript: Card.HEARTS, Card.DIAMONDS, Card.CLUBS, Card.SPADES

**My solution:**

```javascript

var symbols = {
  1: 'Ace',
  11: 'Jack',
  12: 'Queen',
  13: 'King'
}

Card.HEARTS = 'Hearts';
Card.DIAMONDS = 'Diamonds';
Card.CLUBS = 'Clubs';
Card.SPADES = 'Spades';

function Card(suit, rank) {
  this.suit = suit;
  this.rank = rank;
  this.face_card = rank > 10;
  this.valueOf = function(){
    return this.rank;
  }
}

Card.prototype = {
  toString: function() {
    if(typeof symbols[this.rank] === 'undefined'){
      return this.rank + ' of ' +  this.suit;
    }
    else{
      return symbols[this.rank] + ' of ' +  this.suit;
    }
  },
};

function Deck() {
  var kinds = ['Hearts', 'Diamonds', 'Clubs', 'Spades']
  this.cards = [];
  for(var i=0; i<4; i++){
    for(var j=1; j<14; j++){
      this.cards.push(new Card(kinds[i], j));
    }
  }
}

Deck.prototype = {
  count: function() {
    return this.cards.length;
  },
  draw: function(n) {
    var removed = this.cards.slice(-n);
    this.cards = this.cards.slice(0, this.cards.length - n);
    return removed;
  },
  shuffle: function() {
    //Not the greatest shuffle
    var temp = this.cards[0];
    this.cards[0] = this.cards[this.cards.length - 1];
    this.cards[this.cards.length - 1] = temp;
  }
};
```

### EX 7
Description:

In this problem, we are going to be implementing our own enqueue, dequeue, and size methods for the queue constructor we are creating, so we should be able to create new instances of the Queue.

The enqueue method takes in the item as a parameter, while the dequeue method does not.
The size method simply returns the number of items in the queue.
Wait, what?

To enqueue an item into the queue means to insert an item into the back, or tail, of the queue.
To dequeue an item means means to remove the item at the front, or head, of the queue.
In a queue, we remove the item the least recently added.

**My solution:**

```javascript

var Queue = function() {
  this.q = [];
};

Queue.prototype.enqueue = function(item) {
  this.q.push(item);
};

Queue.prototype.dequeue = function() {
  return this.q.shift();
};

Queue.prototype.size = function() {
  return this.q.length;
};

```

##EX 8

Description:

You've just discovered a square (NxN) field and you notice a warning sign. The sign states that there's a single bomb in the 2D grid-like field in front of you.

Write a function mineLocation that accepts a 2D array, and returns the location of the mine. The mine is represented as the integer 1 in the 2D array. Areas in the 2D array that are not the mine will be represented as 0s.

The location returned should be an array where the first element is the row index, and the second element is the column index of the bomb location (both should be 0 based). All 2D arrays passed into your function will be square (NxN), and there will only be one mine in the array.

Examples:

mineLocation( [ [1, 0, 0], [0, 0, 0], [0, 0, 0] ] ) => returns [0, 0]
mineLocation( [ [0, 0, 0], [0, 1, 0], [0, 0, 0] ] ) => returns [1, 1]
mineLocation( [ [0, 0, 0], [0, 0, 0], [0, 1, 0] ] ) => returns [2, 1]

**My solution:**

```javascript
function mineLocation(field){
  var x,y;
  for(var i=0; i< field.length; i++){
    x = i;
    y = field[i].indexOf(1);
    if(y != -1)
      break
  }
  return [x,y]
}
```

## EX 9

Description:

Extend the String object to create a function that converts the value of the String to and from Base64 using the ASCII character set.

Usage:

// should return 'dGhpcyBpcyBhIHN0cmluZyEh'
'this is a string!!'.toBase64();

// should return 'this is a string!!'
'dGhpcyBpcyBhIHN0cmluZyEh'.fromBase64();

**My solution (nodejs):**

```javascript
String.prototype.toBase64 = function(){
  var that = this;
  var s = Object.keys(this).reduce(function(sum, i){ return sum + that[i]; }, '');
  return new Buffer(s).toString('base64');
}

String.prototype.fromBase64 = function(){
  var that = this;
  var s = Object.keys(this).reduce(function(sum, i){ return sum + that[i]; }, '');
  return new Buffer(s, 'base64').toString('ascii');
}
```

##EX 10

Description:

React is "A JavaScript library for building user interfaces". It's become a popular option amongst JavaScript frameworks and now it's supported in Codewars!

For this first React Kata, we'll be exploring how to create elements with React. React has a high level method React.createElement for exactly this purpose. It's usage is as simple as:

`React.createElement('div', { prop: 'value' }, 'Hello world!');`
Where the first argument is the element tag, the second argument is the element's properties and the third tag is the content you want to add into the element.

Your task is to create two wrapper methods called createElement and createUnorderedList for our own purposes.

The createElement method should take in a content, tag, and properties, similar to the React method. We should be able to call this method with just content like createElement('Hello World') and by default it should create a div with the content "Hello World".

The createUnorderedList method should take in list, which is an array strings and create a ul element, whose children are li elements containing the values from the list. Given an array ['apples', 'oranges', 'bananas'], the createUnorderedList method should return a react element with this heirarchy:
```
<ul>
  <li>apples</li>
  <li>oranges</li>
  <li>bananas</li>
</ul>
```
Also, React suggests that you always supply a key property when creating dynamic children so be sure to create a unique key for each child li created.

**My solution:**

```javascript
let React = require('react');

function createElement(content="Hello world!", tag="div", props={}) {
  return React.createElement(tag, props, content);
}

function createUnorderedList(list) {
  let lis = [];
  list.forEach(function(l,i){ return lis.push(React.createElement('li', {key: i}, l)); });
  let ul = React.createFactory('ul');
  return ul({}, lis);
}
```

##EX 11

Description:

It's time to create an autocomplete function! Yay!

The autocomplete function will take in an input string and a dictionary array and return the values from the dictionary that start with the input string. If there are more than 5 matches, restrict your output to the first 5 results. If there are no matches, return an empty array.

Example:

`autocomplete('ai', ['airplane','airport','apple','ball']) = ['airplane','airport']`
For this kata, the dictionary will always be a valid array of strings. Please return all results in the order given in the dictionary, even if they're not always alphabetical. The search should NOT be case sensitive, but the case of the word should be preserved when it's returned.

For example, "Apple" and "airport" would both return for an input of 'a'. However, they should return as "Apple" and "airport" in their original cases.

Important note:

Any input that is NOT a letter should be treated as if it is not there. For example, an input of "$%^" should be treated as "" and an input of "ab*&1cd" should be treated as "abcd".

**My solution:**

```javascript
function autocomplete(input, dictionary){
  input = input.match(/[a-zA-Z]/g).join('');
  return dictionary.filter(function(word){
    var t = word.slice(0, input.length).toUpperCase();
    return t == input.toUpperCase();
  }).slice(0,5);
}
```

##EX 12

Description:

Create the function prefill that returns an array of n elements that all have the same value v. See if you can do this without using a loop.

You have to validate input:

v can be anything (primitive or otherwise)
if v is ommited, fill the array with undefined
if n is 0, return an empty array
if n is anything other than an integer or integer-formatted string (e.g. '123') that is >=0, throw a TypeError
When throwing a TypeError, the message should be n is invalid, where you replace n for the actual value passed to the function.

Code Examples
```javascript

    prefill(3,1) --> [1,1,1]

    prefill(2,"abc") --> ['abc','abc']

    prefill("1", 1) --> [1]

    prefill(3, prefill(2,'2d'))
      --> [['2d','2d'],['2d','2d'],['2d','2d']]

    prefill("xyz", 1)
      --> throws TypeError with message "xyz is invalid"
```

**My solution:**

```javascript
function prefill(n, v) {
  if(isNaN(n) || n < 0 || !isFinite(n) || (n%1 !=0) || (typeof n == "boolean")){
    throw TypeError(n + ' is invalid');
  }
  if(n==0) return [];
  return Array.apply({}, new Array(n)).map(function(i){ return v; });
}
```

##EX 13

Description:

The Array's reverse() method has gone missing! Re-write it, quick-sharp!

When this method is called, it reverses the order of the items in the array it is called on, and then returns that same array.

Here's an example:
```javascript
var input = [1, 2, 3, 4];
input.reverse(); // == [4, 3, 2, 1]  // returned by .reverse()
input;           // == [4, 3, 2, 1]  // items reordered in the original array
```

**My solution:**

```javascript
Array.prototype.reverse = function() {
  let temp,c = 0;
  for(let i=this.length-1; i>=this.length/2; --i){
    temp = this[i];
    this[i] = this[c];
    this[c] = temp;
    c++;
  }
  return this;
};
```

##EX 14

Description:

Create a combinator function named flip that takes a function as an argument and returns that function with it's arguments reversed.

For example:
```js
flip(print)(4,5) // returns "5 -> 4"
function print(a,b) {
  return a + " -> " + b;
}
```
The idea is to reverse any number of arguments using a higher order function, without any concern for the function being passed into it.

**My solution:**

```javascript
function flip(fn) {
    return function(){
      var params = Array.prototype.slice.call(arguments).reverse();
      return fn.apply(this, params);
    }
}
```

##EX 15

Description:

Given an array of integers of any length, return an array that has 1 added to the value represented by the array.

For example an array [2, 3, 9] equals 239, add one would return an array [2, 4, 0].

[4, 3, 2, 5] would return [4, 3, 2, 6]

The array can't be empty and only positive, single digit integers are allowed. The function should return null if the array is empty or any of the array values are negative or more than 10.

[1, -9] would return null/nil/None (according to the language implemented).

```javascript
function upArray(arr){

  if(arr.some(function(i){ return i>9 || i <0;}) || !arr.length) return null;

  var t = arr.join('').toString().split('').map(function(i, index, array){
    if(index == array.length-1) return +i + 1;
    return +i;
  }).reverse();


  for(var i=0; i<t.length; i++){
    if(t[i] == 10){
      t[i] = 0;
      t[i+1] = t[i+1] + 1;
    }
  }

  t.reverse();

  if(!t[0])
    t[0] = 1;

  return t;

}
```

##EX 16

Description:

In this Kata, you will implement The Luhn Algorithm, which is used to help validate credit card numbers.

Given a positive integer of up to 16 digits, return true if it is a valid credit card number, and false if it is not.

Here is the algorithm:

If there are an even number of digits, double every other digit starting with the first, and if there are an odd number of digits, double every other digit starting with the second. Another way to think about it is, from the right to left, double every other digit starting with the second to last digit.

```coffee
1714 => [1*, 7, 1*, 4] => [2, 7, 2, 4]

12345 => [1, 2*, 3, 4*, 5] => [1, 4, 3, 8, 5]

891 => [8, 9*, 1] => [8, 18, 1]
```
If a resulting doubled number is greater than 9, replace it with either the sum of it's own digits, or 9 subtracted from it.
```coffee
 [8, 18*, 1] => [8, (1+8), 1] => [8, 9, 1]

 (or)

 [8, 18*, 1] => [8, (18-9), 1] => [8, 9, 1]
 ```
Sum all of the final digits
 ```coffee
 [8, 9, 1] => 8+9+1 => 18
 ```
Finally, take that sum and divide it by 10. If the remainder equals zero, the original credit card number is valid.
```coffee
 18 (modulus) 10 => 8.  
 #8 does not equal 0, so 891 is not a valid credit card number.
 ```

 **My solution:**

 ```coffee
 validate = (n) ->
  k = n.toString().split('').map((i, index) ->
    if ((n.toString().length % 2 != 0 and index % 2 != 0) or (n.toString().length % 2 == 0 and index % 2 == 0))
      +i * 2
    else
      +i
  ).map((i) -> if i > 9 then i-9 else i)
  .reduce((sum, i) ->
    sum + i
  ,0)

  !(k%10)
```

##EX 17

Description:

Number is a palindrome if it is equal to the number with digits in reversed order. For example, 5, 44, 171, 4884 are palindromes and 43, 194, 4773 are not palindromes.

Write a method palindrome_chain_length which takes a positive number and returns the number of special steps needed to obtain a palindrome. The special step is: "reverse the digits, and add to the original number". If the resulting number is not a palindrome, repeat the procedure with the sum until the resulting number is a palindrome.

If the input number is already a palindrome, the number of steps is 0.

Input will always be a positive integer.

For example, start with 87:

87 + 78 = 165; 165 + 561 = 726; 726 + 627 = 1353; 1353 + 3531 = 4884

4884 is a palindrome and we needed 4 steps to obtain it, so palindrome_chain_length(87) == 4

**My solution:**

```coffee
palindrome_chain_length = (n) ->
  this.counter = this.counter || 0
  if(n.toString().split('').reverse().join('') == n.toString())
    c = this.counter
    delete this.counter
    return c
  else
    this.counter++
    palindrome_chain_length(n+(+n.toString().split('').reverse().join('')))
```

##EX 18

Description:

Write a method that takes a field for well-known board game "Battleship" as an argument and returns true if it has a valid disposition of ships, false otherwise. Argument is guaranteed to be 10*10 two-dimension array. Elements in the array are numbers, 0 if the cell is free and 1 if occupied by ship.

Battleship (also Battleships or Sea Battle) is a guessing game for two players. Each player has a 10x10 grid containing several "ships" and objective is to destroy enemy's forces by targetting individual cells on his field. The ship occupies one or more cells in the grid. Size and number of ships may differ from version to version. In this kata we will use Soviet/Russian version of the game.


Before the game begins, players set up the board and place the ships accordingly to the following rules:
There must be single battleship (size of 4 cells), 2 cruisers (size 3), 3 destroyers (size 2) and 4 submarines (size 1). Any additional ships are not allowed, as well as missing ships.
Each ship must be a straight line, except for submarines, which are just single cell.

The ship cannot overlap or be in contact with any other ship, neither by edge nor by corner.

**My solution:**

```coffee
checkCollapse = (field) ->
  field.every((row,i, array) -> 
    row.every((cell, j, ar) ->
      if cell == 1
        t = [array[i-1]?[j-1], array[i-1]?[j+1], array[i+1]?[j-1], array[i+1]?[j+1]].filter(Boolean).length
        return t == 0
      else
        return true
    )
  )
  
countShips = (field, nc) ->
  pattern1 = '0'
  pattern2 = ''
  pattern3 = ''
  for l in [1..nc]
    pattern1 += '1'
  
  pattern2 = '^' + pattern1.slice(1, pattern1.length) + '0'
  pattern3 = '0' + pattern1.slice(1, pattern1.length) + '$'
  pattern1 = pattern1  + '0'
  counter = 0
  for row in field
    t = row.join('')
    l1 = (t.match(new RegExp(pattern1,'gi')) || []).length 
    l2 = (t.match(new RegExp(pattern2,'gi')) || []).length 
    l3 = (t.match(new RegExp(pattern3,'gi')) || []).length
    counter += l1 + l2 + l3
  counter
  
rotateField = (field) ->
  field.map((row, index, array) ->
    t = field.reduce((sum, i, indx, array) ->
      sum.push(i[index])
      return sum
    ,[])
    return t
  )
  
validateBattlefield = (field) -> 
  return false if checkCollapse(field) == false
  
  battleships = countShips(field, 4) +  countShips(rotateField(field),4)
  cruisers = countShips(field, 3) +  countShips(rotateField(field),3)
  destroyers = countShips(field, 2) +  countShips(rotateField(field),2)
  aces = field.reduce((sum, row) -> 
    return row.filter(Boolean).length + sum
  ,0)
  submarines = aces - 4*battleships - 3*cruisers - 2*destroyers
  return battleships == 1 and cruisers == 2 and destroyers == 3 and submarines == 4
```

##EX 19 

Description:

Sudoku Background

Sudoku is a game played on a 9x9 grid. The goal of the game is to fill all cells of the grid with digits from 1 to 9, so that each column, each row, and each of the nine 3x3 sub-grids (also known as blocks) contain all of the digits from 1 to 9. 
(More info at: http://en.wikipedia.org/wiki/Sudoku)

Sudoku Solution Validator

Write a function validSolution that accepts a 2D array representing a Sudoku board, and returns true if it is a valid solution, or false otherwise. The cells of the sudoku board may also contain 0's, which will represent empty cells. Boards containing one or more zeroes are considered to be invalid solutions.

**My solution:**

```coffee
hasUniqValues = (arr) -> arr.every((i, index, array) -> index == array.indexOf(i))

hasNoZeros = (arr) -> arr.filter(Boolean).length == arr.length
  
rotateBoard = (board) ->
  board.map((row, index, array) ->
    board.reduce((sum, i, indx, array) ->
      sum.push(i[index])
      sum
    ,[])
  )

createIndividualsCellsBoard = (board) ->
  newBoard = []
  for i in [0..board.length-1] by 3
    r1 = board.filter((val, index) -> index < 3)
    r1 = r1[0].splice(0,3).concat(r1[1].splice(0,3)).concat(r1[2].splice(0,3))
    r2 = board.filter((val, index) -> index >= 3 and index <6)
    r2 = r2[0].splice(0,3).concat(r2[1].splice(0,3)).concat(r2[2].splice(0,3))
    r3 = board.filter((val, index) -> index >= 6 and index <9)
    r3 = r3[0].splice(0,3).concat(r3[1].splice(0,3)).concat(r3[2].splice(0,3))
    newBoard.push(r1,r2,r3)
  newBoard

validSolution = (board) ->
  board.every(hasNoZeros) and board.every(hasUniqValues) and rotateBoard(board).every(hasUniqValues) and createIndividualsCellsBoard(board).every(hasUniqValues)   
```

##EX 20

Description:

Instructions

Write a function intersect that takes any number of arguments. The function must return an array containing all the values that is present in every argument given to the function.

All arguments given will be arrays.
The first argument determines the order of the returned values.
Return an empty array for empty result set.

```javascript
Example

var a = ['dog', 'bar', 'foo'];
var b = ['foo', 'bar', 'cat'];
var c = ['gin', 'bar', 'foo'];

intersect(a, b, c); // ['bar', 'foo']
```

**My solution:**

```javascript
var intersect = function () {
  arrays = Array.prototype.slice.call(arguments);
  if(arrays.length == 0) return [];
  return arrays[0].filter(function(word){
    return arrays.every(function(array) { return array.indexOf(word) > -1});
  });
};
```

##EX 21

Description:

Write a function cubeSum(n, m) that will calculate a sum of cubes of numbers in a given range, starting from the smaller (but not including it) to the larger (including). The first argument is not necessarily the larger number.

**My solution:**

```javascript
function cubeSum(n, m){
  return Array.apply({},Array(Math.abs(n-m))).map(function(i,index){ return Math.pow(Math.max(m,n) - index, 3); }).reduce(function(sum, i){ return sum+i; }, 0);
}
```

##EX 25

Description:

Your job is to write a function which increments a string, to create a new string. If the string already ends with a number, the number should be incremented by 1. If the string does not end with a number the number 1 should be appended to the new string.

Examples:

foo -> foo1

foobar23 -> foobar24

foo0042 -> foo0043

foo9 -> foo10

foo099 -> foo100

Attention: If the number has leading zeros the amount of digits should be considered.

**My solution:**

```javascript
function incrementString (strng) {
  if(isNaN(strng.split('').pop())) return strng + 1;
  let digits = strng.match(/[0-9]/g) || '';
  let chars = [];
  if(!!strng.match(/[a-zA-Z]/g)) chars = strng.match(/[a-zA-Z]/g);
  let newnumber = (+digits.filter(Boolean).join('') + 1).toString().split('');
  return chars.join('') + Array.apply({}, new Array(digits.length>newnumber.length? digits.length-newnumber.length:0)).map(function(){return 0}).concat(newnumber).join('');
}
```

