### 题目
> 题目链接： https://leetcode-cn.com/explore/interview/card/top-interview-questions-easy/6/linked-list/42/

题目描述：

```
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
说明：

给定的 n 保证是有效的。

进阶：

你能尝试使用一趟扫描实现吗？
```

### 初级解法
思路：
1. 计数，计算链表的长度
2. 找到被删除节点的前一个节点
3. 进行删除操作，链表顺数第一个节点和最后一个节点要单独处理
```javascript
var removeNthFromEnd = function(head, n) {
     let count = 0;
     let nodeCurr = head;
     if(nodeCurr.next === null){ // 只有一个节点的情况
         return null;
     }
     while(nodeCurr !== null){
         count ++;
         nodeCurr = nodeCurr.next;
     }
     let m = count - n;
     let nodePrev = head;
     while(m > 1){
         nodePrev = nodePrev.next;
         m --;
     }
     if(n === 1) { // 倒数第一个
         nodePrev.next = null;
     } else if (count === n){ // 顺数第一个
         head.val = head.next.val;
         head.next = head.next.next;
     } else if(nodePrev.next !== null){ // 中间节点
         nodePrev.next = nodePrev.next.next;
     }
     return head;
};
```

### 使用一遍扫描实现
思路：
1. 使用快慢指针
2. 慢指针在 0，快指针在 0 + n
3. 快指针的 next 指向 null 的时候，慢指针所在的节点就是倒数第 n 个节点，因为快指针比慢指针快了 n 个
```javascript
var removeNthFromEnd = function(head, n){
     if (head.next === null) { // 只有一个节点的情况
         return null;
     }
    
     let low = head;
     let fast = head;
     let m = n;
     // 这一步是为了给快指针赋值，慢指针在 0，快指针在 0 + n
     while (m > 0){
         if (fast.next === null) { // 删除头节点的情况
             head.val = head.next.val;
             head.next = head.next.next;
             return head;
         } else {
             fast = fast.next;
         }
         m --;
     }
     while (fast.next !== null) {
         low = low.next;
         fast = fast.next;
     }
     if (n === 1) { // 删除倒数第一个节点的情况
         low.next = null;
     } else { // 中间节点
         low.val = low.next.val;
         low.next = low.next.next;
     }
     return head;
};
```


