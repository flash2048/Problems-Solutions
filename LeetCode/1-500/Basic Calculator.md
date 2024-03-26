# 224. Basic Calculator
https://leetcode.com/problems/basic-calculator/

Given a string **s** representing a valid expression, implement a basic calculator to evaluate it, and return the result of the evaluation.

Note: You are **not** allowed to use any built-in function which evaluates strings as mathematical expressions, such as **eval()**.

**Constraints**:

* **1 <= s.length <= 3 * 10^5**
* **s** consists of digits, **'+'**, **'-'**, **'('**, **')'**, and **' '**.
* **s** represents a valid expression.
* **'+'** is not used as a unary operation (i.e., **"+1"** and **"+(2 + 3)"** is invalid).
* **'-'** could be used as a unary operation (i.e., **"-1"** and **"-(2 + 3)"** is valid).
* There will be no two consecutive operators in the input.
* Every number and running calculation will fit in a signed 32-bit integer.

```csharp
public class Solution {
    public int Calculate(string s) {
        var result = 0;
        var sign = 1;

        for (int i = 0; i < s.Length; i++)
        {
            var c = s[i];
            switch (c)
            {
                case ' ': break;
                case '+':
                    sign = 1;
                    break;
                case '-':
                    sign = -1;
                    break;
                case '(':
                    var countOfBrackets = 1;
                    var substringPosition = i + 1;
                    while (countOfBrackets != 0)
                    {
                        if (s[++i] == '(')
                            countOfBrackets++;
                        else
                        if (s[i] == ')')
                            countOfBrackets--;
                    }
                    var substringResult = Calculate(s.Substring(substringPosition, i - substringPosition));
                    result += sign * substringResult;
                    break;
                default:
                    var number = c - '0';
                    while (i + 1 < s.Length && char.IsDigit(s[i + 1]))
                    {
                        number *= 10;
                        number += s[++i] - '0';
                    }
                    result += sign * number;
                    break;
            }
        }

        return result;
    }
}
```