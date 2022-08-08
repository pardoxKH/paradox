Selection sort operates as follows:

1) Check each cell of the array from left to right to find the minimum value
2) Once the minimum value is found we swap it with the value we were at when we started the pass through
3) A pass through consists of finding the minimum value, and swapping it with the value at the index we started with. We repeat the pass through until we reach a pass through where we start at the end of the array, which means that we have sorted the array.


|4|5|7|9|3|
|---|---|---|---|---|
|&#8593 initial|||||

|4|5|7|9|3|
|---|---|---|---|---|
||&#8593||||

|4|5|7|9|3|
|---|---|---|---|---|
|||&#8593|||

|4|5|7|9|3|
|---|---|---|---|---|
||||&#8593||

|4|5|7|9|3|
|---|---|---|---|---|
|||||&#8593|

swap, and advance initial pointer:

|3|5|7|9|4|
|---|---|---|---|---|
||&#8593 initial||||

|3|5|7|9|4|
|---|---|---|---|---|
||&#8593||||

|3|5|7|9|4|
|---|---|---|---|---|
|||&#8593|||

|3|5|7|9|4|
|---|---|---|---|---|
||||&#8593||

|3|5|7|9|4|
|---|---|---|---|---|
|||||&#8593|

swap with initial, and advance initial:

|3|4|7|9|5|
|---|---|---|---|---|
|||&#8593 initial|||

|3|4|7|9|5|
|---|---|---|---|---|
||||&#8593||

|3|4|7|9|5|
|---|---|---|---|---|
|||||&#8593|

swap with initial and advance initial:

|3|4|5|9|7|
|---|---|---|---|---|
||||&#8593 initial||

|3|4|5|9|7|
|---|---|---|---|---|
|||||&#8593|

swap with initial and advance initial:

|3|4|5|7|9|
|---|---|---|---|---|
|||||&#8593 initial|

Initial has reached the end of the array, therefore, the array is sorted and the algorithm terminates.

Code implementation of selection sort:
```js
function selectionSort(arr){

	for(let i=0; i<arr.length-1; i++){
		let minIndex= i;
	    let minVal=arr[i];
		for(let j=i+1;j<arr.length; j++){
			if (arr[j]<minVal){
        minVal = arr[j];
				minIndex = j;
			}
		}
		if (minIndex!=i){
			let temp = arr[i];
			arr[i] = arr[minIndex];
			arr[minIndex] = temp;
		}
    console.log(arr)
	}
	return arr
} 
```

Let's investigate the efficiency of selection sort, similar to bubble sort, it has two types of steps: comparisons and swaps:

- Comparisons: each iteration, we are comparing the value at initial with all the values in the array. That is, in the first iteration we do N-1 comparisons, then N-2 comparisons, then N-3, etc. 
- Swaps: in each iteration we are either doing 1 swap, or no swaps at all. This depends on whether the minimum value is the one where initial is pointing at, or a new value that we found within the array. in the worst case scenario, we would do one swap each pass through, which is the case where the array is in reverse order.
- This means that in the worst case it costs us (N-1)+(N-2)+(N-3)+... comparisons, and 1+1+1+.... swaps, which is equivalent to N(N_1)/2 comparisons and N swaps. Which is O(N<sup>2</sup>)


if we go back to bubble sort, it takes N(N-1)/2 comparisons and N(N-1)/2 swaps to sort the array which is N(N-1).

Selection sort on the other hand, takes N(N-1)/2 comparisons and N swaps, which is N(N-1)/2 + N --->  O(N<sup>2</sup>/2) compared to bubble sort, which is P(N<sup>2</sup>). However, constants are irrelevant in Big O. Therefore, both algorithms have O(N<sup>2</sup>).

We drop constants in Big O because they become irrelevant and indicative of nothing for large inputs. Take for example O(100N) and O(N<sup>2</sup>), for small input sizes O(100N) is less efficient, specifically for N<100, but once the input size reaches 100 and beyond, a O(100N) algorithm is much more efficient than one of O(N<sup>2</sup>).

![[Pasted image 20220806174534.png]]

- Comparing O(100N) with O(N<sup>2</sup>), is like comparing an apartment building with a skycrapper, it's like saying this is a 10 story building and this is a 100 floor skycrapper, the number of floors is irrelavent if we are comparing two different building categories.