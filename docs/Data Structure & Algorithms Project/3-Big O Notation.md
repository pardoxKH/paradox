## Big O Notation 

We have concluded that what helps us determine the algorithm's performance is the number of steps an algorithm takes. However, it's impractical to say this algorithm takes 22 steps, and another takes 30 steps, etc. because the same algorithm can take a different number of steps based on the input it's operating on. Take linear search as an example, if we are searching through an array of 100 elements, then it's a 100-step algorithm, and if we are looking through an array of size 5, then we are looking at a 5-step algorithm.

A much more efficient way of quantifying the efficiency of an algorithm is to represent the number of steps an algorithm takes as a function of the input size. Therefore, linear search is an algorithm that takes N steps given an array of N elements.

### Definition
Big O is a formal mathematical notation used to quantify the efficiency of an algorithm, it's what the pros use instead of using mouthful statements.

Big O notation attempts to answer the following question: *Given N data elements, how many steps will the algorithm take?*

---
### Search

To elaborate: given N data elements, how many steps will the algorithm linear search take to search through the data, is equivalent to what is the big O of linear search?
In which we answer it's O(N)

### Read
Reading an element from the array is O(1), because this is the answer to the question: given an array of N elements, how many steps does it take to read an element. Well, one step. Therefore, reading is an operation that is dependent from the size of the array.

O(1) are the fastest algorithms in existence, they are algorithms independent of the size of the data structure it's operating on. It takes these algorithms a constant number of steps to operate on a 100 element array, and the same time to operate on a 1000,000 element array.

---

### Definition Revisited 

Big O actually doesn't answer the question: Given N elements, how many operations does an algorithm take?
It actually answers the questions, as the number of elements increase, how many operations does an algorithm take?

Given this new definition, an algorithm that takes 3 steps to operate on the data, and one that takes 1 step, are not actually different, because they both take a constant number of steps as the number of elements they operate on changes. Therefore, these are algorithms of constant Big O, and we denote both with O(1).

![[Pasted image 20220803154603.png]]


### Asymptotic Consideration
![[Pasted image 20220803154711.png]]


O(N) is considered a less efficient algorithm compared to O(1) no matter how many steps the O(1) algorithm actually takes. Because there will be a point where O(N) becomes less efficient than O(1).


## Binary Search in the Context of Big O

Binary search is clearly not O(1), because the number of steps increase as the data increases. It is also not O(N) because the number of steps required as the data size increase is not the same as that increment.  What is it then?

It is between O(1) and O(N).

It's O(log N), which is what we use to say that the algorithm takes one additional step as the data size doubles.

![[Pasted image 20220803160041.png]]

#### Mathematically

- Logarithms are the inverse of exponents
- O(log N) means that for N data elements, the algorithm would take log2(N) steps. Or, given N elements, it would take us log(N) steps of dividing the elements in half until we reach a single element.
![[Pasted image 20220803160427.png]]

The Big O depends on the scenario we are looking at, for example, linear search isn't always O(N). If the item we are looking for is at the end of the array it takes N steps, that's true. However, if the item is in the first cell of the array, then it'll take the search one step to find it, i.e. O(1).

This implies that there are different Big Os for the algorithm based on the scenario. Linear search is O(N) in the worst case scenario, and it's O(1) in the best case scenario.

Big O usually refers to the worst case scenario, because we want to be pessimistic in assessing the performance of our algorithm to prepare us for the worst case scenario.