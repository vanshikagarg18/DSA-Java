# Introduction to Merge Sort
Merge sort was invented by John von Neumann in 1945.
Merge sort is a sorting algorithm, based on divide and conquer technique or approach. As the name suggests, divide and conquer is a strategy of solving a large problem by :- 1) breaking the problem into smaller sub-problems,  2) solving the sub-problems, and   3) combining them to get the desired output.

It is a recursive algorithm and is one of the most popular and efficient sorting algorithm. It is a comparison-based sorting algorithm. 

There are 2 approaches to sort an array/list using merge sort-

1) Top-down approach :-

It starts from the top and works in the doemward way by splitting the array in half, making a recursive call, and merging the results until it reaches the bottom of the array to get the sorted array. This is the most common approach used forr merge sort.

<img width="343" alt="top down" src="https://github.com/vanshikagarg18/DSA-Java/assets/135498436/2946a006-357d-4c2b-b9d4-1f804c76b508">


2)  Botom-up approach :-

It starts with a single-element array and then merges two nearby items while sorting them. The combined-sorted arrays are merged and sorted again until only one single unit of the sorted array remains. It is an interative form.

<img width="274" alt="bottom up" src="https://github.com/vanshikagarg18/DSA-Java/assets/135498436/e0ec7916-0a98-4bba-842d-c2c44f3dab9d">

# Understanding the Merge Sort
Merge sort works as follows:

(i) Divide the unsorted array into n subarrays until it cannot be further divided, if the subarray containing one element then consider it as sorted.

(ii) Repeatedly merge subarrays to produce new sorted subarrays until the whole array gets sorted. This will be the final sorted array.

Algorithm - 
  ```
  Step 1 − If there is only one element in the array then it is already sorted, return.
  Step 2 − Divide the array recursively into two halves until it cannot be divided anymore.
  Step 3 − Merge the smaller subarrays into new arrays in sorted order on comparision basis until the main array gets sorted.
  ```
Let's consider an example by taking a small array with elements - [38,27,43,10]
<li>
  Step 1- Dividing the array into halves.
  
  The array contains 4 elements. Thus 4/2=2 subarrays will be formed initially, each containing 2 elements.
</li>
<li>
  Step 2- These 2 subarrays are further divided into two halves, each subarray will contain only 1 element (as there were 2 elements in the subarray). Now, these subarrays are of unit length and can no longer be divided.

  ** An array containing only 1 element is considered as already Sorted. **
</li>
<li>
  Step 3- These sorted subarrays of unit lengths are merged together in ascending order by comparing the elements to form bigger sorted subarrays.
</li>
<li>
  Step 4- Now, the sorted subarrays achieved as the final result of Step 3 will get merged together in ascending order on element comparison basis to form the final sorted array.

  The sorted array achieved in the last step is the sorted array of the provided array.
</li>

Further, the above sorting can be better undersood through the picture below- 

<img width="242" alt="Merge Sort example" src="https://github.com/vanshikagarg18/DSA-Java/assets/135498436/2f87f665-ba55-43d5-8e60-3c5e35836b48">

# Implementation and illustration of Merge Sort
While implementing merge sort two functions are used : 

A mergeSort function takes the input array. This will be a recursive function, thus the base and the recursive conditions are required. The base condition checks if the array length is 1 and it will just return. For the rest of the cases, the recursive call will be executed. 
  ```
  public static void mergeSort(int[] a, int n) {
    if (n < 2) {
        return;
    }
    int mid = n / 2;
    int[] l = new int[mid];
    int[] r = new int[n - mid];

    for (int i = 0; i < mid; i++) {
        l[i] = a[i];
    }
    for (int i = mid; i < n; i++) {
        r[i - mid] = a[i];
    }
    mergeSort(l, mid);
    mergeSort(r, n - mid);

    merge(a, l, r, mid, n - mid);
}
  ```
The merge function, which takes the input and the subarrays, as well as the start and end indices of the subarrays. The merge function compares the elements of the subarrays one by one. Thereby giving us the final sorted array
 ```
public static void merge(
  int[] a, int[] l, int[] r, int left, int right) {
 
    int i = 0, j = 0, k = 0;
    while (i < left && j < right) {
        if (l[i] <= r[j]) {
            a[k++] = l[i++];
        }
        else {
            a[k++] = r[j++];
        }
    }
    while (i < left) {
        a[k++] = l[i++];
    }
    while (j < right) {
        a[k++] = r[j++];
    }
}
 ```
Illustation of merge sort -

Let's take the previous example of Merge Sort and look for its step-wise implementation. Consider a small array with elements - [38,27,43,10]

Step 1 - Divide the array into two equal halves: 
  
  <img width="407" alt="Step 1" src="https://github.com/vanshikagarg18/DSA-Java/assets/135498436/3a7391f8-c74c-438c-8de3-8c7f940a9937">

Step 2 - Divide the subarrays further in two halves. Now, they become array of unit length and can no longer be divided.

  <img width="430" alt="Step 2" src="https://github.com/vanshikagarg18/DSA-Java/assets/135498436/d9417b67-fb29-42d0-a7c4-5e20fb764d0e">

Step 3 - The array of unit length is always sorted. Thus, these sorted subarrays are merged together by comparing the elements to form a bigger sorted subarray.

   <img width="443" alt="Step 3" src="https://github.com/vanshikagarg18/DSA-Java/assets/135498436/f273cadc-aa3a-4e0b-938d-da2c3b9edae8">

Step 4 - The comparing and merging process is continued until the sorted array is formed from the sorted subarrays.

  <img width="312" alt="Step 5" src="https://github.com/vanshikagarg18/DSA-Java/assets/135498436/c1116d70-e571-49a7-a304-3dfa7ef18801">

The sorted array obtained is the final sorted array.
# Merge Sort Code
 ```
import java.io.*;

public class MergeSort {
    
	void merge(int arr[], int l, int m, int r)
	{
		int n1 = m - l + 1;
		int n2 = r - m;
		int L[] = new int[n1];
		int R[] = new int[n2];

		for (int i = 0; i < n1; ++i)
			L[i] = arr[l + i];
		for (int j = 0; j < n2; ++j)
			R[j] = arr[m + 1 + j];

		int i = 0, j = 0;
		int k = l;
		while (i < n1 && j < n2) {
			if (L[i] <= R[j]) {
				arr[k] = L[i];
				i++;
			}
			else {
				arr[k] = R[j];
				j++;
			}
      k++;
		}
		while (i < n1) {
			arr[k] = L[i];
			i++;
			k++;
		}
		while (j < n2) {
			arr[k] = R[j];
			j++;
			k++;
		}
	}
	void mergeSort(int arr[], int l, int r)
	{
		if (l < r) {
			int m = l + (r - l) / 2;

			mergeSort(arr, l, m);
			mergeSort(arr, m + 1, r);
			merge(arr, l, m, r);
		}
	}
	static void printArray(int arr[])
	{
		int n = arr.length;
		for (int i = 0; i < n; ++i)
			System.out.print(arr[i] + " ");
		System.out.println();
	}
	public static void main(String args[])
	{
		int arr[] = { 12, 11, 13, 5, 6, 7 };

		System.out.println("Given array: ");
		printArray(arr);

		MergeSort ob = new MergeSort();
		ob.mergeSort(arr, 0, arr.length - 1);

		System.out.println("\nSorted array: ");
		printArray(arr);
	}
}
 ```
# Complexity analysis 
1) Time Complexity -

Merge Sort is a recursive algorithm and its time complexity can be expressed as following recurrence relation - 

T(n) = 2T(n/2) + θ(n)

-> 2T(n/2) corresponds to the time required to sort the sub-arrays, and O(n) is the time to merge the entire array. 

<li>Best Case Time Complexity - It occurs when there is no sorting required, i.e. the array is already sorted. The best-case time complexity of merge sort is O(n*logn).</li>
<li>Average Case Time Complexity - It occurs when the array elements are in jumbled order that is not properly ascending and not properly descending. The average case time complexity of merge sort is O(n*logn).</li>
<li>Worst Case Time Complexity - It occurs when the array elements are required to be sorted in reverse order. That means suppose you have to sort the array elements in ascending order, but its elements are in descending order. The worst-case time complexity of merge sort is O(n*logn).</li>

-> TIME COMPLEXITY OF MERGE SORT :- Best Case = Worst Case =Average Case: "O(n*logn)"

2) Space Complexity

The Space complexity of merge sort is O(n). It is because, In merge sort all elements are copied into an auxiliary array so n auxiliary space is required for merge sort or it can be concluded that an extra variable n is required for swapping the elements of an array.

# Stability
Merge sort is a stable sorting algorithm. This means that if an array has  two same elements, then their relative positions will be the same in the sorted output array.

If two elements are equal, then the merge sort copies the element from the left half to the output array first. This ensures that the relative positions of equal elements in the input array are preserved in the sorted output array.

For example:

Input array: [5, 3, 2, 1, 4, 5]
Output array: [1, 2, 3, 4, 5, 5]

The elements with the equal value 5 have the same positions in the sorted output array.
# Applications
Merge sort is a versatile sorting algorithm, used in a wide range of applications. It is a good choice for sorting algorithms as it is efficient, stable, and easy to implement.

<li>Sorting linked lists: Merge sort is a good algorithm for sorting linked lists because it does not require random access to the elements of the list.</li>
<li>Counting inversions: Merge sort can be used to efficiently count the number of inversions in an array. An inversion is a pair of elements in an array where the first element is greater than the second element.</li>
<li>External sorting: Merge sort can be used to sort large datasets that are too large to fit in memory, known as external sorting.</li>
<li>Search engines: Merge sort is used by search engines to sort the results of a search query. This ensures that the most relevant results are displayed first.</li>
<li>Databases: Merge sort is used by database management systems to sort data in tables. This makes it easier and faster to find the data that you need.</li>
<li>Compilers: Merge sort is used by compilers to sort the tokens of a program before parsing it. This helps to improve the efficiency of the compiler.</li>
<li>Operating systems: Merge sort is used by operating systems to sort files and directories. This makes it easier to find the files and directories that you need.</li>
