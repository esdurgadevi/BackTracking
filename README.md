# BackTracking
### 78. Subsets
[Leetcodelink](https://leetcode.com/problems/subsets/)
<br>
Given an integer array nums of unique elements, return all possible 
subsets (the power set). The solution set must not contain duplicate subsets. Return the solution in any order.

Example 1:
Input: nums = [1,2,3]
Output: [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]

Example 2:
Input: nums = [0]
Output: [[],[0]]
 
Constraints:
1 <= nums.length <= 10
-10 <= nums[i] <= 10
All the numbers of nums are unique.

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
       List<List<Integer>> ans = new ArrayList<>();
       List<Integer> a1 = new ArrayList<>();
       find(0,ans,a1,nums);
       return ans;
    }
    public void find(int index,List<List<Integer>> ans,List<Integer> a1,int[] nums)
    {
        if(index>=nums.length) 
        {
            ans.add(new ArrayList<>(a1));
            return;
        }
        a1.add(nums[index]);
        find(index+1,ans,a1,nums);
        a1.remove(a1.size()-1);
        find(index+1,ans,a1,nums);
    }
}
```
![image](https://github.com/user-attachments/assets/f766cc10-a739-4e36-9572-73ed345ed493)
- In this code we include all the sub array in the nums using back tracking.
- So what will do is we take each number for two case that is take and not take.
<br>
> [Take U Forward](https://www.youtube.com/watch?v=AxNNVECce8c&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=6)
<br>
> [Neetcode](https://www.youtube.com/watch?v=REOH22Xwdkk)

### Perfect Sum Problem
[Geeks for geeks](https://www.geeksforgeeks.org/problems/perfect-sum-problem5633/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=perfect-sum-problem)
<br>
Given an array arr of size n of non-negative integers and an integer sum, the task is to count all subsets of the given array with a sum equal to a given sum. Note: Answer can be very large, so, output answer modulo 109+7.

Examples:
Input: 
n = 6, arr = [5, 2, 3, 10, 6, 8], sum = 10
Output: 
3
Explanation: 
{5, 2, 3}, {2, 8}, {10} are possible subsets.

Input: 
n = 5, arr = [2, 5, 1, 4, 3], sum = 10
Output: 
3
Explanation: 
{2, 1, 4, 3}, {5, 1, 4}, {2, 5, 3} are possible subsets.
Expected Time Complexity: O(n*sum)
Expected Auxiliary Space: O(n*sum)

Constraints:
1 ≤ n*sum ≤ 106
0 ≤ arr[i] ≤ 106

```java

class Solution{
    private int c = 0;
	public int perfectSum(int arr[],int n, int sum) 
	{ 
	    List<Integer> a1 = new ArrayList<>();
	    find(0,a1,arr,sum);
	    return c;
	} 
	public void find(int index,List<Integer> a1,int[] nums,int sum)
    {
        if(index>=nums.length) 
        {
            if(is_sum(a1,sum)) 
            {
                c++;
            }
            return;
        }
        a1.add(nums[index]);
        find(index+1,a1,nums,sum);
        a1.remove(a1.size()-1);
        find(index+1,a1,nums,sum);
    } 
    public boolean is_sum(List<Integer> a1,int sum)
    {
        int s = 0;
        for(int x:a1)
        {
            s+=x;
        }
        if(s==sum) return true;
        else return false;
    }
}
```
- This is same as the above problem but instead of track the sub sequence we count the no of sub sequence whos sum is equal to the given sum.
### 39. Combination Sum
[Leetcode link](https://leetcode.com/problems/combination-sum/description/)
<br>
Given an array of distinct integers candidates and a target integer target, return a list of all unique combinations of candidates where the chosen numbers sum to target. You may return the combinations in any order.
The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the 
frequency of at least one of the chosen numbers is different.
The test cases are generated such that the number of unique combinations that sum up to target is less than 150 combinations for the given input.
 
Example 1:
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]
Explanation:
2 and 3 are candidates, and 2 + 2 + 3 = 7. Note that 2 can be used multiple times.
7 is a candidate, and 7 = 7.
These are the only two combinations.

Example 2:
Input: candidates = [2,3,5], target = 8
Output: [[2,2,2,2],[2,3,3],[3,5]]

Example 3:
Input: candidates = [2], target = 1
Output: []
 
Constraints:
1 <= candidates.length <= 30
2 <= candidates[i] <= 40
All elements of candidates are distinct.
1 <= target <= 40
![image](https://github.com/user-attachments/assets/4014d771-435c-4ff6-8188-7747d25c151a)
![image](https://github.com/user-attachments/assets/5de1d9b2-be2d-4874-bb6f-e57b77666502)
<br>
```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        ArrayList<Integer> a1 = new ArrayList<>();
        find(0,candidates,ans,a1,target);
        return ans;
    }
    public void find(int index,int[] num,List<List<Integer>> ans,ArrayList<Integer> a1,int sum)
    {
        System.out.println(a1);
        if(index>=num.length) 
        {
            if(sum==0)
            {
                System.out.println(a1);
                ans.add(new ArrayList<>(a1));
            }
            return;
        }
        //If we use the couple of code then also correct not include that also correct
        /*if(sum==0)
        {
            System.out.println(a1);
            ans.add(new ArrayList<>(a1));
            return;
        }*/ 
        if(sum>=num[index]) 
        {
            //taking
            a1.add(num[index]);
            find(index,num,ans,a1,sum-num[index]);
            a1.remove(a1.size()-1);
        }
        //Not taking
        find(index+1,num,ans,a1,sum);
    }
}
```
- In the combination problem we have two option one is pick another one is not pick. First we call the function for zeroth index and target.
- Then the one option is to take the same index and the another one is to take the next index that is (not taking condition).
- In the taking option we must reduce the the target by the current index value. We take the current index value only the target value is greater than the current index value.
- So that time we repeatly call the function for the same index. Whenever it reach the last index then it will got to the base condition and check if the target value is zero or not if the target value is zero then we added to the answer otherwise we did not added to the answer we simply return it.
- so we backtrack the condition so we remove the current index value from a1 then we call the function for the next index.
- then it will do the same for that index.
- in the image one pop will shown we add the element then we do all the operation then we pop it to the back track condition then we add the element.
> [REference](https://www.youtube.com/watch?v=OyZFFqQtu98&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=10)

### 40. Combination Sum II
[Leetcode link](https://leetcode.com/problems/combination-sum-ii/description/?envType=problem-list-v2&envId=backtracking&status=ATTEMPTED&difficulty=MEDIUM)
<br>
Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sum to target.
Each number in candidates may only be used once in the combination.
Note: The solution set must not contain duplicate combinations. 

Example 1:
Input: candidates = [10,1,2,7,6,1,5], target = 8
Output: 
[
[1,1,6],
[1,2,5],
[1,7],
[2,6]
]

Example 2:
Input: candidates = [2,5,2,1,2], target = 5
Output: 
[
[1,2,2],
[5]
] 

Constraints:
1 <= candidates.length <= 100
1 <= candidates[i] <= 50
1 <= target <= 30
![image](https://github.com/user-attachments/assets/dd972957-0eab-4e12-ad80-7cced9f1ba40)
#### Brute Froce solution 
```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        ArrayList<Integer> a1 = new ArrayList<>();
        Arrays.sort(candidates);
        find(0,candidates,target,ans,a1);
        return ans;
    }
    public void find(int index,int[] num,int sum,List<List<Integer>> ans,ArrayList<Integer> a1)
    {
        if(index>=num.length)
        {
            if(sum==0)
            {
                if(!ans.contains(new ArrayList<>(a1))) ans.add(new ArrayList<>(a1));
            }
            return;
        }
        if(sum>=num[index])
        {
            a1.add(num[index]);
            find(index+1,num,sum-num[index],ans,a1);
            a1.remove(a1.size()-1);
        }
        find(index+1,num,sum,ans,a1);
    }
}
```
#### Optimal Solution
```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        List<List<Integer>> ans = new ArrayList<>();
        ArrayList<Integer> a1 = new ArrayList<>();
        Arrays.sort(candidates);
        find(0,candidates,target,ans,a1);
        return ans;
    }
    public void find(int index,int[] num,int sum,List<List<Integer>> ans,ArrayList<Integer> a1)
    {
        if(sum==0) 
        {
            ans.add(new ArrayList<>(a1));
            return;
        }
        for(int i=index;i<num.length;i++)
        {
            if(i>index && num[i]==num[i-1]) continue;
            if(sum<num[i]) break;
            a1.add(num[i]);
            find(i+1,num,sum-num[i],ans,a1);
            a1.remove(a1.size()-1);
        }
    }
}
```
- In this code first we do the brute force solution but it wont run for the large input that brute force solution we uses the same logice used in the combination sum 1 but we did not use the sma eindex so we call index+1each time and also we check if the a1 is already present in the ans or not if it is not present then we added to the answer.
- But in the optimal approach we did not take the repeated once.
- First we call the function for index 0. Using the for loop the loop will run from the current index to the length of the num
- The only condition we check is if the sum will smaller than the array element then we break it.
- If the current value is equal to the previous value that we need not to call the recursive function so continue.
- After checking the both condition we add the current element to a1 and recursively call the function for i+1 after that we remove the final elemnet added to the a1.
> [Reference](https://www.youtube.com/watch?v=G1fRTGRxXU8&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=11)
### Subset Sums
[Geeks for geeks link](https://www.geeksforgeeks.org/problems/subset-sums2234/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=subset-sums)
<br>
Given a list arr of n integers, return sums of all subsets in it. Output sums can be printed in any order.

Examples:
Input: n = 2, arr[] = {2, 3}
Output: 0 2 3 5
Explanation: When no elements is taken then Sum = 0. When only 2 is taken then Sum = 2. When only 3 is taken then Sum = 3. When element 2 and 3 are taken then Sum = 2+3 = 5.

Example 2:
Input: n = 3, arr = {1, 2, 1}
Output: 0 1 1 2 2 3 3 4

Expected Time Complexity: O(2n)
Expected Auxiliary Space: O(2n)

Constraints:
1 <= n <= 15
0 <= arr[i] <= 104

```java
class Solution {
    ArrayList<Integer> subsetSums(ArrayList<Integer> arr, int n) {
        ArrayList<Integer> ans = new ArrayList<Integer>();
        find(0,arr,ans,0);
        return ans;
    }
    void find(int index,ArrayList<Integer> arr,ArrayList<Integer> ans,int sum)
    {
        if(index>=arr.size()) 
        {
            ans.add(sum);
            return;
        }
        find(index+1,arr,ans,sum+arr.get(index));
        find(index+1,arr,ans,sum);
    }
    
}
```
- In this code we find the all possible sub sequence sum.
- so the idea is simple take and non take
- For take We add the current index value to the sum for not take we move to the next value without taking the current values to the sum whenver we reach the length of the array that time we add the sum to the ans.
> [Reference](https://www.youtube.com/watch?v=rYkfBRtMJr8&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=12)
### 90. Subsets II
[Leetcode link](https://leetcode.com/problems/subsets-ii/)
<br>
Given an integer array nums that may contain duplicates, return all possible 
subsets(the power set). The solution set must not contain duplicate subsets. Return the solution in any order.

Example 1:
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]

Example 2:
Input: nums = [0]
Output: [[],[0]]

Constraints:
1 <= nums.length <= 10
-10 <= nums[i] <= 10

```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        ArrayList<Integer> a1 = new ArrayList<>();
        Arrays.sort(nums);
        find(0,nums,ans,a1);
        return ans;
    }
    public void find(int index,int[] num,List<List<Integer>> ans,ArrayList<Integer> a1)
    {
        if(index>=num.length)
        {
            if(!ans.contains(a1)) ans.add(new ArrayList<>(a1));
            return;
        }
        a1.add(num[index]);
        find(index+1,num,ans,a1);
        a1.remove(a1.size()-1);
        find(index+1,num,ans,a1);
    }
}
```
- In this case also the same take and non take algorithm and did not add the duplicate to the ans.
- But it will take average of 8ms how i efficient this code means i take only the unique combination.
#### Optimal Code
```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        ArrayList<Integer> a1 = new ArrayList<>();
        Arrays.sort(nums);
        find(0,nums,ans,a1);
        return ans;
    }
    public void find(int index,int[] num,List<List<Integer>> ans,ArrayList<Integer> a1)
    {
        ans.add(new ArrayList<>(a1));
        for(int i=index;i<num.length;i++)
        {
            if(i!=index && num[i]==num[i-1]) continue;
            a1.add(num[i]);
            find(i+1,num,ans,a1);
            a1.remove(a1.size()-1);
        }
    }
}
```
- In this code we take one index in that index we continously call the next next index if the current index value is equal to the previous index value then we continue.
- Other wise we add the element and find the next index then we remove the finally added element. This is same as the combination sum 2. 
> [Reference](https://www.youtube.com/watch?v=RIn3gOkbhQE&list=PLgUwDviBIf0rGlzIn_7rsaR2FQ5e6ZOL9&index=13)
### 1415. The k-th Lexicographical String of All Happy Strings of Length n
[Leetcode link](https://leetcode.com/problems/the-k-th-lexicographical-string-of-all-happy-strings-of-length-n/?envType=daily-question&envId=2025-02-19)
<br>
```java
class Solution {
    public String getHappyString(int n, int k) {
        List<Character> arr = new ArrayList<>();
        List<List<Character>> list = new ArrayList<>();
        find(n,arr,list);
        if(list.size()<k) return "";
        else
        {
            StringBuilder ans = new StringBuilder();
            List<Character> t = list.get(k-1);
            for(char x:t) ans.append(x);
            return ans.toString();
        }
    }
    public void find(int n,List<Character> arr,List<List<Character>> list)
    {
        if(arr.size()>=n)
        {
            list.add(new ArrayList<>(arr));
            return;
        }
        char[] ch = {'a','b','c'};
        for(char x:ch)
        {
            if(arr.size()==0 || arr.get(arr.size()-1)!=x)
            {
                arr.add(x);
                find(n,arr,list);
                arr.remove(arr.size()-1);
            }
        }
    }
}
```
- In this method we back track and find the answer first we generate all the strings using a b c with length of n but no consecutive repetation.
- for this base condition is size greater than the n
- for each charater from a to b if it is empty or not previous one add that and call the function for back track after calling remove it.

### 1980. Find Unique Binary String
[Leetcode link](https://leetcode.com/problems/find-unique-binary-string/?envType=daily-question&envId=2025-02-20)
<br>
Given an array of strings nums containing n unique binary strings each of length n, return a binary string of length n that does not appear in nums. If there are multiple answers, you may return any of them.

 

Example 1:

Input: nums = ["01","10"]
Output: "11"
Explanation: "11" does not appear in nums. "00" would also be correct.
Example 2:

Input: nums = ["00","01"]
Output: "11"
Explanation: "11" does not appear in nums. "10" would also be correct.
Example 3:

Input: nums = ["111","011","001"]
Output: "101"
Explanation: "101" does not appear in nums. "000", "010", "100", and "110" would also be correct.
 

Constraints:

n == nums.length
1 <= n <= 16
nums[i].length == n
nums[i] is either '0' or '1'.
All the strings of nums are unique.

```java
class Solution {
    public String findDifferentBinaryString(String[] nums) {
        StringBuilder str = new StringBuilder();
        List<String> list = new ArrayList<>();
        find(nums[0].length(),list,str);
        for(String x:nums) 
        {
            list.remove(x);
        }
        return list.get(0);
    }
    public void find(int n,List<String> list,StringBuilder str)
    {
        if(str.length()==n) 
        {
            list.add(new String(str.toString()));
            return;
        }
        str.append('0');
        find(n,list,str);
        str.deleteCharAt(str.length()-1);
        str.append('1');
        find(n,list,str);
        str.deleteCharAt(str.length()-1);
    }
}
```
- Using back tracking we generate all the string with length n that is strings length then which string not present in the nums array then we return that string.

#### Other Method:
```java
class Solution {
    public String findDifferentBinaryString(String[] nums) {
        StringBuilder ans= new StringBuilder();                  
        for(int i=0; i<nums.length; i++)  
            ans.append(nums[i].charAt(i) == '0' ? '1' : '0');              // Using ternary operator
        return ans.toString();
    }
}
```
- The trick to do this question is somewhat similar toCantor's Diagonalization. You can read about it in detailhere.

- Since we are given that number of bits in the number is equal to number of elements.
- What we can do is we create a binary string which differs from first binary at 1st position, second binary at 2nd position, third binary at 3rd position,...and so on.

- This will make sure that the binary we have made is unique (as it differs from all others at atleast one position).

- We create an empty string first.
- And simply iterate through the binary strings while putting the flipped bit of ith bit of "binary at ith position".
### 46. Permutations
[Leetcode link](https://leetcode.com/problems/permutations/)
<br>
Given an array nums of distinct integers, return all the possible permutations. You can return the answer in any order.

 

Example 1:

Input: nums = [1,2,3]
Output: [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
Example 2:

Input: nums = [0,1]
Output: [[0,1],[1,0]]
Example 3:

Input: nums = [1]
Output: [[1]]
 

Constraints:

1 <= nums.length <= 6
-10 <= nums[i] <= 10
All the integers of nums are unique.

```java
class Solution {
    public void find(int[] nums,List<List<Integer>> ans,List<Integer> arr,boolean[] freq)
    {
        if(arr.size()==nums.length){
            ans.add(new ArrayList<>(arr));
            return;
        }
        for(int i=0;i<nums.length;i++){
            if(!freq[i]){
                freq[i] = true;
                arr.add(nums[i]);
                find(nums,ans,arr,freq);
                arr.remove(arr.size()-1);
                freq[i] = false;
            }
        }
    }
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        List<Integer> arr = new ArrayList<>();
        boolean[] freq = new boolean[nums.length];
        find(nums,ans,arr,freq);
        return ans;
    }
}
```
> [Reference](https://www.youtube.com/watch?v=YK78FU5Ffjw)
### 1863. Sum of All Subset XOR Totals
[Leetcodelink](https://leetcode.com/problems/sum-of-all-subset-xor-totals/?envType=daily-question&envId=2025-04-05)
<br>
The XOR total of an array is defined as the bitwise XOR of all its elements, or 0 if the array is empty.

For example, the XOR total of the array [2,5,6] is 2 XOR 5 XOR 6 = 1.
Given an array nums, return the sum of all XOR totals for every subset of nums. 

Note: Subsets with the same elements should be counted multiple times.

An array a is a subset of an array b if a can be obtained from b by deleting some (possibly zero) elements of b.

 

Example 1:

Input: nums = [1,3]
Output: 6
Explanation: The 4 subsets of [1,3] are:
- The empty subset has an XOR total of 0.
- [1] has an XOR total of 1.
- [3] has an XOR total of 3.
- [1,3] has an XOR total of 1 XOR 3 = 2.
0 + 1 + 3 + 2 = 6
Example 2:

Input: nums = [5,1,6]
Output: 28
Explanation: The 8 subsets of [5,1,6] are:
- The empty subset has an XOR total of 0.
- [5] has an XOR total of 5.
- [1] has an XOR total of 1.
- [6] has an XOR total of 6.
- [5,1] has an XOR total of 5 XOR 1 = 4.
- [5,6] has an XOR total of 5 XOR 6 = 3.
- [1,6] has an XOR total of 1 XOR 6 = 7.
- [5,1,6] has an XOR total of 5 XOR 1 XOR 6 = 2.
0 + 5 + 1 + 6 + 4 + 3 + 7 + 2 = 28
Example 3:

Input: nums = [3,4,5,6,7,8]
Output: 480
Explanation: The sum of all XOR totals for every subset is 480.
 

Constraints:

1 <= nums.length <= 12
1 <= nums[i] <= 20

```java
class Solution {
    public int subsetXORSum(int[] nums) {
        List<Integer> arr = new ArrayList<>();
        find(0,nums,arr,0);
        int ans = 0;
        for(int x:arr)
        {
            ans += x;
        }
        return ans;
    }
    public void find(int index,int[] nums,List<Integer> ans,int res)
    {
        if(index >= nums.length)
        {
            System.out.println(res);
            ans.add(res);
            return;
        }
        //taking
        find(index+1,nums,ans,res^nums[index]);
        //not taking
        find(index+1,nums,ans,res);
    }
}
```
