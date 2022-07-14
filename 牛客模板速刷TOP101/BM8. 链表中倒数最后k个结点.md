[BM8. 链表中倒数最后k个结点](https://www.nowcoder.com/practice/886370fe658f41b498d40fb34ae76ff9?tpId=295&tqId=1377477&ru=%2Fpractice%2F253d2c59ec3e4bc68da16833f79a38e4&qru=%2Fta%2Fformat-top101%2Fquestion-ranking&sourceUrl=%2Fexam%2Foj)
### 解法一（时间复杂度：O(n)）:
#### 思路分析：
1. 最简单的思路是先遍历一遍整个链表，统计出链表中节点总数total
2. 然后再从头开始找到第total+1-k个节点并返回即可
3. 还有一种思路是利用双指针
4. 设置一快一慢两个指针，从链表头部开始，前者先出发走k步，然后后者再出发
5. 由于他们都是一次走一步，中间会始终差着k个节点，那么当快指针到链表尾部时，慢指针会刚好指着倒数第k个节点
6. 复杂度分析：时间复杂度O(n)，空间复杂度O(1)
#### CODE:
```
import java.util.*;

/*
 * public class ListNode {
 *   int val;
 *   ListNode next = null;
 *   public ListNode(int val) {
 *     this.val = val;
 *   }
 * }
 */

public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param pHead ListNode类 
     * @param k int整型 
     * @return ListNode类
     */
    public ListNode FindKthToTail (ListNode pHead, int k) {
        // write code here
        ListNode cur = pHead;
        int total = 0;
        while (cur != null) {
            total++;
            cur = cur.next;
        }
        if (total < k) {
            return null;
        }
        cur = pHead;
        for (int count = 1; count < (total + 1 - k); count++) {
            cur = cur.next;
        }
        return cur;
        
        /** 
        * 还有一个双指针思路
        * 先让第一个指针走k步，然后第二个指针再出发
        * 两个指针都是一次一步，他们之间始终差着k个节点
        * 这样当第一个指针到达链表尾部时第二个指针刚好指着倒数第k个节点
        */
    }
}
```
