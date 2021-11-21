## 第一周 - 2021-11-21


##### 题目：(1)加一
##### 链接：https://leetcode-cn.com/problems/plus-one/
##### 语言：Python
```python
class Solution(object):
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        i = len(digits) - 1
        while i >= 0 :
            digits[i] += 1
            digits[i] %= 10
            if digits[i] != 0: return digits
            i -= 1
        
        v = []
        n = len(digits) + 1
        for k in range(n): v.append(0)
        v[0] = 1
        return v


解题思路：
	1.从后往前遍历数组；
	2.在当前元素上自增1，然后和10进行位进；
		- 不等于0：
			表示没有位进，直接返回；

		- 等于0：
			表示存在位进，创建个空数组，
			补齐输入数组的长度+1，并将下标为0的元素置为1；

```
<br>


##### 题目：(2)合并两个有序链表
##### 链接：https://leetcode-cn.com/problems/merge-two-sorted-lists/
##### 语言：Go
```go
func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
    // 链表
    result := &ListNode{Val: 0} 
    // 链表偏移量
    last := result
 
    for l1 != nil || l2 != nil {
        if l2 == nil || (l1 != nil && l1.Val <= l2.Val) {
            last.Next = l1
            last = l1
            l1 = l1.Next
        } else {
            last.Next = l2
            last = l2
            l2 = l2.Next
        }
    }
    return result.Next
}


解题思路：
	1.创建新链表用于记录历史链表元素、记录偏移量；
	2.链表 l1 为空时取 l2, l2 为空时 取 l1；
	3.更新对应 l1、l2 的历史链表和对应偏移量，然后当前循环的链表更新到下个元素；

```
<br>


##### 题目：(3)设计循环双端队列
##### 链接：https://leetcode-cn.com/problems/design-circular-deque/
##### 语言：Python
```python
class MyCircularDeque(object):

    def __init__(self, k):
        """
        :type k: int
        """
        self.queue = []
        self.size = 0
        self.limit_size = k

    def insertFront(self, value):
        """
        :type value: int
        :rtype: bool
        """
        if self.isFull(): return False
        self.queue = [value] + self.queue
        self.size += 1
        return True

    def insertLast(self, value):
        """
        :type value: int
        :rtype: bool
        """
        if self.isFull(): return False
        self.queue.append(value)
        self.size += 1
        return True

    def deleteFront(self):
        """
        :rtype: bool
        """
        if self.isEmpty(): return False
        self.size -= 1
        if len(self.queue) == 1: self.queue = []
        self.queue = self.queue[1:len(self.queue)]
        return True

    def deleteLast(self):
        """
        :rtype: bool
        """
        if self.isEmpty(): return False
        self.queue.pop()
        self.size -= 1
        return True

    def getFront(self):
        """
        :rtype: int
        """
        if self.isEmpty(): return -1
        v = self.queue[0]
        # self.deleteFront()
        return v

    def getRear(self):
        """
        :rtype: int
        """
        if self.isEmpty(): return -1
        v = self.queue[-1]
        # self.deleteLast()
        return v

    def isEmpty(self):
        """
        :rtype: bool
        """
        return len(self.queue) == 0

    def isFull(self):
        """
        :rtype: bool
        """
        return self.size >= self.limit_size

```

