[BM1. 反转链表](https://www.nowcoder.com/practice/75e878df47f24fdc9dc3e400ec6058ca?tpId=295&tqId=23286&ru=%2Fpractice%2Fb58434e200a648c589ca2063f1faf58c&qru=%2Fta%2Fformat-top101%2Fquestion-ranking&sourceUrl=%2Fexam%2Foj)
### 解法一（时间复杂度：O((n)）:
#### 思路分析：
1. 利用双指针新建一个链表，其头结点newHead一开始指向空节点，temp始终指向head.next
2. head.next指向新链表头节点newHead，然后head随着新链表的生成不断向后移动
3. 直到head为空节点为止，说明旧链表已遍历完成，最后返回新链表newHead即可
4. 时间复杂度分析：遍历一次链表，O(n)，空间复杂度为创建的新链表O(n)
#### CODE:
```
import java.util.*;
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode ReverseList(ListNode head) {
        ListNode newHead = null;
        while (head != null) {
            temp = head.next;
            head.next = newHead;
            newHead = head;
            head = temp;
        }
        return newHead;
    }
}
```
