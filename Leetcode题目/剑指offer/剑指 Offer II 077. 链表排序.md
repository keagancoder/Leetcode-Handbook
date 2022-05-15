### 题目描述

给定链表的头结点 `head` ，请将其按 **升序** 排列并返回 **排序后的链表** 。

**示例 1：**

![img](https://assets.leetcode.com/uploads/2020/09/14/sort_list_1.jpg)

```
输入：head = [4,2,1,3]
输出：[1,2,3,4]
```

**示例 2：**

![img](https://assets.leetcode.com/uploads/2020/09/14/sort_list_2.jpg)

```
输入：head = [-1,5,3,4,0]
输出：[-1,0,3,4,5]
```

**示例 3：**

```
输入：head = []
输出：[]
```

---

### 解题思路

#### 归并排序

- 分治：使用快慢指针的方式取链表中点划分
- 合并：分别取两个链表进行合并

##### 代码：

```java
class Solution {
	public ListNode sortList(ListNode head) {
		return sortList(head,null);
	}
	public ListNode sortList(ListNode head, ListNode tail){
		if(head == null){
			return head;
		}
		if(head.next == tail){
			head.next = null;
			return head;
		}
		ListNode slow = head, fast = head;
		while(fast != tail){
			slow = slow.next;
			fast = fast.next;
			if(fast != tail){
				fast = fast.next;
			}
		}
		ListNode mid = slow;
		ListNode list1 = sortList(head, mid);
		ListNode list2 = sortList(mid, tail);
		ListNode sorted = merge(list1, list2);
		return sorted;
	}
	public ListNode merge(ListNode head1, ListNode head2){
		ListNode dummyHead = new ListNode(0);
		ListNode cur = dummyHead, cur1 = head1, cur2 = head2;
		while(cur1 != null && cur2 != null){
			if(cur1.val < cur2.val){
				cur.next = cur1;
				cur1 = cur1.next;
			} else{
				cur.next = cur2;
				cur2 = cur2.next;
			}
			cur = cur.next;
		}
		cur.next = cur1== null ? cur2:cur1;
		return dummyHead.next;
	}
}
```

