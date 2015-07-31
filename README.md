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

My solution

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
