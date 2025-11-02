Best Time to Buy and Sell Stock - leetcode 121 :
	Trick : We are on an element, the best time to buy if we are seliing on the current element is the minimum element (0 to i-1) index, so just maintain a minimum element while solving and that's it

Pushing Zero to the end:
	Trick: we can just start with 2 pointers with first pointer in the start and the second pointer in the end. The first pointer can can  move forward until 0 occurs, similarly end pointer can move back until it finds a number, then swap them  and continue until they pass each other

Next Permutation:
	How to approach:

		We have to find out the next permutation. that means the next number in the dictionary order of all permutations

	Or, We have to find the next closest number in dict order
	and so, it should have the LONGEST COMMON PREFIX, then we can tweak the next elements and create a number from it
	
	Consider 51430
	
	here if we take prefic 514, then out of the rest 30, we cant create a bigger number so move on
	for 51, still we cant create a bigger or next number than 430, so move on again
	
	for 5, we can actually create a bigger number as we got 1430, (index is 1 / pivot) (so arr[i] <arr [i+1])
	
	if we cant find a pivot that means we are at the last permutation, now, so just return the 1st permuation or reverse the current array
	
	as we went from right end, just find a number that is greater than pivot , that way its just bigger/ next number for pivot.
	
	swap it with index, so we got 53410 now, and we got to have the lowest number order after 53. That way its the smallest number in bigger than current permutation  / NEXT PERMUTATION.
	
	reverse the array after index now,
	
	Finally we got 53014, which is the next permutation

Subarray Sum K
	
	I’m at prefix j — use all _previous_ prefix sums to find matches,  
	then remember this prefix for future j’s.


## Finding the minimum element in a rotated array

WE know the property: if we divide by l,m,r then either of l,m or m,r  has to be sorted,
so use this property to find the minimum, 
store the minimum element of the sorted array (the first one), then skip the array as we dont need to see larget elements more, we got the minimum, just move forward with new and potentially small elements.



>		
>