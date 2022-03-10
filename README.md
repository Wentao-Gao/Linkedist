# 链表

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

## 链表相关leetcode题目：

### [203. 移除链表元素](https://leetcode-cn.com/problems/remove-linked-list-elements/) - [视频讲解](https://www.youtube.com/watch?v=JI71sxtHTng) - [思路讲解](https://www.programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html)

**给你一个链表的头节点 head 和一个整数 val ，请你删除链表中所有满足 Node.val == val 的节点，并返回 新的头节点。**

 ```
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

设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：val 和 next。val 是当前节点的值，next 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 prev 以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。

在链表类中实现这些功能：

get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。

addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。

addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。

addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。

deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。
 
```
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
