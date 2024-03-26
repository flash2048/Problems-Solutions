# 3005. Count Elements With Maximum Frequency
https://leetcode.com/problems/count-elements-with-maximum-frequency/

You are given an array **nums** consisting of **positive** integers.

Return the **total frequencies** of elements in **nums** such that those elements all have the maximum frequency.

The **frequency** of an element is the number of occurrences of that element in the array.

```csharp
public class Solution {
    public int MaxFrequencyElements(int[] nums) {
        var dictionary = new Dictionary<int, int>();
        var maxCount = 0;
        foreach (var element in nums)
        {
            dictionary.TryGetValue(element, out int value);
            value++;
            dictionary[element] = value;
            if (value > maxCount)
                maxCount = value;
        }
        return dictionary.Count(x => x.Value == maxCount) * maxCount;
    }
}
```