# 1759. Count Number of Homogenous Substrings
https://leetcode.com/problems/count-number-of-homogenous-substrings/

Given a string `s`, return *the number of **homogenous** substrings of* `s`*.* Since the answer may be too large, return it **modulo** `109 + 7`.

A string is **homogenous** if all the characters of the string are the same.

A **substring** is a contiguous sequence of characters within a string.

**Example 1:**

```
Input: s = "abbcccaa"
Output: 13
Explanation: The homogenous substrings are listed as below:
"a"   appears 3 times.
"aa"  appears 1 time.
"b"   appears 2 times.
"bb"  appears 1 time.
"c"   appears 3 times.
"cc"  appears 2 times.
"ccc" appears 1 time.
3 + 1 + 2 + 1 + 3 + 2 + 1 = 13.
```

**Example 2:**

```
Input: s = "xy"
Output: 2
Explanation: The homogenous substrings are "x" and "y".
```

**Example 3:**

```
Input: s = "zzzzz"
Output: 15
```

```csharp
public class Solution
{
	public int CountHomogenous(string s)
	{
		var homogenouses = new Dictionary<char, long>();

		var usedSymbol = '\t';
		var currentCount = 0;
		for (var i = 0; i < s.Length; i++)
		{
			var currentSymbol = s[i];
			if (currentSymbol.Equals(usedSymbol))
			{
				currentCount++;
				if (homogenouses.TryGetValue(currentSymbol, out var usedCount))
					homogenouses[currentSymbol] += currentCount;
				else
					homogenouses.Add(currentSymbol, 1);
			}
			else
			{
				currentCount = 1;
				usedSymbol = currentSymbol;

				if (homogenouses.ContainsKey(currentSymbol))
					homogenouses[currentSymbol] += currentCount;
				else
					homogenouses.Add(currentSymbol, currentCount);
			}
		}

		return (int)(homogenouses.Sum(x => x.Value) % 1000000007);
	}
}
```