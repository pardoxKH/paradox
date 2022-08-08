Before delving into Big O notation, a technique used to analyze the efficiency of different algorithms, we need to study the building blocks that the algorithms we are analyzing operate on. Namely, Data Structures.

### Why Data Structures Matter?

Data structures help us increase the quality of our code.
How do we compare the quality of two snippets of code that achieve the same functionality? Do we say, that since both pieces of code achieve the same objective, they are therefore equivalent? This is clearly not the case, blocks of code differ in quality.

The quality of the code depends on two main factors:
	1. Maintainability: for the code to be easily maintainable, it should be easily understood by people who haven't written it. Therefore, it has to be organized, readable, and modular.
	2. Efficiency: An efficient piece of code is one that runs faster, but also one that doesn't consume too many resources. i.e. it's code that attempts to strike a balance between its space and time requirements.

To demonstrate how two pieces of code achieving the same functionality might differ in efficiency,
let's create a function that simply prints the arguments passed to it.

```js
const printArgsV1(initial, final){
	for(let i = initial; i<=final; i++){
		if((i==initial)||(i==final)){
			console.log(i);
		}
		
	}
}
```

```js
const printArgsV2(initial, final){
	console.log(initial);
	console.log(final);
}
```

If we compare the two versions of our function, clearly the second version is much more efficient, in the first version we are looping over all the numbers between initial and final, if initial = 0 and final = 1,000,000, we are essentially doing one million iteration, just to print the values of initial and final. In the second version, on the other hand, we print the two values without a single iteration.

The first version is an inefficient piece of code, and a naive mistake that no programmer would typically make. However, there are more subtle and nuanced optimizations that even seasoned programmers tend to miss. The study of data structures and algorithms would help us spot such mistakes, and avoid them in the first place. 

### What are Data Structures?
Data structures are ways of organizing pieces of data.

```js
let a = 1;
let b = 2;
let c = 3;

console.log(a+b+c); //outputs 6
```

```js
const arr = [1,2,3]
console.log(arr[0]+arr[1]+arr[2]); //outputs 6
```

In both cases, the result is the same. Which is the sum of the numbers 1, 2, and 3. However, when we execute the `console.log()` statement, the source of the data to be summed is different. In the first snippet we are retrieving the values 1, 2, 3 from memory, where each value is assigned to a separate variable a, b, c. In the second case, the values are *organized* in an array, all of them are stored in a single data structure, called an array. Instead of being stored separately, each in its unique variable.

When building a piece of software, a web application for instance. How we choose to *organize* our data is of great significance. Because the way data is organized affects the storage and the retrieval of that data. Therefore, directly affecting the performance.

If we take tiktok's feed for instance, those videos you are scrolling through have to be stored somewhere, how they are stored, displayed and organized would directly affect the experience of the millions of users who are requesting the data simultaneously while scrolling through the feed.

To summarize:
	Data structures are ways of organizing data in memory, knowing what data structure to choose for a given problem would directly affect the efficiency of manipulating the organized data, i.e. adding to it, searching it, retrieving from it, or removing it.

### Data Structure Operations
- Read: Answering the question, **what value resides in a given location of the data structure?**
- Search: Answering the question, **does the value exist in the data structure, if it does, what's the location of that value?**
- Insert: **Adding a given value to a specific location in the data structure.**
- Delete **Removing a particular value from the data structure, or removing the value in a given location.**

### Choosing a Data Structure
Our choice of a data structure is critical, because the four main operations carried out on a data structure (Read, Search, Insert, Delete), the efficiency of these operations is affected by the data structure we are operating on.

#### Speed as a performance metric
"If you take away just one thing from this book, let it be this: when we measure
how “fast” an operation takes, we do not refer to how fast the operation takes in terms of pure *time*, but instead in how many *steps* it takes."
Jay Wngrow- A common sense guide to data structure and algorithms

We've seen a demonstration of this in [[Why Data Structures Matter]], where `printArgs2` was faster because it took a fraction of the number of steps (iterations) taken in `printArgsV1`.

Why do we measure speed of an operation ([[Time Complexity]])
by the number of steps instead of the time it takes?
Because, the time an operation takes is a function of the hardware the operation is running on. While, the number of steps of an operation is only dependent on the implementation of the operation, i.e. the piece of code which is what we're interested in.


### The Array Data Structure
The first data structure we are going to discuss, is the simplest and the wildly used, the arrays.
Arrays are contiguous space in memory, where the computer associates the address of the zeroth element of the array and its with the array's address.

![[Pasted image 20220801185022.png]]

As we've mentioned earlier, the importance of the choice of the data structure lies in the fact that it affects the efficiency of the four main operations. Before going through each of these operations with respect to the array data structure, here is a list of the operations and their efficiency.

The cost of each operation on the array:

|Operation|Best Case|Worst Case|
|---------|---------|----------|
|[[Read-Arrays]]|1 step|1 step|
|[[Search-Arrays]]|1 step|N steps|
|[[Insert-Arrays]]|1 step|N+1 steps|
|[[Delete-Arrays]]|1 step|N steps|

## The Array Operations
### Arrays Read Operation
created on: 2022-08-01 14:28

As we've mentioned in [[Speed as a Performance Measure]], we measure the speed of an operation by the number of steps it takes. 
To read a variable from memory, it takes a single step,  which is a retrieval from memory step.
If we take the [[array]] data structure. To read an element from an array, it also takes a single step, that's quite fast. And is attributed to the way the data is organized in an array.

To understand this, let us see what happens when we define an array:
```js
let arr = ['a','b','c','d'];
```
when the array `arr` is defined, the computer has to store the data in memory, an array by definition in a contiguous space in memory, meaning, the values 'a', 'b', 'c', 'd' are going to be stored in sequential addresses in memory. 
for example:
value 'a' at memory location 005
value 'b' at memory location 006
value 'c' at memory location 007
value 'd' at memory location 008

```js
let x = arr[0]
let y = arr[3]
``` 

Each array stored in memory is associated with an address, the address of the element in the zeroth index, in our example, array `arr` would be associated with the address 005. Accessing any element other than the one stored at the zeroth element would be equivalent to accessing the element at the address: array's address + index we are trying to access. 

Consequently, the first line is equivalent to: go to the address 005 of the array `arr`, add 0 to the address (The index we're reading), read the value at the address 005 + 0, then assign it to the variable x. That's two steps, a read step, and an assignment step.

Similarly, the second line is equivalent to: go to the address 005, add 3 to it (the index we're reading), read the value at the address 005+3, then assign it to the variable x. Also, two steps, a read step and an assignment step.

Note that reading from an array costs exactly one step regardless of the location (index) we are interested in reading from. This is why arrays as a data structure are considered attractive, it's because it costs one step to read from any position in the array.

### Arrays Search 
Based on the definition of the search operation in [[Data Strcture Operations]], if we are looking for a particular value in an array, it means that we don't have the index of the value we are looking for, if we don't have the index, it means that we can't read it. Therefore, we need to look for the index where the value of interest resides. 

Assume there is a defined function `search`, that takes two arguments, an array and a value to look for within the array, and returns the index in which the value was found.

```js
arr = ['a','b','c','d'];

locA = search(arr,'a'); 
locC = search(arr,'c');
```

Executing the function `search(arr,'a')` based on the previous definition of the function would return the value 0, and `search(arr,'c')` would return the value 2. 

To find the index where the value is stored, the computer looks for the value started at the address of the array (which is at the zeroth index), if the value is found there it returns the index, otherwise it proceeds to the adjacent address (address + 1), until it traverses the full array.

Therefore, if it finds the value at index 0, it takes it one step, if it finds it at index 3 it takes 4 steps, if the array is of size 1000 and the element is at index 999, it takes it 999 steps to find it. And if the array is of size n, and the value is at the last index of the array, then it takes the search n steps to find the value. This is known as linear search, it's one search algorithm, there are many others that are more efficient as we'll see later.  

### Arrays Insert
Inserting data into an array is dependent on the position we are inserting the data in.

- Appending the data to the array takes one step.
	```js
	let arr = ['a','b','c'];
	arr.push('d');
```

pushing the value d to the array `arr` , is equivalent to telling the computer to go to the address of `arr` (which is the address of the zeroth element in the array), adding the size of the array to it, reaching the address where d is supposed to be added, i.e. at the end of the array. When an array is stored in memory, the computer keeps track of the array's size. [[The Array Data Structure]]

- Inserting in a position other than the end of the array.
If we want to insert the value "x" at index 2 of the array `['a','b','c']`, then we would need to shift c to index 2 for x to take its place, similarly if we want to insert x at index 1, we would need to shift both c and b to the right for x to be inserted. We notice that inserting at the first index of the array would result in the largest number of steps required for insertion. Namely, N + 1 steps, N shifting steps and 1 insertion step, where N is the size of the array.

### Arrays Delete
Deleting is very similar to the [[Insert-Arrays]] operation.

- Deleting the final element takes exactly one step. 
	Assume we have a function delete, that removes the value stored at the passed index. 

	```js
	let arr = ['a','b','c'];
	arr.delete(2);
```

the array would become `['a','b']`, however if we want to delete element b:
```js
let arr = ['a','b','c'];	
arr.delete(1);
```
Thiss would result in removing the value b, then moving the value c from index 2 to index 1 to replace the location of the index that was occupied by b, this done to preserve the array as a data structure ofcontiguouss locations.Similarlyy if we want to delete the value at index 0, it would cost us a step for deletion, and two steps to shift b to index 0, and c to index 1. Consequently,in ann array of size N, deleting its zerothh element would cost us N steps.

## The Set Data Structure

There are differentt types of sets, array-based sets in particular are identical to arrays with one additional constraints. The constraint being that it doesn't allow storing duplicates.

This would have an implication on one of the operations, let's investigate the speed of each of the operations:
1. Read: it takes one step to read a value at a given index, just like an array.
2. Search: it takes the 1 step in the best case and N steps in the worst case to find an element in a set, just like arrays
3. Insertion: To insert an element into the set, we have to make sure that the element doesn't already exist in the set. Therefore, an insertion operation consists of search (to look for that element), and insertion steps to insert it. i.e in the best case, it would take N+1 steps to insert an element at the end of the array (N steps for search and 1 for insertion), and in the worst case, which is inserting an element at the beginning of the array it would require N steps of search. And N steps of shifting the elements to the right to free up space at the zeroth index and 1 step to insert the new value. i.e. a total of 2N+1 steps.
4. Deletion: it takes the same number of steps as arrays, one step for deletion and the number of elements to the right of the deleted element for shifting. If we're deleting the last element of the set, then we need only one step (to delete), if we are deleting the first element of an array of size N, then we need 1 step to delete the element and N-1 steps to shift the elements to the left, which is a total of N steps.

To sum up:
The cost of each operation in an array-based set:

|Operation|Best Case|Worst Case|
|---|---|---|
|Read| 1 step| 1 step|
|Search|1 step| N steps|
|Insert|N+1|2N+1 steps|
|Delete|1 step|N steps|






