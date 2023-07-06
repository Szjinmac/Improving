# DAY3



由于数组中的数据在内存中是 **连续** 存放的，通过数组下标的可以以 *O*(1) 的时间复杂度访问到元素的值。

在数组中

- 内存地址连续
- 相同类型的元素所占的空间
- 因此要访问数组里的某个元素，程序要执行的操作数与这个元素 在数组里的位置无关 。所以我们说，数组支持 随机访问（Random Access） ，这里的「随机」可以理解为「随意」，即：访问数组的不同位置的元素的值是相对方便的，这一点区别于链表。


由于数组中的数据在内存中是连续存放的，如果要在数组的任意位置 **插入** 或者 **删除** 元素，时间复杂度为 *O*(*N*)



## 链表

与数组不同的是，链表中的数据 **分散** 在内存的不同位置，通常由 CPU 随机分配。在真正存储数据的部分后面还带着一块区域，这块区域存储了 下一个数据 的 内存地址 。程序读取这个内存地址，就可以访问到下一个元素。由于要保存真正的数据和下一个数据的内存地址，链表的最基本单元至少有 2 个数据块，它们通过类的对象（Java、Python 语言）或者结构体（C 语言）组织起来。



- 在链表里增加、删除节点，时间复杂度为O(1),在链表里访问一个节点，时间复杂度为o(N)。于是我们在数组里添加、或者删除元素，通常会在 **数组的末尾** 操作，而对链表的添加和删除，通常会在 **链表的起始位置** 操作。



### 206.反转链表

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseList(ListNode head) {
        if(head == null || head.next == null) return head;
        ListNode preNode = null;
        ListNode curNode = head;

        while(curNode!=null){
            ListNode nextNode = curNode.next;
            curNode.next =preNode;
            preNode = curNode;
            curNode = nextNode;
        }

        return preNode;
    }
}
```



### 203.移除链表元素

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if(head == null) return head;

        //添加虚拟头节点
        ListNode dummy = new ListNode(-1);
        dummy.next = head;

        ListNode preNode = dummy;
        ListNode curNode = dummy.next;

        while(curNode != null ){
            if(curNode.val == val){
                preNode.next = curNode.next;
                curNode = preNode.next;
            }else{
                preNode = curNode;
                curNode = curNode.next;
            }
        }

        return dummy.next;
    }
}
```



### 707.设计链表

```java
class MyLinkedList {
    int size;
    ListNode head;

    public MyLinkedList() {
        size = 0;
        head = new ListNode(0);
    }

    public int get(int index) {
        if (index < 0 || index >= size) {
            return -1;
        }
        ListNode cur = head;
        for (int i = 0; i <= index; i++) {
            cur = cur.next;
        }
        return cur.val;
    }

    public void addAtHead(int val) {
        addAtIndex(0, val);
    }

    public void addAtTail(int val) {
        addAtIndex(size, val);
    }

    public void addAtIndex(int index, int val) {
        if (index > size) {
            return;
        }
        index = Math.max(0, index);
        size++;
        ListNode pred = head;
        for (int i = 0; i < index; i++) {
            pred = pred.next;
        }
        ListNode toAdd = new ListNode(val);
        toAdd.next = pred.next;
        pred.next = toAdd;
    }

    public void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }
        size--;
        ListNode pred = head;
        for (int i = 0; i < index; i++) {
            pred = pred.next;
        }
        pred.next = pred.next.next;
    }
}

class ListNode {
    int val;
    ListNode next;

    public ListNode(int val) {
        this.val = val;
    }
}

```

