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


