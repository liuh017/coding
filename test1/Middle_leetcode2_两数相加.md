#### [2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

```/**
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
        ListNode * L0=new ListNode(0);
        ListNode* LL=L0;
        int c_out=0,sum=0;
        
        /*if (l1->val==0) {
            return l2;
        }
        else if (l2->val==0)
        {
            return l1;
        }*/
        while((l1!=NULL || l2!=NULL) || c_out!=0) {
            LL->next=new ListNode(0);
            LL=LL->next;
            sum=c_out;
            if (l1!=NULL || l2!=NULL) {
                if(l1==NULL)
                    sum+=l2->val;
                else if(l2==NULL)
                    sum+=l1->val;
                else
                    sum+=l1->val+l2->val;
                if(sum>9)
                {
                    c_out=1;
                    LL->val=sum-10;
                }
                else
                {   c_out=0;
                    LL->val=sum;
                }
                if(l1!=NULL)
                l1=l1->next;
                if(l2!=NULL)
                l2=l2->next;
            }
            else
            {
                c_out=0;
                LL->val=sum;
            }
        }
        
       // cout<<"L0"<<L0->next->val<<endl;
        return L0->next;
    }
};
```

执行用时 :36 ms, 在所有 C++ 提交中击败了73.66%的用户

内存消耗 :10.1 MB, 在所有 C++ 提交中击败了95.76%的用户
