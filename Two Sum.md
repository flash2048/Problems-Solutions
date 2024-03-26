# 1. Two Sum
https://leetcode.com/problems/two-sum

Given an array of integers `nums` and an integer `target`, return *indices of the two numbers such that they add up to `target`*.

You may assume that each input would have ***exactly* one solution**, and you may not use the *same* element twice.

You can return the answer in any order.

**Example 1:**

```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**

```
Input: nums = [3,2,4], target = 6
Output: [1,2]
```

**Example 3:**

```
Input: nums = [3,3], target = 6
Output: [0,1]
```

```csharp
public class Solution {
    public int[] TwoSum(int[] nums, int target) {
        var lookUp = nums.Select((value, index) => new { value, index }).ToLookup(x => x.value, x => x.index);
        for (var i = 0; i < nums.Length; i++)
        {
            var secondElement = target - nums[i];
            if (lookUp.Contains(secondElement))
            {
                var secondIndex = lookUp[secondElement].FirstOrDefault(x => x != i, -1);
                if (secondIndex == -1)
                    continue;
                return new[] { i, secondIndex };
            }
        }
        return Array.Empty<int>();
    }
}
```