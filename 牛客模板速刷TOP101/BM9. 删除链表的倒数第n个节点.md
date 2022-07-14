[BM9. 删除链表的倒数第n个节点](https://www.nowcoder.com/practice/f95dcdafbde44b22a6d741baf71653f6?tpId=295&tqId=727&ru=%2Fpractice%2F886370fe658f41b498d40fb34ae76ff9&qru=%2Fta%2Fformat-top101%2Fquestion-ranking&sourceUrl=%2Fexam%2Foj)
### 解法一（时间复杂度：O(n)）:
#### 思路分析：
1. 利用BM8中提到的双指针法找到倒数第n个节点，其前序节点指向其后继节点即可完成删除该节点的操作
2. 为了可能需要能够删除头节点，在链表前面再添加一个节点res，后继指向head
3. 再设置一个pre指针跟在cur指针后面一步，以便完成删除操作
4. 最后返回res.next即可
5. 复杂度分析：时间复杂度O(n)，空间复杂度O(1)
#### CODE:
```
import java.util.*;

/*
 * public class ListNode {
 *   int val;
 *   ListNode next = null;
 * }
 */

public class Solution {
    /**
     * 
     * @param head ListNode类 
     * @param n int整型 
     * @return ListNode类
     */
    public ListNode removeNthFromEnd (ListNode head, int n) {
        // write code here
        ListNode res = new ListNode(-1);
        res.next = head;
        ListNode fast = head;
        ListNode cur = head;
        ListNode pre = res;
        while (n != 0) {
            fast = fast.next;
            n--;
        }
        while (fast != null) {
            fast = fast.next;
            pre = cur;
            cur = cur.next;
        }
        pre.next = cur.next;
        return res.next;
    }
}
```
