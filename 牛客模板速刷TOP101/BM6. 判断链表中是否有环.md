[BM6. 判断链表中是否有环](https://www.nowcoder.com/practice/650474f313294468a4ded3ce0f7898b9?tpId=295&tqId=605&ru=%2Fpractice%2F65cfde9e5b9b4cf2b6bafa5f3ef33fa6&qru=%2Fta%2Fformat-top101%2Fquestion-ranking&sourceUrl=%2Fexam%2Foj)
### 解法一（时间复杂度：O(n)）:
#### 思路分析：
1. 典型的也是最简单的双指针
2. 设置一快一慢两个指针，从链表头部开始，前者一次走两步，后者一次走一步
3. 如果链表中有环那么一定会有两指针相遇的一次。否则如果快指针指向了null则不存在环
4. 复杂度分析：时间复杂度O(n)，空间复杂度O(1)
#### CODE:
```
import java.util.*;
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (fast == slow) return true;
        }
        return false;
    }
}
```
