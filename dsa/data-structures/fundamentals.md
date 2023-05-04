

# Data Structures

### What are Data Structures?

A data structure is a specialized format for organizing, processing, retrieving and storing data.


### Why are Data Structures important?

Think of a library, think of how many different types of mediums for media there are in a library, books, magazines, dvds, blu-rays, cassette tapes, cds. You could think of each of these medums as data structures. Each medium has its trade-offs

A DVD for example, its cheaper, yet cant store nearly as much data as a blu-ray, and a blu-ray has more capacity but is more expensive

Data structure sin programming have similar trade offs instead of expensive monetarilly data structures could be expensive in time & space

There is no better Data Structure, simply just the better data structure for the situation or job



### Type of Data Structures

In CS There are a lot of Data Structures

- Hash Map
- Array
- Binary Search Tree
- Linked List
- Stack
- Queue
- Heap
- Graph

As JavaScript Developers, we are already familiar with at least two Data Structures. 

- Object
- Array

In JavaScript, there is actually a total of 4 OOTB Data Structures (Array, Object, Map, Set)

In Computer Science, a more formal name for these two data structures would be Hasm Map (Object) & Dynamic Array (Array), however each language has their own name for each data structure


#### Dynamic Array

- Python: List
- Java: ArrayList
- JavaScript: Array
- C/C++/Rust: Vector


#### Hash Map/ Hash Table

- Python: Dictionary
- JavaScript: Object 
- Java: Hash Map
- C#: Dictionary




However, just because JS gives us only two DS out-of-the-box, doesn't mean thats all we can work with. With the current Data Structures we have in JS, we can implement other Data Structures.



For example, if we wanted to implement a Stack with JavaScript





```js
class Stack{
constructor(){
    this.stack = []
    }
    push(value){
        this.stack.push(value)
    }
    pop(){
        return this.stack.pop()
    }

}

```


As you can see here, we are using ES6 Classes to create a Stack constructor, which is using a basic JS array as its core DS. The way I like to think of this is that we're using an array but we are implementing a stack


Now to drive one of my most important points about DS. 

Think of Data Structures as __BEHAVIOR__ 

Here we are limiting the usage of this array to only push and pop, therefore weve implemented the behavior of a stack


Even if I decided to rid the contructor and I just have an array in my code that only pushes and pops.

I could call it a stack


### Major Operations of Data Structures

The major or the common operations that can be performed on the data structures are:

- Searching: We can search for any element in a data structure.
- Sorting: We can sort the elements of a data structure either in an ascending or descending order.
- Insertion: We can also insert the new element in a data structure.
- Updation: We can also update the element, i.e., we can replace the element with another element.
- Deletion: We can also perform the delete operation to remove the element from the data structure.

After the breakdown and implementatiopn of each Data Structure, we'll measure the time complexity for each of these operations for a single DS

### Learning Data Structures

Learnning new data structures should be split into 3 parts

1. High-Level understanding of the DS
2. Low Level understanding of the DS (How the ds works with memory and time)
3. Implementing the DS with JS


## Array


### High-Level 

- An Array is an __ordered__ collection of values

- Arrays in JS can contain any data type

- Arrays in JS are considered Dynamic Arrays, which mean they are resizable and the size doesnt have be to decalared prior opposed to a Static Array

- Arrays are iterables, you can loop through them


### Low-Level

An Array is a collection of items stored at contiguous memory locations. 

This makes it easier to calculate the position of each element by simply adding an offset to a base value, i.e., the memory location of the first element of the array (generally denoted by the name of the array). The base value is index 0 and the difference between the two indexes is the offset

As stated above, all the data elements of an array are stored at contiguous locations in the main memory. The name of the array represents the base address or the address of the first element in the main memory. Each element of the array is represented by proper indexing.

We can define the indexing of an array in the below ways -

- 0 (zero-based indexing): The first element of the array will be arr[0].
- 1 (one-based indexing): The first element of the array will be arr[1].
- n (n - based indexing): The first element of the array can reside at any random index number.

![Arrays](https://static.javatpoint.com/ds/images/ds-array2.png)

In the above image, we have shown the memory allocation of an array arr of size 5. The array follows a 0-based indexing approach. The base address of the array is 100 bytes. It is the address of arr[0]. Here, the size of the data type used is 4 bytes; therefore, each element will take 4 bytes in the memory.


### JavaScript Implementation
(Notate the big O of each operation)

```js
const arr = [1, 2, 3, 4, 5]

for(const val of arr){
        console.log(val)
    }

arr[5] = 6

arr.push(7)
arr.pop()
arr.shift()
arr.unshift(1,2)

```

### Big-O


#### Operations
- Access O(1)


- Insertion O(n) // unless at the end which is O(1)


- Deletion O(n) // unless at the end which is O(1)


- Searching O(n)

#### Methods

- push() O(1)

- pop() O(1)

- shift() O(n)

- unshift() O(n)



## Hash Maps

JavaScript has built-in Objects and Maps which are implementations of the Hash Map Data Structure. First We are going to learn about those, and then later implement our own Hash Map from scratch

### High-Level

- Hash Maps are __unordered__ collections of data organized into key/value pairs
- Hash Maps are typically very efficient because the key has direct access to the value and operations like insertion, deletion, and access are very fast



### Low-Level

- Hash Maps utilize what is called a __Hash Function__, it takes in a key and generates a index for a fixed size array where the value shall be stored
- These hash functions can accidentilly generate the same index for a key and cause what is known as a "collision", to avoid this they use what is called a hash bucket which is just another data structure like an array used at that specfic index 

![Hash Map](https://www.freecodecamp.org/news/content/images/2021/05/g983.jpg)

### JavaScript Implementation


First let's implement the basic Hash Table, and then refactor it to consider collisions

```
class HashMap {
        constructor(size){
            this.size = size
            this.map = Array(size)
            }
        hash(){

        }
    }

```









