# 394. Decode String
https://leetcode.com/problems/decode-string/

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed `105`.

**Example 1:**

```
Input: s = "3[a]2[bc]"
Output: "aaabcbc"
```

**Example 2:**

```
Input: s = "3[a2[c]]"
Output: "accaccacc"
```

**Example 3:**

```
Input: s = "2[abc]3[cd]ef"
Output: "abcabccdcdcdef"
```

```csharp
public class Solution
{
	public string DecodeString(string s)
	{
		var result = new StringBuilder();

		var count = 0;
		for (int i = 0; i < s.Length; i++)
		{
			if (char.IsDigit(s[i]))
			{
				count = count * 10 + s[i] - '0';
			}
			else
			if (s[i] == '[')
			{
				var j = i + 1;
				var bcount = 1;
				while (bcount != 0)
				{
					if (s[j] == '[')
						bcount++;
					else if (s[j] == ']')
						bcount--;
					j++;
				}
				var str = DecodeString(s.Substring(i + 1, j - i - 2));
				result.Append(string.Join("", Enumerable.Repeat(str, count)));
				i = j - 1;
				count = 0;
			}
			else
			{
				result.Append(s[i]);
			}
		}

		return result.ToString();
	}
}
```