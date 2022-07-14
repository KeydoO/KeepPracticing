[BM3. 链表中的节点每k个一组翻转](https://www.nowcoder.com/practice/b49c3dc907814e9bbfa8437c251b028e?tpId=295&tqId=722&ru=%2Fpractice%2Fb58434e200a648c589ca2063f1faf58c&qru=%2Fta%2Fformat-top101%2Fquestion-ranking&sourceUrl=%2Fexam%2Foj)
### 解法一（时间复杂度：O((n)）:
#### 思路分析：
1. 反转过程与BM1思路类似，双指针分别指向当前节点和当前节点的前置节点，反转时再引入temp临时指针
2. 只不过在本题中要先进行分组，从第一个元素开始每k个一组，在组内进行翻转
3. 如果从最后一组开始翻转，得到了最后一组的链表首，就可以直接连在倒数第二组翻转后的尾（即翻转前的头）后面，更加方便
4. 所以要采用递归调用的方法，具体分析如下：
   终止条件： 当进行到最后一个分组，即不足k次遍历到链表尾（0次也算），就将剩余的部分直接返回。  
   返回值： 每一级要返回的就是翻转后的这一分组的头，以及连接好它后面所有翻转好的分组链表。  
   本级任务： 对于每个子问题，先遍历k次，找到该组结尾在哪里，然后从这一组开头遍历到结尾，依次翻转，结尾就可以作为下一个分组的开头，而先前指向开头的元素已经跑到了这一分组的最后，可以用它来连接它后面的子问题，即后面分组的头。
5. 时间复杂度分析：遍历一次链表，O(n)，递归栈深度为n/k，给空间复杂度为O(n)
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
     * @param k int整型 
     * @return ListNode类
     */
    public ListNode reverseKGroup (ListNode head, int k) {
        // write code here
        // 找到每次反转的尾部，从头部开始
        ListNode tail = head;
        // 遍历k次到尾部
        for (int i = 0; i < k; i++) {
            // 如果不足k到了尾部，直接返回，不用反转
            if (tail == null) {
                return head;
            }
            tail = tail.next;
        }
        // 以下翻转思路和BM1相同
        ListNode pre = null;
        ListNode cur = head;
        while (cur != tail) {
            ListNode temp = cur.next;
            cur.next = pre;
            pre = cur;
            cur = temp;
        }
        // 当前尾指向下一段要反转的链表头部
        head.next = reverseKGroup(tail, k);
        return pre;
    }
}
```
