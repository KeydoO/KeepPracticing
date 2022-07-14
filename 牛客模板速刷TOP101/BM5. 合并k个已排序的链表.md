[BM5. 合并k个已排序的链表](https://www.nowcoder.com/practice/65cfde9e5b9b4cf2b6bafa5f3ef33fa6?tpId=295&tqId=724&ru=%2Fpractice%2Fd8b6b4358f774294a89de2a6ac4d9337&qru=%2Fta%2Fformat-top101%2Fquestion-ranking&sourceUrl=%2Fexam%2Foj)
### 解法一（时间复杂度：O(nlog(k))）:
#### 思路分析：
1. 第一时间想到归并排序，并且是已经完成了部分排序的（各个数组）向上归并
2. 先分组，将所有数组对半分直到分为两个一组，如果共k个数组，则会分成k/2组
3. 将每组中的两个数组合并成一个数组，得到k/2个数组，再两两组成一组得到k/4组……不断重复这一过程直到得到最终结果数组并返回
4. 复杂度分析：由于每个数组长度最大为n，共有k个数组，归并排序的时间复杂度就是O(nlog(k))，空间复杂度为递归层数最大为O(log(k))
#### CODE:
```
import java.util.*;
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode Merge(ListNode list1, ListNode list2) {
        if (list1 == null) {
            return list2;
        }
        if (list2 == null) {
            return list1;
        }
        
        ListNode head = new ListNode(0);
        ListNode cur = head;
        
        while (list1 != null && list2 != null) {
            if (list1.val <= list2.val) {
                cur.next = list1;
                list1 = list1.next;
            } else {
                cur.next = list2;
                list2 = list2.next;
            }
            cur = cur.next;
        }
        
        if (list1 != null) cur.next = list1;
        if (list2 != null) cur.next = list2;
        
        return head.next;
    }
    
    ListNode divideMerge(ArrayList<ListNode> lists, int left, int right) {
        if (left > right) {
            return null;
        } else if (left == right) {
            return lists.get(left);
        }
        int mid = (left + right) / 2;
        return Merge(divideMerge(lists, left, mid), divideMerge(lists, mid + 1, right));
    }
    
    public ListNode mergeKLists(ArrayList<ListNode> lists) {
        return divideMerge(lists, 0, lists.size() - 1);
    }
}
```
