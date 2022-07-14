[BM7. 链表中环的入口结点](https://www.nowcoder.com/practice/253d2c59ec3e4bc68da16833f79a38e4?tpId=295&tqId=23449&ru=%2Fpractice%2F650474f313294468a4ded3ce0f7898b9&qru=%2Fta%2Fformat-top101%2Fquestion-ranking&sourceUrl=%2Fexam%2Foj)
### 解法一（时间复杂度：O(n)）:
#### 思路分析：
1. 与BM6一样使用双指针，设置一快一慢两个指针，快的走两步慢的走一步
2. 如果在快慢指针相遇前快指针先到达了链表尾部说明不存在环，返回null即可
3. 如果快慢指针相遇了说明存在环，且存在如下数学关系：  
   假设链表中环前有b个节点，环中有c个节点，快慢指针相遇时，fast走了f步，slow走了s步  
   显然由于两个指针的步幅会有f = 2s；而且相遇时一定是在环中，快指针比慢指针多走了c的整数倍步（nc）（俗称套圈了）
   即f = 2s = s + nc，所以有s = nc，f = 2nc  
   而他们相遇的点由于是在环前先走了t步，那么再在环中走t步就会回到进入环的起点位置（建议画图辅助理解）  
4. 这样我们明确了，先找到相遇点，在从相遇点起走t步到达的那个位置就是入环点
5. 为了确定走了t步，我们把快指针移回链表头部而慢指针原地不动，同时开始移动两个指针一次一步，他们再次相遇的位置就是入环点
6. 复杂度分析：时间复杂度就是n的一次关系所以是O(n)，空间复杂度引入两个指针O(1)
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
}
*/
public class Solution {

    public ListNode EntryNodeOfLoop(ListNode pHead) {
        ListNode fast = pHead;
        ListNode slow = pHead;
        while (true) {
            if (fast.next == null || fast.next.next == null) {
                return null;
            }
            slow = slow.next;
            fast = fast.next.next;
            if (fast == slow) {
                break;
            }
        }
        fast = pHead;
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        return fast;
    }
}
```
