Bubble Sort
created on: 2022-08-06 14:37

- Sorting algorithms solve the following problem: Given an array of unsorted values, how can we sort them such that they end up in ascending order.
- Bubble sort algorithm:
	- point to two consecutive values in an array starting from the first two and compare them.
	- If the left value is larger than the one on the right, swap them. Otherwise, do nothing in this step.
	- Move the two pointers to the right.
	- Repeat the first three steps until we reach the end of the array.
	- We move the two pointers to their initial position and repeat steps 1 through 4 (pass through)
	- We keep doing pass throughs, until we reach a pass through in which no swaps take place. i.e. the array is already sorted.
- Example:

|4|5|7|9|3|
|---|---|---|---|---|
|&#8593|&#8593||||

|4|5|7|9|3|
|---|---|---|---|---|
||&#8593|&#8593|||

|4|5|7|9|3|
|---|---|---|---|---|
|||&#8593|&#8593||

|4|5|7|9|3|
|---|---|---|---|---|
||||&#8593|&#8593|

|4|5|7|3|9|
|---|---|---|---|---|
||||&#8593|&#8593|

We are done with the first passthrough, where the 9 is properly placed.

|4|5|7|3|9|
|---|---|---|---|---|
|&#8593|&#8593||||

|4|5|7|3|9|
|---|---|---|---|---|
||&#8593|&#8593|||

|4|5|7|3|9|
|---|---|---|---|---|
|||&#8593|&#8593||

|4|5|3|7|9|
|---|---|---|---|---|
|||&#8593|&#8593||

|4|5|3|7|9|
|---|---|---|---|---|
||||&#8593|&#8593|

We are done with the second pass through where the 7 is properly placed.

|4|5|3|7|9|
|---|---|---|---|---|
|&#8593|&#8593||||

|4|5|3|7|9|
|---|---|---|---|---|
||&#8593|&#8593|||

|4|3|5|7|9|
|---|---|---|---|---|
||&#8593|&#8593|||

|4|3|5|7|9|
|---|---|---|---|---|
|||&#8593|&#8593||


We are done with the third pass through where the 5 is properly placed.

|4|3|5|7|9|
|---|---|---|---|---|
|&#8593|&#8593||||

|3|4|5|7|9|
|---|---|---|---|---|
|&#8593|&#8593||||

The final pass through is done, where the 4 is properly placed, the array is now sorted.

```js

function bubbleSort(arr){
	let lastIndex = arr.length - 1;
	while !(sorted){
		let sorted = true
		for(let j=0; j<=lastIndex; j++){
			if(arr[j]<arr[j+1]){
				swap(arr[j], arr[j+1])
				sorted = false
			}
		}
		lastIndex = lastIndex-1;
		
	}
}
```


The Bubble sort has two significant types of steps:
- Comparisons: we iteratively keep comparing two consecutive numbers together to determine which one is greater.
- Swaps: two numbers are swapped with one another in order to sort them.

Let's see how many comparison steps, and how many swaps, are required for the bubble sort.

Comparison steps:
	- first pass through: N-1 comparisons 
	- second pass through: N-2 comparisons
	- third pass through: N-3 comparisons
Swap steps: In the worst case (descending order), we would require a swap for each comparison, which is (N-1)+(N-2)+(N-3)+(N-4)+.......+1 swaps.

Therefore, for an array of N values, we need:
	- (N-1)+(N-2)+(N-3)+(N-4)+.......+1 comparisons
	- (N-1)+(N-2)+(N-3)+(N-4)+.......+1 swaps
- In both cases, this series is evaluated to N*(N-1)/2. Which is 
O(N<sup>2</sup>).

![[Pasted image 20220806153131.png]]

The bubble sort is a quadratic algorithm solving a [[quadratic problem]].


## Quadratic Problem

Let's create a function that determines whether an array has duplicate values or not.


```js

function checkDuplicates(arr){
	for(let i=0; i<arr.length; i++){
		for(let j=0; j< arr.length;j++){
			if(i!=j && arr[i]==arr[j]){
				return true;
			}
		}
	}
	return false;

}
```

It works, but is it sufficient?  let's attempt to answer this with: 
1) Big O
For each iteration we are doing N comparisons, and we are doing N iterations, Therefore, the algorithm is O(N<sup>2</sup>).
2) Tracking the number of steps
```js

function checkDuplicates(arr){
	for(let i=0; i<arr.length; i++){
		for(let j=0; j< arr.length;j++){
			if(i!=j && arr[i]==arr[j]){
				steps++; // to track the number of steps
				return true;
			}
		}
	}
	return false;

}

```

Since our algorithm is O(N<sup>2</sup>), this should be a red flag, since O(N<sup>2</sup>) is considered inefficient, and we should look for faster alternatives.

Here is a linear solution to the same problem:
```js

function hasDuplicatesV2(arr){
	let existinNumbers=[];
	for(let i=0; i<=arr.length;i++){
		if(existingNumbers[arr[i]] === 1){
			return true;
		}
		else{
			existingNumbers[arr[i]] =1;
		}
	}
	return false;
	
}
```

In the new version of ```hasDuplicates``` We are iterating over the array arr, and each step doing a comparison, therefore given array arr of N elements, we'll do N comparisons, therefore, the algorithm is O(N<sup></sup>), or a linear algorithm. However, it should be noted that we've used another array ``existingNmber``  to track the elements we've seen in  `arr`, this means that although we have optimized for time complexity, we need more space for that. But for now we are focusing on time complexity, space complexity is a topic for another discussion.

In conclusion, using Big O to analyze the efficiency of a given algorithm has enabled us to look for more efficient alternatives, and we've consequently found a linear algorithm to look for duplicates instead of the quadratic algorithm we used earlier. 