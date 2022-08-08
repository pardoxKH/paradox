## Why Algorithms?

An algorithm: a set of instructions to complete a specific task.

We've seen the effect of choosing a data structure on the performance of our code, even similar data structures such as arrays and sets differ in behavior in an operation like insertion for example.

Similarly, we will see that selecting a proper algorithm can have an effect on the efficiency of our code.  

## Ordered Arrays as a Data Structure
Ordered arrays are arrays where the order of elements is preserved. This fact would have an implication on two main operations carried out on sorted arrays, mainly insertion and search.

Similar to what we've done for arrays, and sets. To study a data structure, we need to investigate how the four main operations are affected by choosing such a data structure.

## Ordered Arrays Search

A superpower of ordered arrays is search.

If we take linear search as the searching algorithm of choice (that's what we have in our arsenal until now), and search for an element in an ordered array, it would have a drastically different performance compared to searching through a regular array.

If we are searching for the element 10 in the following regular array:

|9|5|7|4|
|---|---|---|---|

We would have to traverse every element in the array to ensure 10 doesn't exist in the array. That's N steps.

To search for element 10 in the ordered array:
|9|12|20|25|
|---|---|---|---|
It would take us 2 steps to determine that 10 doesn't exist in the array. Because in the first step we find 9, in the second we find 12, but since it's an ordered array, all the values to the right of 12 would be >= 12, but 10 < 12. Therefore, there is no way we would find 10 to the right of 12, so we stop our search costing us N/2 steps, that's half the number of steps required for searching a regular array.

Let's create a function that looks for an element in a given array.

```js
const linearSearch(arr, searchValue){
	for(let i=0; i< arr.length; i++){
		if (arr[i] == searchValue){
		return i;}
	}
	return null;
}
```
The previous function searches linearly through a regular array.  It's not adapted to search through an ordered array. Adapting the function to search an ordered array implies that we need a condition that checks if the element we are comparing with is larger than `searchValue`, in that case we know that the element doesn't exist in the array, and we can exit the function. After modifying it, it looks something like this.

```js
function linearSearchV2(arr, searchValue){
	for(let i=0; i<arr.length; i++){
		if (arr[i]==searchValue){
		return i;}
		else if (arr[i]>searchValue){
			//exit, because we don't to look further
			return null;
		}
		return null;
	}
}
```

The previous function searches linearly through a regular array.  It's not adapted to search through an ordered array. Adapting the function to search an ordered array implies that we need a condition that checks if the element we are comparing with is larger than `searchValue`, in that case we know that the element doesn't exist in the array, and we can exit the function. After modifying it, it looks something like this.

```js
​￼function linearSearchV2(arr, searchValue){
	​￼for(let i=0; i<arr.length; i++){
		if (arr[i]==searchValue){
		return i;}
		​￼else if (arr[i]>searchValue){
			//exit, because we don't to look further
			return null;
		}
		return null;
	}
}
```

In conclusion, searching through an ordered array can take less steps than searching through a regular array. But if the element we are looking for happens to be the last element of the array, then searching through an ordered array would take N steps, the same number of steps it takes to search through a regular array.

The big advantage and super power if ordered arrays is that they allow us to use a much faster searching algorithm to search through them. Namely, the [[Binary Search]] algorithm.

## Binary Search

If I asked you to guess a number that I have in my mind, it's between 1 and 100, and I will reply to your guesses with higher or lower. What's the first number you'd pick as your guess. Well, intuitively you'd pick 50, because it's right in the middle. If I told you higher, you've eliminated all the numbers less than 50, and if I tell you lower, you have eliminated half the numbers below 50. Let's say I tell you the number is lower than 50, now the problem becomes that you have to guess a number between 1 and 50, half the search space. So your second guess would be....25, again based on my answer, I am going to either eliminate all the numbers between 25 and 50. Or all the numbers between 1 and 25. This process can go on until the number we guess the number correctly. And it's much more efficient than random guesses. Because as we've seen, we are halving the search space at each step.

If I asked you to guess a number that I have in my mind, it's between 1 and 100, and I will reply to your guesses with higher or lower. What's the first number you'd pick as your guess. Well, intuitively you'd pick 50, because it's right in the middle. If I told you higher, you've eliminated all the numbers less than 50, and if I tell you lower, you have eliminated half the numbers below 50. Let's say I tell you the number is lower than 50, now the problem becomes that you have to guess a number between 1 and 50, half the search space. So your second guess would be....25, again based on my answer, I am going to either eliminate all the numbers between 25 and 50. Or all the numbers between 1 and 25. This process can go on until the number we guess the number correctly. And it's much more efficient than random guesses. Because as we've seen, we are halving the search space at each step.

This same logic applies to ordered arrays, we are looking for the value 10 for example in the ordered array:
|5|10|15|20|25|30|35|40|45|50|55|60|
|---|---|---|---|---|---|---|---|---|---|---|

We start by comparing with the element in the middle of the array:
|5|10|15|20|25|30|35|40|45|50|55|60|
|---|---|---|---|---|---|---|---|---|---|---|
||||||?||||

Is 10 higher or lower than 30, lower. Therefore, we eliminate the upper half of the array. And we don't need to look through it.
|5|10|15|20|25|30|35|40|45|50|55|60|
|---|---|---|---|---|---|---|---|---|---|---|
||||||x|x|x|x|x|x|

we are left with the elements 5, 10, 15, 20, 25 to look through, so once again we start with comparing with the element in the middle of those elements:
|5|10|15|20|25|30|35|40|45|50|55|60|
|---|---|---|---|---|---|---|---|---|---|---|
|||?|||x|x|x|x|x|x|

Is 10 lower or higher than 15, it's lower. So, we eliminate the upper part of the subarray:
|5|10|15|20|25|30|35|40|45|50|55|60|
|---|---|---|---|---|---|---|---|---|---|---|
|||x|x|x|x|x|x|x|x|x|

We do the same step again, comparing with the element in the middle of the subarray 5, 10. Since we have an even number of elements, we can choose arbitrarily either the element to the right or to the left of the middle, in our example, the index in the middle of 1, 2 is 0.5, then we can either take 0 or 1 to start comparing. If we take 0:
|5|10|15|20|25|30|35|40|45|50|55|60|
|---|---|---|---|---|---|---|---|---|---|---|
|?||x|x|x|x|x|x|x|x|x|

Is 10 lower or higher than 5, higher. Then, we eliminate 5, and we are left with one element, 10. 10 = 10 ? Yes, which is the value we are looking for.

It took us 4 steps to find the element we are looking for in an array of size 10, an operation that would take N steps if it was a linear search, and we were looking for an element at the end of the array. While, in binary search, it would also take us 4 steps to look for an element at the end of the array. Try it out! 

Binary search in code:
```js
const binarySearch(arr, searchValue){
	let lower = 0;
	let upper = array.length - 1;

	while(lower!<= upper){
		let mid = (lower+upper)/2;
		if (searchValue == arr[mid]){
			//the element is found
			return mid;	
		}
		else if (searchValue < mid){
			//we need to look in the lower half
			upper = mid - 1;
			
		
		}
		else{
			//we need to look in the upper half
			lower = mid +1; 
		}}
}
```

### Binary Search vs Linear search

The real difference in performance between binary search and linear search is significant for large arrays, with an array containing 100 values, the maximum number of steps required to look for a value is:
	- Linear Search: 100 steps
	- Binary Search: 7 steps

If we double the size of the array:
	- linear search would require additional steps equal to the number of added values to search for a value.
	- binary search would require one additional step to search for a required value.

The difference between the performance of the two becomes more drastic as the size of the array increases.
![[Pasted image 20220803150647.png]]

Reminder: 

Ordered Arrays aren't faster with respect to all operations, insertion for example in ordered array is slower than regular arrays. Therefore, by using an ordered array, we get a somewhat slower insertion, but a much faster search.

Upgraded insertion: since we have binary search in our toolkit now, and since insertion into ordered arrays requires search before inserting an element, we can upgrade the search to binary search. However, insertion into regular arrays is still faster as they don't require search at all.


## Ordered Arrays Insertion
- Insertion:

if we need to insert the value 6 into the following sorted array:

|4|5|7|9|
|---|---|---|---|

We can't directly append to the array as in the regular arrays case, because the ordering has to be preserved after the insertion, because it's an **ordered** array. Therefore, we would have to look for the proper location where the value 6 is going to be inserted.

|4|5|7|9|
|---|---|---|---|
|X|||

We first do the comparison: 6>4? 
6 is larger than 4, so 6 has to be placed to the right of 4

|4|5|7|9|
|---|---|---|---|
||X||

Then, we do the second comparison: 6>5?
6 is larger than 5, so 6 has to be placed to the right of 5

The third comparison would be with the 7:
|4|5|7|9|
|---|---|---|---|
|||X|

6 is less than 7, therefore, it would have to be inserted to the left of 7. 

To insert it to the left of 7, the 9 has to be shifted to the right (that's one step), and the 7 has to replace the 9 (that's two steps).

Finally, after 5 steps, we reach the following state:

|4|5||7|9|
|---|---|---|---|--|

Now, the location where 6 should be inserted is unoccupied, and it can be inserted (an additional step).

|4|5|6|7|9|
|---|---|---|---|--|

So it took us 6 steps to insert in a 4 element sorted array. Which is N+2 steps. In this case, they were N/2 + 1steps of comparison, N/2  steps for shifting, and 1 insertion step.

It turns out that the location where the element is going to be inserted doesn't affect the number of steps required, it just changes the distribution of the number of steps, between the steps required for shifting, and the steps required for comparison.

For example, if we are inserting at the end of the sorted array, we would need N comparison steps, 0 shifts, and 1 insertion step, N+1 steps. If we are inserting at the beginning of sorted array, it would require us one comparison, N shifts, and 1 insertion.

In conclusion, the insertion in sorted arrays takes N+1 steps in the best case, and N+2 steps in the worst case.
