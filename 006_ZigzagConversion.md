### 题目描述
The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
```
P   A   H   N
A P L S I I G
Y   I   R
```
And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:
string convert(string s, int numRows);
**Example 1:**
```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```
**Example 2:**
```
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"

Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```

### 分析
- Z字形其实主要考虑是是三段，Z字的两边和中间， 两边是一样的都是N个字符，中间是N-2个字符
- 所以就是N和N-2两种情况， 可以考虑每个横行使用一个字符串变量这样一共N个这样的变量，这N个变量放入一个数组List中。
+ 遍历输入字符串
    - 如果当前字符串处于N段，则数组的第1到N个字符串依次得到一个字符
    - 如果当前字符串处于N-2段， 则数组的第N-1到第2个字符串依次得到一个字符
+ 需要考虑的点，下面的代码中都有答案
    - 如何确定当前字符处于N段还是N-2段
    - 就是字符处于N-2段时，数组的下标如何得到


### 代码
```
class Solution:
    def convert(self, s, numRows):
        """
        :type s: str
        :type numRows: int
        :rtype: str
        """
        if numRows == 1:
            return s  
        ret = ""
        list = []  #用来保存每一横行的字符
        for i in range(numRows):
            list.append("")
        for i in range(len(s)): #遍历每个字符
            index = i % (2*numRows -2)  #2*numRows-2 为两个竖行
            if index < numRows: #在完整的竖行
                list[index] += s[i]
            else: #在中间行
                list[2*numRows-2-index] += s[i]
        for i in range(numRows):
            ret += list[i]
        return ret

s = "PAYPALISHIRING"
s = "A"
#print(Solution().convert(s,3))
print(Solution().convert(s,4))
```

### 提交的结果

