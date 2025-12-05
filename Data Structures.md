## Best Time to Buy and Sell Stock - leetcode 121 :
	Trick : We are on an element, the best time to buy if we are seliing on the current element is the minimum element (0 to i-1) index, so just maintain a minimum element while solving and that's it

## Pushing Zero to the end:
	Trick: we can just start with 2 pointers with first pointer in the start and the second pointer in the end. The first pointer can can  move forward until 0 occurs, similarly end pointer can move back until it finds a number, then swap them  and continue until they pass each other

## Next Permutation:
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

## Subarray Sum K
	
	I’m at prefix j — use all _previous_ prefix sums to find matches,  
	then remember this prefix for future j’s.


## Finding the minimum element in a rotated array

WE know the property: if we divide by l,m,r then either of l,m or m,r  has to be sorted,
so use this property to find the minimum, 
store the minimum element of the sorted array (the first one), then skip the array as we dont need to see larget elements more, we got the minimum, just move forward with new and potentially small elements.

## 3 Sum Problem
	Sort the array, 
		loop i,
			if i>0 and nums[i] == nums[i-1]: continue  // dublicates
			
		 j<k while loop starts at i+1, k at end

			if sum i+j+k > 0 k--
			else sum < 0 j+=1
			else
				ans and then we need to ensure that:  we are not repeating numbers at j and k and so while loop so we escape that range.
				while j> k and nums[j] == nums[j-1] : j+=1
				and so for k

## Majority Element II
	The counters dont store the exact frequency count n/3, they just say about potential answers. 

	pseudo code:
		Cnt1,ele1,cnt2,ele2

		if cnt1== 0 and nums[i]!=ele2 # dont need double counting of same element
		Similarly,
		if cnt2== 0 and nums[i]!=ele1 # dont need double counting of same element
		All other cases

		Then a final loop to check if both ele, have count > n/3.






## Single element in twice repeating array (BS)
	if 0th index is not single, then the pattern is like, even and odd numbers till we have the single element, after that pattern shifts to odd even occurences.

so a binary search approach is that, when at mid, if mid-1 is also equal and see the indices, if mid-1 is lets say even and mid is odd, then its guranteed that the single element is in the right half of the array and vice versa.

## Merge Sorted array (no extra space : 2 approaches)

First:
	one pointer at the end of first array, 2nd pointer at the start of second array, now start comparing, i1+=1 and i2-=1, whereever nums1[i1] < nums2[i2], then previous elements would also satisfy as i1 goes towards decreasing value, whereas i2 towards increasing.
	So, we can stop here, sort the individual array to get both of them sorted.

Second:
	Gap Method: initial gap  = ceil (m+n/2) or  ((m+n) / 2) + (m+n)%2 works as ceil
	start a pointer at i at first array and another at i+gap. then start comparing if they can be swapped. when the right pointer reaches the end. 
	Then, do gap/2 with ceil and repeat again with updated gap. when gap == 1 stop, and we have the SORTED ARRAYS.




##  **Dijkstra explanation**

We do **not** use a visited array in Dijkstra because a node might be reached again with a smaller cost from a different path. Therefore, we rely on a `dist[][]` matrix: whenever we find a smaller cost, we push that state into the min-heap. The min-heap ensures we always expand the currently most promising (minimum-cost) state first, improving convergence.

## **BFS explanation**

In BFS, all edges have equal weight. BFS processes states level by level, so the first time we reach a node, we have already found its shortest path. Any later revisit would always come from a deeper level (greater distance), so it can never be optimal. That’s why BFS uses a visited array and doesn't reconsider nodes



