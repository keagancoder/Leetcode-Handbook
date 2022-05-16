### 题目描述

给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

**示例 1：**

```java
输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6

```

----

### 解题思路

在解决合并多个链表之前，回想合并两个链表的思路；那么不难得出，合并多个链表可以通过分治-归并的思想：

- Step 1: 划分链表：针对链表数组不断划分链表直到两两一组
- Step 2: 归并链表：定义两个`list`的`head1` 和`head2`，按照合并两个链表的思路合并

##### 代码：

```java
class Solution {
	public ListNode mergeKLists(ListNode[] lists) {
		return merge(lists,0,lists.length - 1);
	}
	public ListNode merge(ListNode[] lists, int l, int r){
		if(l == r) return lists[l];
		if(l > r ) return null;
		int mid = l + (r - l) /2;
		return mergeTwoList(merge(lists, l, mid),merge(lists,mid+1,r));
	}
	public ListNode mergeTwoList(ListNode l1, ListNode l2){
		if(l1 == null && l2 == null) return null;
		if(l1 == null || l2 == null) return l1==null?l2:l1;
		ListNode preHead = new ListNode(-1);
		ListNode cur = preHead;
		while(l1 != null && l2 != null){
			if(l1.val < l2.val){
				cur.next = l1;
				l1 = l1.next;
			} else{
				cur.next =l2;
				l2 = l2.next;
			}
			cur = cur.next;
		}
		cur.next = l1==null? l2:l1;
		return preHead.next;
	}
}
```

