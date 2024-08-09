# Data-Structure-Arrays

What are arrays: Arrays in Java are dynamically created objects. Because Java arrays are objects, they are created using new operator. The size of a Java array object is fixed at the time of its creation that cannot be changed later throughout the scope of the object. When an object is created in Java by using new operator the identifier holds the reference not the object exactly.

======
Can array store an array: An element of an array can be an array. If the element type is Object or Cloneable or java.io.Serializable, then some or all of the elements may be arrays, because any array object can be assigned to any variable of these types. Java allows creating arrays of abstract class types. Elements of such an array can either be null or instances of any subclass that is not itself abstract.

======
Is array of size 0 is allowed? Negative size array possible: Java allows creating an array of size zero. If the number of elements in a Java array is zero, the array is said to be empty. In this case you will not be able to store any element in the array. You can also create an array of negative size. Your program will be successfully compiled by the compiler with a negative array size, but when you run this program it will throw java.lang.NegativeArraySizeException exception.

======
Reference variables: as the name implies, creates a copy of a reference variable pointing to an object. If we have a Car object, with a myCar variable pointing to it and we make a reference copy, we will now have two myCar variables, but still one object.

======
Object copying: An object copy creates a copy of the object itself. So if we again copied our car object, we would create a copy of the object itself, as well as a second reference variable referencing that copied object.

======
SHALLOW COPY: shallow copy of an object copies the ‘main’ object, but doesn’t copy the inner objects. The ‘inner objects’ are shared between the original object and its copy. For example, in our Person object, we would create a second Person, but both objects would share the same Name and Address objects. The problem with the shallow copy is that the two objects are not independent. If you modify the Name object of one Person, the change will be reflected in the other Person object.

======
A deep copy is a fully independent copy of an object. If we copied our Person object, we would copy the entire object structure. A change in the Address object of one Person wouldn’t be reflected in the other object. To create a true deep copy, we need to keep copying all of the Person object’s nested elements, until there are only primitive types and “Immutables” left. Just because a deep copy will let you change the internal details of an object, such as the Address object, it doesn’t mean that you should. Doing so would decrease code quality, as it would make the Person class more fragile to changes – whenever the Address class is changed, you will have to (potentially) apply changes to the Person class also.

======
Cloning is also a way of creating an object, but in general, cloning is not just about creating a new object. Cloning means creating a new object from an already present object and copying all data of the given object to that new object. In order to create a clone of an object, we generally design our class in such way that:
1) Our class should implement the Cloneable interface. Otherwise, the JVM will throw CloneNotSupportedException if we will call clone() on our object.
2) Our class should have a clone method, which should handle CloneNotSupportedException.
3) And finally, we need to call the clone() method of the superclass, which will call its super clone(). This chain will continue until it reaches the clone() method of the Object class. The Object.clone() method is the actual worker that creates the clone of your object, and another clone() method just delegates the call to its parent’s clone(). It is not necessary to define our method by the name of clone. We can give it any name we want, e.g. createCopy(). Actually we are not overriding the Object.clone() method here, so we don’t have to follow any specification. Object.clone() is protected by its definition, so, practically, child classes of Object outside the package of the Object class (java.lang) can only access it through inheritance and within itself. (person1 == person2) will evaluate false because person1 and person2 are copies of each other, but both are different objects and hold different spots in heap memory. Meanwhile, person1.equals(person2) evaluates true because both have the same content.Class should implement Cloneable
public Person clone() throws CloneNotSupportedException {
        Person clonedObj = (Person) super.clone();
        clonedObj.city = this.city.clone();
        return clonedObj;
}
And super.clone() will call its super.clone() and the chain will continue until the call reaches the clone() method of the Object class, which will create a field copy of our object and return it back.

======
What is ArrayStoreException in java? When you will get this exception? ArrayStoreException is a run time exception which occurs when you try to store non-compatible element in an array object.
public class MainClass{
    public static void main(String[] args) {
        Object[] stringArray = new String[5];   //No compile time error : String[] is auto-upcasted to Object[]
        stringArray[1] = "JAVA";     
        stringArray[2] = 100;     //No compile time error, but this statement will throw java.lang.ArrayStoreException at run time
        //because we are inserting integer element into an array of strings
    }
}
You cannot store an String in an array of primitive int, it will result in compile time error, but if you create an array of Object and assign String[] to it and then try to store Integer object on it. Compiler won't be able to detect that and it will throw ArrayStoreExcpetion at runtime.

======
What is an anonymous array? Give example?
public class MainClass{
    public static void main(String[] args){
        //Creating anonymous arrays
        System.out.println(new int[]{1, 2, 3, 4, 5}.length);    //Output : 5
        System.out.println(new int[]{21, 14, 65, 24, 21}[1]);   //Output : 14
    }
}

======
What are the differences between Array and ArrayList in java? Arrays are of fixed length. ArrayList is of variable length. You can’t change the size of the array once you create it. Size of the ArrayList grows and shrinks as you add or remove the elements. Array does not support generics. ArrayList supports generics. You can use arrays to store both primitive types as well as reference types. You can store only reference types in an ArrayList.

======
What are jagged arrays in java? Jagged arrays in java are the arrays containing arrays of different length. Jagged arrays are also multidimensional arrays.

======
There are 2 int type array data type. One is containing 50 elements, and another one is containing 30 elements. Can we assign the array of 50 elements to an array of 30 elements? Yes we can assign provided they should the same type. The compiler will check the only type of the array, not the size.

======
How do we search a specific element in an array? We can use Arrays.binarySearch() method. This method uses binary search algorithm.

======
Can we make array volatile in Java? Yes, we can make an array volatile in Java, but we only make the variable which is pointing to array volatile.

======
Program to cyclically rotate an array by one: Store last element in a variable say x. Shift all elements one position ahead. Replace first element of array with x.

======
Find the minimum element in a sorted and rotated array
- Traverse the complete array and find minimum. This solution requires O(n) time.
- O(Logn) using Binary Search. The minimum element is the only element whose previous is greater than it. If there is no previous element, then there is no rotation (first element is minimum). We check this condition for middle element by comparing it with (mid-1)’th and (mid+1)’th elements. If minimum element is not at middle (neither mid nor mid + 1), then minimum element lies in either left half or right half. If middle element is smaller than last element, then the minimum element lies in left half. Else minimum element lies in right half.

========
Maximum sum of i*arr[i] among all rotations of a given array
- A simple solution is to try all possible rotations. Compute sum of i*arr[i] for every rotation and return maximum sum. Naive Solution : O(n2) 
- The idea is to compute value of a rotation using value of previous rotation. When we rotate an array by one, following changes happen in sum of i*arr[i]. 1) Multiplier of arr[i-1] changes from 0 to n-1, i.e., arr[i-1] * (n-1) is added to current value. 2) Multipliers of other terms is decremented by 1. i.e., (cum_sum – arr[i-1]) is subtracted from current value where cum_sum is sum of all numbers. Efficient Solution : O(n)

======	
Move all negative elements to end in order with extra space allowed
- Idea is create an empty array (temp[]). First we store all positive element of given array and then we store all negative element of array in Temp[]. Finally we copy temp[] to original array.

======
Segregate positive and negative numbers
- Here we use some part of quick sort. Here 0 is the pivot element. Negative on left and Positive on right. i at the start and j at the end. Increment i if i is less than 0 and j if greater than 0. if both not met then we swap and we repeat.
	
======
Replace every element with the greatest element on right side. For array {16, 17, 4, 3, 5, 2}, answer is {17, 5, 5, 5, 2, -1}.
- A naive method is to run two loops. The outer loop will one by one pick array elements from left to right. The inner loop will find the greatest element present after the picked element. Finally the outer loop will replace the picked element with the greatest element found by inner loop. The time complexity of this method will be O(n*n).
- A tricky method is to replace all elements using one traversal of the array. The idea is to start from the rightmost element, move to the left side one by one, and keep track of the maximum element. Replace every element with the maximum element.

======	
Segregate 0s and 1s in an array
- Count the number of 0s and put the 0s and rest as 1
- Maintain two indexes. Initialize first index left as 0 and second index right as n-1. Do following while left < right. Keep incrementing index left while there are 0s at it. Keep decrementing index right while there are 1s at it. If left < right then exchange arr[left] and arr[right]

======
Find Index of 0 to be replaced with 1 to get longest continuous sequence of 1s in a binary. arr[] =  {1, 1, 0, 0, 1, 0, 1, 1, 1, 0, 1, 1, 1}
- A Simple Solution is to traverse the array, for every 0, count the number of 1s on both sides of it. Keep track of maximum count for any 0. Finally return index of the 0 with maximum number of 1s around it. The time complexity of this solution is O(n2).
- Using an Efficient Solution, the problem can solved in O(n) time. The idea is to keep track of three indexes, current index (curr), previous zero index (prev_zero) and previous to previous zero index (prev_prev_zero). Traverse the array, if current element is 0, calculate the difference between curr and prev_prev_zero (This difference minus one is the number of 1s around the prev_zero). If the difference between curr and prev_prev_zero is more than maximum so far, then update the maximum. Finally return index of the prev_zero with maximum difference.

======	
Program for array rotation. Input arr[] = [1, 2, 3, 4, 5, 6, 7], d = 2, n =7
- Use temp array
- Rotate one by one
- Juggling Algorithm: Instead of moving one by one, divide the array in different sets where number of sets is equal to GCD of n and d and move the elements within sets. If GCD is 1 as is for the above example array (n = 7 and d =2), then elements will be moved within one set only, we just start with temp = arr[0] and keep moving arr[I+d] to arr[I] and finally store temp at the right place.
- Reversal algorithm: Let AB are the two parts of the input array where A = arr[0..d-1] and B = arr[d..n-1]. The idea of the algorithm is:
Reverse A to get ArB. /* Ar is reverse of A */
Reverse B to get ArBr. /* Br is reverse of B */
Reverse all to get (ArBr) r = BA.
For arr[] = [1, 2, 3, 4, 5, 6, 7], d =2 and n = 7
A = [1, 2] and B = [3, 4, 5, 6, 7]
Reverse A, we get ArB = [2, 1, 3, 4, 5, 6, 7]
Reverse B, we get ArBr = [2, 1, 7, 6, 5, 4, 3]
Reverse all, we get (ArBr)r = [3, 4, 5, 6, 7, 1, 2]

======
Dutch National Flag Problem: Sort an array of 0s, 1s and 2s. Input :  {0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1}: We will have three variables one is pointing to the start, one to the end and another which traverse throughout the list. We will have the following checkwhile (mid <= hi){
    switch (a[mid]){
    case 0:
        swap(&a[lox`++], &a[mid++]);
        break;
    case 1:
        mid++;
        break;
    case 2:
        swap(&a[mid], &a[hi--]);
        break;
    }
}

======
Find the missing number in an array having duplicates and below the largest index of the array
- n*(n+1)/2 - sum of all the numbers in array = missing number
- XOR the XOR of the all the numbers till n and XOR of the numbers present in the array : Note it will not work in case of duplicates
- create a separate array ans start marking the index of the array as -1 or visited.
- Sort and linearly check

======	
Find the two missing numbers : Given an array of n unique integers where each element in the array is in range [1, n]. The array has all distinct elements and size of array is (n-2). Hence Two numbers from the range are missing from this array. Find the two missing numbers.
- O(n) time complexity and O(n) Extra Space. Take a boolean array mark that keeps track of all the elements present in the array.
- O(n) time complexity and O(1) Extra Space. 
Input : 1 3 5 6, n = 6
Sum of missing integers = n*(n+1)/2 - (1+3+5+6) = 6.
Average of missing integers = 6/2 = 3.
Sum of array elements less than or equal to average = 1 + 3 = 4. Sum of natural numbers from 1 to avg = avg*(avg + 1)/2 = 3*4/2 = 6
First missing number = 6 - 4 = 2
Sum of natural numbers from avg+1 to n  =  n*(n+1)/2 - avg*(avg+1)/2  =  6*7/2 - 3*4/2  =  15
Sum of array elements greater than average = 5 + 6 = 11	Second missing number = 15 - 11 = 4
- Find XOR of all array elements and natural numbers from 1 to n. Let the array be arr[] = {1, 3, 5, 6}. XOR = (1 ^ 3  ^ 5 ^ 6) ^ (1 ^ 2 ^ 3 ^ 4 ^ 5 ^ 6). As per the property of XOR, same elements will cancel out and we will be left with 2 XOR 4 = 6 (110). But we don’t know the exact numbers,let them be X and Y. A bit is set in xor only if corresponding bits in X and Y are different. This is the crucial step to understand. We take a set bit in XOR. Let us consider the rightmost set bit in XOR, set_bit_no = 010. Now again if we XOR all the elements of arr[] and 1 to n that have rightmost bit set we will get one of the repeating numbers, say x. Ex: Elements in arr[] with bit set: {3, 6}. Elements from 1 to n with bit set {2, 3, 6}. Result of XOR'ing all these is x = 2. Similarly, if we XOR all the elements of arr[] and 1 to n that have rightmost bit not set, we will get the other element, say y. Ex: Elements in arr[] with bit not set: {1, 5}. Elements from 1 to n with bit not set {1, 4, 5}. Result of XOR'ing all these is y = 4
	
======
Find duplicates in O(n)time and O(1) extra space of a given array of n elements which contains elements from 0 to n-1, with any if these numbers appearing any number of time {1,2,3,1,3,6,6}
- We will change the sign of the value at the index which is present at the index starting from 0. If that number again comes and value at the index is already negative then it is repeating.
- Go to index arr[i]%n and increment the value by n. Now traverse the array again and print all those indexes i for which arr[i]/n is greater than 1
	
======
Find the next greater element in an array. 5,3,2,10,6,8,1,4,12,7,4  -> 10,10,10,12,8,12,4,12,no,no,no
- We have to use stack. We keep putting the value into the stack until the value becomes more than the value present in the stack or till the stack is empty. At the end add that value. put 5. put 3. put 2. now 10 is greater then 2, so 10 is greater value of 2, 3, 5 and then 10 is put into the stack. put 6. then 8 is greater then 6. 8 is greater value for 6. put 8. put 1, put 4, now 12 is greater and greater value for 1,8,10

======
Heap Sort: There is an array of integers and are made it into the tree in sequential order 8,7,9,10,3,4,1,12,6,5
	8							     1
   / \							 3       4
  7   9      =>        		   6  5     8  9	  
 / \ / \					12  10  7
10 3 4  1
/\ \
12  6 5      
We take one by one the level starting from number 10 and set the node with minimum value of the three i.e. 10,12,6 and swap the 6 and 10. Keep doing until we get the min heap. Min heap is when all the nodes are less than their children node. As it is the mean heap the root node is always the lowest number. Remove the 1 and replace it with the last element i.e. last level last element i.e. 7. Now make this tree as min heap again. Which will give the root node as minimum again. Keep doing this, you will get sorted array. 

======
Majority of the array: When an element has occurrence greater than n/2 then the element is called majority of the array. 
- Use hash table for counting.
- sort the array and then check at i + n/2 position. If the same element is present at that position means it is majority element

======
Find the leader in an array: For a leader L, all the elements on the right side of L are less then L.
array {16, 17, 4, 3, 5, 2}, leaders are 17, 5 and 2.
- Generic solution, for each item check each right value that it is less than the value of item.
- Start from right, and check the maximum value till it reach another maximum value.

======
Find the pairs with given sum in an array
- Sort the array with merge sort. Start one variable from left and another from right sum it if the sum is more than required then move right variable to left. If sum is less then shift the left value by one position.
- Keep putting the values in the hasMap and then while comparing in next interaction find the value subtracted from desired result.

======
Find the number occurring odd number of times
- simple solution is to use two loops to count number of times the number is being repeated
- There is only one number in the array which occurs only one odd number of times. We can use XOR over here. All the items which are even time cancel out and only one item which is odd time 

======
Search an element in an sorted matrix. Where all the rows and columns are sorted
Input : mat[4][4] = { {10, 20, 30, 40},
                      {15, 25, 35, 45},
                      {27, 29, 37, 48},
                      {32, 33, 39, 50}};              x = 29
Output : Found at (2, 1). Go to the end of the first row (last column) and compare. If it is less than that value then go to column less than the selected column. Basically if value at matrix is less than element, go to previous column, if matrix value is greater than element, go to next row.

======
Print matrix in spiral form. Input:
        1    2   3   4
        5    6   7   8
        9   10  11  12
        13  14  15  16
Output: 1 2 3 4 8 12 16 15 14 13 9 5 6 7 11 10
- Take four variables and then keep decrementing the last row and last column and incrementing the first row and first column as you keep passing on. Do put check of if last column should not be equal to first column and vice versa for row.

========
** Largest subarray with equal number of 0s and 1s
- A simple method is to use two nested loops. The outer loop picks a starting point i. The inner loop considers all subarray starting from i. If size of a subarray is greater than maximum size so far, then update the maximum size.
- change the 0 to -1. Create a temporary array sumleft[] of size n. Store the sum of all elements from arr[0] to arr[i] in sumleft[i]. This can be done in O(n) time. There are two cases, the output subarray may start from 0th index or may start from some other index. We will return the max of the values obtained by two cases. To find the maximum length subarray starting from 0th index, scan the sumleft[] and find the maximum i where sumleft[i] = 0. Now, we need to find the subarray where subarray sum is 0 and start index is not 0. This problem is equivalent to finding two indexes i & j in sumleft[] such that sumleft[i] = sumleft[j] and j-i is maximum. To solve this, we can create a hash table with size = max-min+1 where min is the minimum value in the sumleft[] and max is the maximum value in the sumleft[]. The idea is to hash the leftmost occurrences of all different values in sumleft[]. The size of hash is chosen as max-min+1 because there can be these many different possible values in sumleft[]. Initialize all values in hash as -1. To fill and use hash[], traverse sumleft[] from 0 to n-1. If a value is not present in hash[], then store its index in hash. If the value is present, then calculate the difference of current index of sumleft[] and previously stored value in hash[]. If this difference is more than maxsize, then update the maxsize. To handle corner cases (all 1s and all 0s), we initialize maxsize as -1. If the maxsize remains -1, then print there is no such subarray

========
Is there any subarray with 0 sum. Input: {4, 2, -3, 1, 6}
- find all the subarrays and check their sum.
- Use hashing. We take the sum till each index from starting i.e. from arr[0] to arr[i] and put them in hash. While putting we will check if the same sum value is already present in the HashMap. If yes it means there is a subarray having the sum as 0.
arr[]=      {1, 4, -2, -2, 5, -4, 3}
sumArray[] ={1, 5,  3,  1, 6,  2, 5} Here there are two subarrays: in sumArray 1<->1 and 5<->5

========
Finding all subarrays of an array. It is not same as finding all the permutations of an array: There will be two loops. One is the starting point and another is number of items to be selected in that sub array.
arr[] = {1, 2, 3, 4}. Output: 1, 12, 123, 1234, 2, 23, 234, 3, 34, 4

========
Find subarray with given sum : Numbers non negative, Input: arr[] = {1, 4, 20, 3, 10, 5}, sum = 33
- Find all the subarrays of an array and find their sum. 
- sort the array. Keep adding the numbers and if increases than the required numbers than start subtracting from starting until it becomes equal or less than the desired number

========
First non repeating char in a string
- There are 256 char. Create an array. Increment the value of array at that ASCII value of char. Now again loop the string and check which char position in the array has value 1.
- Now in place of looping again the string, it is better to loop only the char array. There may be a long string having only 4 char like DNA and the value that is unique may be at the end only. So why to loop again. So in place of saving number of times the char is present in the array, we save the position of the first occurrence of the char. and if found again just update it to -2. By default initialize this array to -1.

========
Remove duplicates from unsorted array
- Take hashMap. Traverse the array and check if the value is present in the hashMap. If present then continue otherwise insert and print that value.
- sort the array
- using sets

========
There is an array with every element repeated twice except one. Find that element?
- XOR all elements

========
K’th Smallest/Largest Element in Unsorted Array 
- Sort the array and find the desired element in O(nlogn)
- Using minheap : Create a min heap and call extractMin k times. O(n + kLogn).

========
Minimum swaps required to bring all elements less than or equal to k together
Input:  arr[] = {2, 1, 5, 6, 3}, k = 3. Output: 1
- A simple solution is to first count all elements less than or equals to k(say ‘good’). Now traverse for every sub-array and swap those elements whose value is greater than k. Time complexity of this approach is O(n2)
- Find count of all elements which are less than or equals to ‘k’. Let’s say the count is ‘cnt’. Using two pointer technique for window of length ‘cnt’, each time keep track of how many elements in this range are greater than ‘k’. Let’s say the total count is ‘bad’. Repeat step 2, for every window of length ‘cnt’ and take minimum of count ‘bad’ among them. This will be the final answer.

=========
Find all triplets with zero sum: 
- O(n3). The naive approach is that run three loops and check one by one that sum of three elements is zero or not if sum of three elements is zero then print elements other wise print not found.
- O(n2): Hashing. We iterate through every element. For every element arr[i], we find a pair with sum “-arr[i]”. This problem reduces to pairs sum and can be solved in O(n) time using hashing.
- O(n2): Sorting: Sort the input array. Fix the first element as A[i] where i is from 0 to array size – 2. After fixing the first element of triplet, find the other two elements using method 1 of this post.

========
Find the smallest missing number. Given a sorted array of n distinct integers where each integer is in the range from 0 to m-1 and m > n. Find the smallest number that is missing from the array. Input: {0, 1, 2, 6, 9}, n = 5, m = 10, Output: 3
- Method 1 (Use Binary Search) O(m log n)
- Method 2 (Linear Search) O(n)

=========
STRINGS
=========
Is String a keyword in java: No. String is not a keyword in java. String is a final class in java.lang package which is used to represent the set of characters in java.

======
Is String a primitive type or derived type: String is a derived type.

======
In how many ways you can create string objects in java: There are two ways to create string objects in java. One is using new operator and another one is using string literals. The objects created using new operator are stored in the heap memory and objects created using string literals are stored in string constant pool.

======
What is string constant pool: String Constant Pool is the memory space in heap memory specially allocated to store the string objects created using string literals. In String Constant Pool, there will be no two string objects having the same content. Whenever you create a string object using string literal, JVM first checks the content of the object to be created. If there exist an object in the string constant pool with the same content, then it returns the reference of that object. It doesn’t create a new object. If the content is different from the existing objects then only it creates new object.

======
Why StringBuffer and StringBuilder classes are introduced in java when there already exist String class to represent the set of characters: The objects of String class are immutable in nature. i.e you can’t modify them once they are created. If you try to modify them, a new object will be created with modified content. This may cause memory and performance issues if you are performing lots of string modifications in your code. To overcome these issues, StingBuffer and StringBuilder classes are introduced in java.

======
How do you create mutable string objects: Using StringBuffer and StringBuilder classes. These classes provide mutable string objects.

======
Where exactly string constant pool is located in the memory: Inside the heap memory. JVM reserves some part of the heap memory to store string objects created using string literals. 

======
What is string intern: String object in the string constant pool is called as String Intern. You can create an exact copy of heap memory string object in string constant pool. This process of creating an exact copy of heap memory string object in the string constant pool is called interning. intern() method is used for interning.

======
Why strings have been made immutable in java?
- Immutable strings increase security. As they can’t be modified once they are created, so we can use them to store sensitive data like username, password etc.
- Immutable strings are thread safe. So, we can use them in a multi threaded code without synchronization.
- String objects are used in class loading. If strings are mutable, it is possible that wrong class is being loaded as mutable objects are modifiable.

======
Can we use String as HashMap key in Java: Yes, we can use String as a key in HashMap because it implements equals() and hashcode() method which is a required for an object to be used as a key in HashMap.

======
Can string be used in switch case: Java 7 extended the capability of switch case to use Strings also, earlier java versions doesn’t support this.

======
Check whether two strings are anagram of each other. An anagram of a string is another string that contains same characters, only the order of characters can be different. For example, “abcd” and “dabc” are anagram of each other.
- User Sorting. And compare the sorted strings. O(nLogn)
- Create 2 arrays of size 256. Increment the count while traversing both the strings. Compare arrays
- We can increment the value by 1 for string1 and decrement the value by 1 for string2. Using only 1 array. In the end all the values has to be 0
