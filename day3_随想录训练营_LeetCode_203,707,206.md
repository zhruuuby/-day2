## Leecode_ [203. 移除链表元素](https://leetcode.cn/problems/remove-linked-list-elements/)
给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 **新的头节点** 。
**示例 1：**

![](https://assets.leetcode.com/uploads/2021/03/06/removelinked-list.jpg)

输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]

思路：
快慢指针i，j；`j=i->next；`如果`j=val`，则`i`直接连接`j->next`，释放`j`，然后`j`指向`next`

## 无虚拟头结点
要区分头结点和非头结点的满足情况

> 头结点的值等于val，则直接移动头结点即可
> 非头结点的值等于val，则头结点不动，要新建结点

   

     class  Solution {
        public:    
            ListNode*  removeElements(ListNode*  head, int  val) {
        //无虚拟头结点时    
		    //删除头结点    
		    while(head != nullptr && head -> val == val){    
				    ListNode *temp = head;    
				    head = head -> next;
				    delete temp;//手动清除这个结点    
		    }
    		    //删除非头结点    
		    ListNode *p = head;    
		    while(p != nullptr && p -> next != nullptr){    
			    if(p -> next -> val == val){    
					    ListNode *temp = p -> next;    
					    p -> next = p -> next -> next;    
					    delete temp;    
			    }    
			    else{    
					    p = p -> next;    
				   }    
		    }
		    return head;
		}
    };

## 有虚拟头结点
则一视同仁，最后要注意把虚拟头结点删除   

    class  Solution {
            public:    
                ListNode*  removeElements(ListNode*  head, int  val) {
    ListNode* dummyHead = new ListNode(0); // 设置一个虚拟头结点
            dummyHead->next = head; // 将虚拟头结点指向head，这样方面后面做删除操作
            ListNode* p= dummyHead;
            while (p->next != NULL) {
                if(p->next->val == val) {
                    ListNode* tmp = p->next;
                    cur->next = p->next->next;
                    delete tmp;
                } 
                else {
                    p= p->next;
                }
            }
            head = dummyHead->next;
            delete dummyHead;
            return head;
        }
    };          

## LeetCode [707. 设计链表](https://leetcode.cn/problems/design-linked-list/)    

暂时保留，有些还没弄懂

## LeetCode [206. 反转链表](https://leetcode.cn/problems/reverse-linked-list/)
法一：头插法，记得是数据结构中，头插法可以实现链表逆转，依旧可以自己先创建一个虚拟头结点

    class Solution {
    public:
        ListNode* reverseList(ListNode* head) {
            ListNode *dummyHead = new ListNode(0);
            ListNode *p = head;
            while(p != nullptr){
                head = head -> next;
                p -> next = dummyHead -> next;
                dummyHead -> next = p;
                p = head;
            }
            head = dummyHead -> next;
            delete dummyHead;
            return head;
        }
    };
    
法二：双指针法，和头插法大同小异
![enter image description here](https://code-thinking.cdn.bcebos.com/gifs/206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.gif)

*（图片来自代码随想录）*

实现循环的地方：

    cur -> next = pre;
    pre = cur;
    cur = temp;
完整代码：
```
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* temp; // 保存cur的下一个节点
        ListNode* cur = head;
        ListNode* pre = NULL;
        while(cur) {
            temp = cur->next;  // 保存一下 cur的下一个节点，因为接下来要改变cur->next
            cur->next = pre; // 翻转操作
            // 更新pre 和 cur指针
            pre = cur;
            cur = temp;
        }
        return pre;
    }
};
```
