# [链表](https://gwt9970161.github.io/Linkedist/)

[算法与数据结构目录](https://gwt9970161.github.io/Data-structue-and-algorithym-python/)

这一节将着重知识讲解与代码实践

## 链表的理论基础

链表是一种通过指针串联在一起的线性结构，每一个节点由两部分组成，一个是数据域一个是指针域（存放指向下一个节点的指针），最后一个节点的指针指
向null（空指针的意思）

链接的入口节点称为链表的头节点也就是head。

![image](https://user-images.githubusercontent.com/77952995/157702248-1b1d2d43-b9c1-4768-8a4b-7bee970e4df3.png)

### 链表的类型

**单链表**：

上面所说即是单链表

**双链表**：

单链表的节点只能指向节点的下一个节点。
双链表： 每一个节点有两个指针域，一个指向下一个节点，一个指向上一个节点。
双链表既可以向前查询也可以向后查询。

![image](https://user-images.githubusercontent.com/77952995/157702331-6de63c27-851a-4a68-a9b7-78fd3333b584.png)


**循环链表**

循环链表，就是链表首尾相连。
循环链表用于解决约瑟夫环问题。

![image](https://user-images.githubusercontent.com/77952995/157702366-4ea3e856-746f-4bfe-9d01-856c37061350.png)


### 链表的存储方式

数组是在内存中连续分布的，但是链表在内存中可不是连续分布的。

链表是通过指针域的指针链接在内存中的各个节点。

所以链表中的节点在内存中不是连续分布的，而是散乱分布在内存的某地址上，分配机制取决于操作系统的内存管理。


链表的定义（记下）：

```python

class ListNode{
   def __init__(self, val, next = None):
        self.val = val
        self.next = next      
}

```

### 链表操作：

#### 删除节点

删除D节点

![image](https://user-images.githubusercontent.com/77952995/157702790-acbd90c0-3a17-44bc-b607-f856f6540f5c.png)

只要将C节点的next指针指向E节点就可以了。

#### 添加节点

![image](https://user-images.githubusercontent.com/77952995/157705180-cfa928e4-89d5-433a-99dc-bb2dcfdbd99b.png)

将C节点指向F节点，再将F节点指向D节点即可

可以看出链表的增添和删除都是$O(1)$操作，也不会影响到其他节点。

但是要注意要是删除第五个节点，需要从头节点查找到第四个节点通过next指针进行删除操作，查找的时间复杂度为$O(n)$

### 性能分析
再把链表的特性和数组的特性进行一个对比，如图所示：

![image](https://user-images.githubusercontent.com/77952995/157707352-9898909b-3658-4b86-9995-2d4cf77a82d2.png)

数组在定义的时候，长度就是固定的，如果想改动数组的长度，就需要重新定义一个新的数组。

链表的长度可以是不固定的，并且可以动态增删，适合数据量不固定，频繁增删，较少查询的场景。


## 链表相关leetcode题目

**[链表题思路](https://www.youtube.com/watch?v=0czlvlqg5xw)**

### [203. 移除链表元素](https://leetcode-cn.com/problems/remove-linked-list-elements/) - [视频讲解](https://www.youtube.com/watch?v=JI71sxtHTng) - [思路讲解](https://www.programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html)

```
**给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点。**

示例：

示例 1：
输入：head = [1,2,6,3,4,5,6], val = 6
输出：[1,2,3,4,5]；

示例 2：
输入：head = [], val = 1
输出：[]；

示例 3：
输入：head = [7,7,7,7], val = 7
输出：[]；
 
提示：
列表中的节点数目在范围 [0, 104] 内
1 <= Node.val <= 50
0 <= val <= 50
```
**Solution**

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: ListNode, val: int) -> ListNode:
        dummy_head = ListNode(next = head)
        curr = dummy_head
        while curr.next != None:
            if curr.next.val == val:
                curr.next = curr.next.next
            else:
                curr = curr.next
        return dummy_head.next
```

### [707. 设计链表](https://leetcode-cn.com/problems/design-linked-list/) - [视频讲解](https://www.youtube.com/watch?v=uLSbZzLaeQ4) - [思路讲解](https://www.programmercarl.com/0707.%E8%AE%BE%E8%AE%A1%E9%93%BE%E8%A1%A8.html#%E4%BB%A3%E7%A0%81)

```
设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：val 和 next。val 是当前节点的值，next 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 prev 以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。

在链表类中实现这些功能：

get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。

addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。

addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。

addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。

deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。
 
示例：

MyLinkedList linkedList = new MyLinkedList();
linkedList.addAtHead(1);
linkedList.addAtTail(3);
linkedList.addAtIndex(1,2);   //链表变为1-> 2-> 3
linkedList.get(1);            //返回2
linkedList.deleteAtIndex(1);  //现在链表是1-> 3
linkedList.get(1);            //返回3
 

提示：

所有val值都在 [1, 1000] 之内。
操作次数将在  [1, 1000] 之内。
请不要使用内置的 LinkedList 库。

```
**Solution**

```python
class Node:
    def __init__(self, val):
        self.val = val
        self.next = None

class MyLinkedList:

    def __init__(self):
        self._head = Node(0)
        self._count = 0


    def get(self, index: int) -> int:
        if 0 <= index < self._count:
            node = self._head
            for _ in range(index + 1):
                node = node.next
            return node.val
        else:
            return -1


    def addAtHead(self, val: int) -> None:
        self.addAtIndex(0, val)


    def addAtTail(self, val: int) -> None:
        self.addAtIndex(self._count, val)


    def addAtIndex(self, index: int, val: int) -> None:
        if index < 0:
            index = 0
        elif index > self._count:
            return
        
        self._count += 1

        add_node = Node(val)
        prev_node, curr_node = None, self._head
        for _ in range(index+1):
            prev_node, curr_node = curr_node, curr_node.next
        else:
            prev_node.next, add_node.next = add_node, curr_node

        
    def deleteAtIndex(self, index: int) -> None:
        if 0 <= index < self._count:
             self._count -= 1
             prev_node, current_node = None, self._head
             for _ in range(index + 1):
                prev_node, current_node = current_node, current_node.next
             else:
                prev_node.next, current_node.next = current_node.next, None



# Your MyLinkedList object will be instantiated and called as such:
# obj = MyLinkedList()
# param_1 = obj.get(index)
# obj.addAtHead(val)
# obj.addAtTail(val)
# obj.addAtIndex(index,val)
# obj.deleteAtIndex(index)

```

### [206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/) - [视频讲解](https://www.youtube.com/watch?v=G0_I-ZF0S38&t=26s) - [思路讲解](https://www.programmercarl.com/0206.%E7%BF%BB%E8%BD%AC%E9%93%BE%E8%A1%A8.html#%E5%8F%8C%E6%8C%87%E9%92%88%E6%B3%95)
```
给你单链表的头节点 head ，请你反转链表，并返回反转后的链表。
 
示例 1：
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
示例 2：
输入：head = [1,2]
输出：[2,1]
示例 3：
输入：head = []
输出：[]

提示：

链表中节点的数目范围是 [0, 5000]
-5000 <= Node.val <= 5000

```

**Solution**

```python

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        curr = head
        pre = None
        while (curr != None):
            rec = curr.next
            curr.next = pre
            pre = curr
            curr = rec
        return pre 

```

### [24. 两两交换链表中的节点](https://leetcode-cn.com/problems/swap-nodes-in-pairs/) - [视频讲解](https://www.youtube.com/watch?v=o811TZLAWOo) - [思路讲解](https://www.programmercarl.com/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html#_24-%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9)

```
给你一个链表，两两交换其中相邻的节点，并返回交换后链表的头节点。你必须在不修改节点内部的值的情况下完成本题（即，只能进行节点交换）。

示例 1：
输入：head = [1,2,3,4]
输出：[2,1,4,3]
示例 2：
输入：head = []
输出：[]
示例 3：
输入：head = [1]
输出：[1]
 
提示：
链表中节点的数目在范围 [0, 100] 内
0 <= Node.val <= 100

```
**Solution**

```python

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        res = ListNode(next = head)
        pre = res

        while pre.next and pre.next.next:
            curr = pre.next
            post = pre.next.next

            curr.next = post.next
            post.next = curr
            pre.next = post

            pre = pre.next.next
        return res.next

```

### [19. 删除链表的倒数第N个节点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/) - [视频讲解](https://www.youtube.com/watch?v=XVuQxVej6y8) - [思路讲解](https://www.programmercarl.com/0019.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B9.html#_19-%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACn%E4%B8%AA%E8%8A%82%E7%82%B9)

```
19. 删除链表的倒数第 N 个结点
给你一个链表，删除链表的倒数第 n 个结点，并且返回链表的头结点。

示例 1：
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
示例 2：
输入：head = [1], n = 1
输出：[]
示例 3：
输入：head = [1,2], n = 1
输出：[1]
 
提示：
链表中结点的数目为 sz
1 <= sz <= 30
0 <= Node.val <= 100
1 <= n <= sz
```
**Solution**

```python

# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        head_dummy = ListNode()
        head_dummy.next = head

        slow, fast = head_dummy, head_dummy
        while(n!=0): #fast先往前走n步
            fast = fast.next
            n -= 1
        while(fast.next!=None):
            slow = slow.next
            fast = fast.next
        #fast 走到结尾后，slow的下一个节点为倒数第N个节点
        slow.next = slow.next.next #删除
        return head_dummy.next

```

### [206. 链表相交](https://leetcode-cn.com/problems/intersection-of-two-linked-lists-lcci/) - [视频讲解](https://www.youtube.com/watch?v=D0X0BONOQhI) - [思路讲解](https://www.programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html#%E6%80%9D%E8%B7%AF)

```
给你两个单链表的头节点 headA 和 headB ，请你找出并返回两个单链表相交的起始节点。如果两个链表没有交点，返回 null 。

图示两个链表在节点 c1 开始相交：



题目数据 保证 整个链式结构中不存在环。

注意，函数返回结果后，链表必须 保持其原始结构 。

 

示例 1：



输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
输出：Intersected at '8'
解释：相交节点的值为 8 （注意，如果两个链表相交则不能为 0）。
从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。
在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。
示例 2：



输入：intersectVal = 2, listA = [0,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
输出：Intersected at '2'
解释：相交节点的值为 2 （注意，如果两个链表相交则不能为 0）。
从各自的表头开始算起，链表 A 为 [0,9,1,2,4]，链表 B 为 [3,2,4]。
在 A 中，相交节点前有 3 个节点；在 B 中，相交节点前有 1 个节点。
示例 3：



输入：intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
输出：null
解释：从各自的表头开始算起，链表 A 为 [2,6,4]，链表 B 为 [1,5]。
由于这两个链表不相交，所以 intersectVal 必须为 0，而 skipA 和 skipB 可以是任意值。
这两个链表不相交，因此返回 null 。
 

提示：

listA 中节点数目为 m
listB 中节点数目为 n
0 <= m, n <= 3 * 104
1 <= Node.val <= 105
0 <= skipA <= m
0 <= skipB <= n
如果 listA 和 listB 没有交点，intersectVal 为 0
如果 listA 和 listB 有交点，intersectVal == listA[skipA + 1] == listB[skipB + 1]
```

Solution

```python

class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        """
        根据快慢法则，走的快的一定会追上走得慢的。
        在这道题里，有的链表短，他走完了就去走另一条链表，我们可以理解为走的快的指针。

        那么，只要其中一个链表走完了，就去走另一条链表的路。如果有交点，他们最终一定会在同一个
        位置相遇
        """
        cur_a, cur_b = headA, headB     # 用两个指针代替a和b

        
        while cur_a != cur_b:
            cur_a = cur_a.next if cur_a else headB      # 如果a走完了，那么就切换到b走
            cur_b = cur_b.next if cur_b else headA      # 同理，b走完了就切换到a
        
        return cur_a

```

### [142. 环形链表II](https://leetcode-cn.com/problems/linked-list-cycle-ii/) - [视频讲解](https://www.youtube.com/watch?v=gBTe7lFR3vc) - [思路讲解](https://www.programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html#_142-%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8ii)

```
给定一个链表的头节点  head ，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，评测系统内部使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。

不允许修改 链表。

 

示例 1：



输入：head = [3,2,0,-4], pos = 1
输出：返回索引为 1 的链表节点
解释：链表中有一个环，其尾部连接到第二个节点。
示例 2：



输入：head = [1,2], pos = 0
输出：返回索引为 0 的链表节点
解释：链表中有一个环，其尾部连接到第一个节点。
示例 3：



输入：head = [1], pos = -1
输出：返回 null
解释：链表中没有环。
 

提示：

链表中节点的数目范围在范围 [0, 104] 内
-105 <= Node.val <= 105
pos 的值为 -1 或者链表中的一个有效索引
```
**Solution**

```python

class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            # 如果相遇
            if slow == fast:
                p = head
                q = slow
                while p!=q:
                    p = p.next
                    q = q.next
                #你也可以return q
                return p

        return None

```
