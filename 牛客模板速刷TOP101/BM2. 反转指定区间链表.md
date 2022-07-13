[BM2. 反转指定区间链表](https://www.nowcoder.com/practice/b58434e200a648c589ca2063f1faf58c?tpId=295&tqId=654&ru=%2Fpractice%2F75e878df47f24fdc9dc3e400ec6058ca&qru=%2Fta%2Fformat-top101%2Fquestion-ranking&sourceUrl=%2Fexam%2Foj)
### 解法一（时间复杂度：O((n)）:
#### 思路分析：
1. 与BM1思路类似，双指针分别指向当前节点和当前节点的前置节点
2. 首先要找到起始位置m，然后开始在此位置直到n结束开始进行翻转
3. 在原链表头节点前面添加一个新的节点，因为如果要从链表头的位置开始反转，在多了一个表头的情况下就能保证第一个节点永远不会反转，不会到后面去
4. 在m到n的反转这一步中，仍然使用BM1的方法
5. 时间复杂度分析：遍历一次链表，O(n)，空间复杂度为创建的新指针O(1)
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
    /**
     *
     * @param head ListNode类
     * @param m int整型
     * @param n int整型
     * @return ListNode类
     */
    public ListNode reverseBetween (ListNode head, int m, int n) {
        // write code here
        ListNode res = new ListNode(-1);
        res.next = head;
        ListNode pre = res;
        ListNode cur = head;
        // 定位到m
        for (int i = 1; i < m; i++) {
            pre = cur;
            cur = cur.next;
        }
        // 从m开始反转直到n
        // 与BM1比较的话，就是用cur替换了head，用temp.next替换了newHead
        // 而由于pre.next指向的是改变之前的cur，所以也用prenext替换了head
        for (int i = m; i < n; i++) {
            ListNode temp = cur.next;
            cur.next = temp.next;
            temp.next = pre.next;
            pre.next = temp;
        }
        return res.next;
    }
}
```
