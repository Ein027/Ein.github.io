---
layout:     post
title:      【leetcode】题解3 Longest Substring Without Repeating Characters (Medium)
subtitle:   避免手凉
date:       2018-10-27
author:     Ein
header-img: img/leetcode.png
catalog: true
tags:
    - Leetcode
---
## Longest Substring Without Repeating Characters	无重复字符的最长子串

Link: <https://leetcode.com/problems/longest-substring-without-repeating-characters/>

#### Problem:

Given a string, find the length of the **longest substring** without repeating characters.

给定两个**非空**链表来表示两个非负整数。位数按照**逆序**方式存储，它们的每个节点只存储单个数字。将两数相加返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

#### Example:

```
输入: "abcabcbb"
输出: 3 
解释: 无重复字符的最长子串是 "abc"，其长度为 3。

输入: "bbbbb"
输出: 1
解释: 无重复字符的最长子串是 "b"，其长度为 1。

输入: "pwwkew"
输出: 3
解释: 无重复字符的最长子串是 "wke"，其长度为 3。
     请注意，答案必须是一个子串，"pwke" 是一个子序列 而不是子串。
```



#### Approach:

**“滑动窗口法”**，窗口由 **I** 和 **r** 包含，假设永远其中永远无重复部分, **r** 不断右移，如果检查到重复，则把 **l** 变为使 **[l,r]** 恰好不重复的边界,即让 **l** 等于字母为 **s[r]** 且最靠近的下标的后一个。这样能保证窗口内永无重复。
比方说 **abcabccc** 当你右边扫描到 **abca** 的时候你得把前一个重复 **a** 删掉得到 **bca**，然后"窗口"继续向右 滑动，每当加到一个新char的时候，左边检查有无重复的char，然后如果没有重复的就正常添加，有重复的话就左边扔掉一部分（从最左到重复char这段扔掉），在这个过程中记录最大窗口长度。

#### Solution:

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if(s.size()==0)
            return 0;       
        unordered_map<char,int> record; /*储存某字母最右的下标，可以优化成数组*/
        int longest=0;
        int left=0; /*没有重复的最有*/
        int size=0;
        for(int i=0;i<s.size();i++)
        {
            left=max(left, record.find(s[i])==record.end()?0:record[s[i]]+1);
            /*注意这里是找到这个字符的后一个*/
            size=i-left+1;
            if(longest<size)
                longest=size;  
            record[s[i]]=i;
        }
        return longest;  
    }
};
```

