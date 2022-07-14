[BM4. 合并两个排序的链表](https://www.nowcoder.com/practice/d8b6b4358f774294a89de2a6ac4d9337?tpId=295&tqId=23267&ru=%2Fpractice%2Fb49c3dc907814e9bbfa8437c251b028e&qru=%2Fta%2Fformat-top101%2Fquestion-ranking&sourceUrl=%2Fexam%2Foj)
### 解法一（时间复杂度：O(n)）:
#### 思路分析：
1. 很简单的归并排序，新建一个头指针result作为结果返回，新建一个指针cur指向当前元素，每向结果链表中添加一个元素cur就向后移动一位
2. 从两个链表的头节点开始，每次循环中都比较两个链表的头节点元素值，谁更小就作为比较结果加入到结果链表中，并且该链表的头指针向后移动一位
3. 时间复杂度分析：遍历一次两个链表，O(n)，空间复杂度为一些创建的新指针故为O(1)
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
    public ListNode Merge(ListNode list1,ListNode list2) {
        ListNode result = new ListNode(-1);
        ListNode cur = result;
        while (list1 != null && list2 != null) {
            if (list1.val > list2.val) {
                cur.next = list2;
                list2 = list2.next;
                cur = cur.next;
            }
            else {
                cur.next = list1;
                list1 = list1.next;
                cur = cur.next;
            }
        }
        if (list1 != null) {
            cur.next = list1;
        }
        if (list2 != null) {
            cur.next = list2;
        }
        return result.next;
    }
}
```
