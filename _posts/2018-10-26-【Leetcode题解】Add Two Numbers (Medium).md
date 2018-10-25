---
layout:     post
title:      【leetcode】题解2 Add Two Numbers (Medium)
subtitle:   避免手凉
date:       2018-10-26
author:     Ein
header-img: img/leetcode.png
catalog: true
tags:
    - Leetcode
---
## Add Two Numebers	两数相加

Link: <https://leetcode.com/problems/add-two-numbers/>

#### Problem:

You are given two **non-empty** linked lists representing two non-negative integers. The digits are stored in **reverse order** and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

给定两个**非空**链表来表示两个非负整数。位数按照**逆序**方式存储，它们的每个节点只存储单个数字。将两数相加返回一个新的链表。

你可以假设除了数字 0 之外，这两个数字都不会以零开头。

#### Example:

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```



#### Approach:

暴力，注意进位，dump节点的技巧。

#### Solution:

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* cur_1=l1;
        ListNode* cur_2=l2;
        int flag=0; /*进位标志*/
        ListNode* pre;
        ListNode* dump=new ListNode(0); /*哑节点*/
        ListNode* cur=dump;
        while(cur_1!=NULL || cur_2!=NULL || flag!=0)
        {
            int sum=0;
            if(cur_1!=NULL)
            {
                sum=sum+cur_1->val;
                cur_1=cur_1->next;
            }
            if(cur_2!=NULL)
            {
                sum=sum+cur_2->val;
                cur_2=cur_2->next;
            }
            sum=sum+flag;
            flag=sum/10;
            cur->next=new ListNode(sum%10); /*直接插入*/
            cur=cur->next;
        }
        return dump->next;
    }
};
```

