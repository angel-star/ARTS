
# Algorithm

[893. Groups of Special-Equivalent Strings](https://leetcode.com/contest/weekly-contest-99/problems/groups-of-special-equivalent-strings/)

题目描述：

**英文：**
You are given an array A of strings.

Two strings S and T are special-equivalent if after any number of moves, S == T.

A move consists of choosing two indices i and j with i % 2 == j % 2, and swapping S[i] with S[j].

Now, a group of special-equivalent strings from A is a non-empty subset S of A such that any string not in S is not special-equivalent with any string in S.

Return the number of groups of special-equivalent strings from A.


**中文：**
你将得到一个字符串数组 A。

如果经过任意次数的移动，S == T，那么两个字符串 S 和 T 是特殊等价的。

 

一次移动包括选择两个索引 i 和 j，且 i％2 == j％2，并且交换 S[j] 和 S [i]。

现在规定，A 中的特殊等价字符串组是 A 的非空子集 S，这样不在 S 中的任何字符串与 S 中的任何字符串都不是特殊等价的。

 

返回 A 中特殊等价字符串组的数量。

**Example 1:**

>Input: [[2]]

>Input: ["a","b","c","a","c","c"]

>Output: 3

>Explanation: 3 groups ["a","a"], ["b"], ["c","c","c"]

**Example 2:**

>Input: ["aa","bb","ab","ba"] 
>
>Output: 4 
>
>Explanation: 4 groups ["aa"], ["bb"], ["ab"], ["ba"]


**Example 3:**

>Input: ["abc","acb","bac","bca","cab","cba"]

>Output: 3

>Explanation: 3 groups ["abc","cba"], ["acb","bca"], ["bac","cab"]

**Example 4:**

>Input: ["abcd","cdab","adcb","cbad"]

>Output: 1

>Explanation: 1 group ["abcd","cdab","adcb","cbad"]



```c++


class Solution {
public:
    int numSpecialEquivGroups(vector<string>& A) {
        unordered_map<string, int> mp;
        for(auto &s : A){
            string even, odd;
            for(int i=0;i<s.size();i+=2) even.push_back(s[i]);
            for(int i=1;i<s.size();i+=2) odd.push_back(s[i]);
            sort(even.begin(), even.end());
            sort(odd.begin(), odd.end());
            ++mp[even+odd];
        }
        return mp.size();
    }
};
```
