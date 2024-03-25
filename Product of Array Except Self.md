# 238. Product of Array Except Self
https://leetcode.com/problems/product-of-array-except-self

Given an integer array `nums`, return *an array* `answer` *such that* `answer[i]` *is equal to the product of all the elements of* `nums` *except* `nums[i]`.

The product of any prefix or suffix of `nums` is **guaranteed** to fit in a **32-bit** integer.

You must write an algorithm that runs in `O(n)` time and without using the division operation.

**Example 1:**

```
Input: nums = [1,2,3,4]
Output: [24,12,8,6]
```

**Example 2:**

```
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]
```

```csharp
public class Solution
{
	public int[] ProductExceptSelf(int[] nums)
	{
		var size = nums.Length;
		var countOfZero = 0;
		var zeroIndex = 0;
		var mult = 1;

		for (var i = 0; i < size; i++)
		{
			if (nums[i] == 0)
			{
				countOfZero++;
				zeroIndex = i;
			}
			else
			{
				mult *= nums[i];
			}

			if (countOfZero == 2)
				return new int[size];
		}

		if (countOfZero > 0)
		{
			nums = new int[size];
			nums[zeroIndex] = mult;
		}
		else
		{
			for (var i = 0; i < size; i++)
			{
				nums[i] = mult / nums[i];
			}
		}

		return nums;
	}
}
```