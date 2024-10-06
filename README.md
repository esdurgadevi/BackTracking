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



