## Insertion Sort

Although we've provided the rationale for considering the worst case scenario in our Big O calculation, because preparing for the worst case scenario would make sure we are in good shape. There are certain situations where considering all scenarios is an important skill.

We've encountered two sorting algorithms until now, the bubble sort and selection sort, both requiring O(N<sup>2</sup>) to run, selection sort being twice as fast.

Insertion sort consists of the following steps:
1)  In the first pass through, we remove the value at index 1 and put it in a temp variable. Then we start looking through the values to the left of the gap left by the value stored in the temp variable.
2) We begin the shifting phase, where for each value to the left of the gap, if that value is larger than the temp value we shift it to the right, which means the gap shifts to the left. We keep doing that until we encounter a value that is lower than the value in the temp that we are comparing to. Or if we reach the leftmost position of the array.
3) Once we reach that point, we insert the temp value in the gap.
4) We repeat steps 1 through 3, until the pass through begins at the final index of the array. Because by then the array would be sorted.


|4|5|7|9|3|
|---|---|---|---|---|
||&#8593 initial||||

|4|5|7|9|3|
|---|---|---|---|---|
|&#8593| initial||||

|4|5|7|9|3|
|---|---|---|---|---|
|||initial|||

|4|5|7|9|3|
|---|---|---|---|---|
||&#8593|initial|||

|4|5|7|9|3|
|---|---|---|---|---|
|&#8593||initial|||

|4|5|7|9|3|
|---|---|---|---|---|
||||initial||

|4|5|7|9|3|
|---|---|---|---|---|
|||&#8593|initial||

|4|5|7|9|3|
|---|---|---|---|---|
||&#8593||initial||

|4|5|7|9|3|
|---|---|---|---|---|
|&#8593|||initial||

|4|5|7|9|3|
|---|---|---|---|---|
|||||initial|

|4|5|7|9|3|
|---|---|---|---|---|
||||&#8593|initial|

Begin the shifting phase:

|4|5|7||9|
|---|---|---|---|---|
|||||initial|

|4|5||7|9|
|---|---|---|---|---|
|||||initial|

|4||5|7|9|
|---|---|---|---|---|
|||||initial|

| |4|5|7|9|
|---|---|---|---|---|
|||||initial|

We have reached the leftmost of the array while shifting, therefore, we insert the value in temp in the current gap, which is at index 0.

|3 |4|5|7|9|
|---|---|---|---|---|
|||||initial|

Insertion Sort in code:
```js
function insertionSort(arr){
  for(let i=1; i<arr.length; i++){
    let temp = arr[i];
    let j = i-1;
    while((j>=0)&&(arr[j]>temp)){
      if(arr[j]>temp){
        arr[j+1] = arr[j];
        j--;
      }
   
    }
    arr[j+1] = temp;
      console.log(arr);
    
  
}return arr;}

```


To analyze the efficiency of the insertion sort, we look at 4 kinds of steps being done during the algorithm's execution:
1) removal (putting the value in temp)
2) Comparisons (comparing the values to the left of the index of the value to be inserted) to the value to be inserted. 
3) Shifts (shifting the values larger than temp to the right)
4) Insertion (once we reach the location where the value is to be inserted, we insert it)

- Comparisons: comparisons take place each time we compare a value to the left of the gap to the temp value. The worst case scenario for comparisons, is to need to compare all the values to the left with temp value, this happens when the array is in reverse order. At the first pass through, we make one comparison which is the one element to the left of index 1, the second pass through we do two comparisons, etc., until the final pass through where the index is at the end of the array, then we do N-1 comparisons.
	- Therefore, in the worst case we have 1+2+3+4+5+6+...N-1 comparisons. Which, as we have observed earlier, evaluates to N(N-1)/2, which is O(N<sup>2</sup>/2).
- Shifts occur each time the element is larger than the temp value, in the worst case, i.e. when the array is in reverse order, shifts happen as much as comparisons, which is N(N-1)/2 times.
-  Shifts and comparisons are N(N-1)/2 + N(N-1)/2, which is N(N-1), and a total of O(N<sup>2</sup>)
- With respect to removal and insertion, in the worst case, there is at max one removal and one insertion at each pass through. Since we have N-1 pass through, then we have (N-1) removals, and N-1 insertions.
- Finally, we have N<sup>2</sup> comparisons and shifts, and we have N-1 removals, and N-1 insertions, leaving us with a total of N<sup>2</sup> + 2N  - 2 steps. Which is O(N<sup>2</sup> + N) after removing the constants. However, Big O has another rule. Which is:
- Big O only takes into account the highest order of N when we have multiple orders added together.
- Therefore, simplifying it down to the most dominant term, Insertion sort is also O(N<sup>2</sup>).
- Insertion sort takes O(N<sup>2</sup>/2) in the [[Average Case]]

## Average Case

created on: 2022-08-06 19:57

 Although selection sort is faster than insertion sort in the worst case scenario, we need to inspect the average case because it's the case that is most frequent, i.e. more likely to occur.
- Insertion sort in the best case (where the array is sorted) scenario would take one comparison each pass through and zero shifts.
- Insertion sort in the average case is the average between its best case and worst case, we can say that on aggregate we compare and shift half of the data, therefore, we can say that insertion sort takes about N<sup>2</sup> steps on the average scenario. 
- We conclude that the performance of insertion sort varies significantly based on the scenario. 
- ![[Pasted image 20220806195436.png]]
- selection sort on the other hand is O(N<sup>2</sup>/2) in all cases, because it has no mechanism to end a pass through early, it has to compare to all the values in a pass through.
- ![[Pasted image 20220806195607.png]]
- So, if we ask the question of which is better selection sort or insertion sort, it depends on the scenario we are encountering. If we suspect the arrays we are dealing with to be close to sorted, then insertion sort would be the better fit, while if we have a reason to believe that the arrays we are dealing with are going to be reversely sorted, then selection sort would be a better alternative, in the average case where we are not sure of the nature of the data we are operating on, there is no big difference between the two.

Example:
Finding the intersection between two arrays
```js
function findIntersection(arr1,arr2){
let intersection = [];
	for(let i =0; i<arr1.length; i++){
		for(let j=0; j<arr2.length; j++){
			if(arr1[i]===arr2[j]){
				result.push(arr1[i]);
			}
		}
	
	}
	
}
```

This is O(N<sup>2</sup>), in the worst case, the two arrays have no intersection, and therefore, for each element in `arr1` we would have to go through every element in `arr2` to look for an element in common. However, in the average case, there would be intersection between the two arrays. And therefore, the addition of a simple break after an element in common is found would reduce the number of steps required.

```js
function findIntersection(arr1, arr2){
	let result = [];
	for(let i=0; i< arr1.length; i++){
		for(let j=0; j< arr2.length; j++){
			if(arr[i]===arr[j]){
				result.push(arr[i]);
				break;
			}
		}	
	}

}

```

- Remember, while it's good to prepare for the worst case scenarios. Considering the average case is useful since it's the case that would occur most of the time.
