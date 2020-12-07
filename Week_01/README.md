#本周作业及下周预习

##第一周
====================================
## 本周作业

### 简单：

- 用 add first 或 add last 这套新的 API 改写 Deque 的代码
- 分析 Queue 和 Priority Queue 的源码
- [删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)（Facebook、字节跳动、微软在半年内面试中考过）
- [旋转数组](https://leetcode-cn.com/problems/rotate-array/)（微软、亚马逊、PayPal 在半年内面试中考过）
- [合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)（亚马逊、字节跳动在半年内面试常考）
- [合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)（Facebook 在半年内面试常考）
- [两数之和](https://leetcode-cn.com/problems/two-sum/)（亚马逊、字节跳动、谷歌、Facebook、苹果、微软在半年内面试中高频常考）
- [移动零](https://leetcode-cn.com/problems/move-zeroes/)（Facebook、亚马逊、苹果在半年内面试中考过）
- [加一](https://leetcode-cn.com/problems/plus-one/)（谷歌、字节跳动、Facebook 在半年内面试中考过）

### 中等：

- [设计循环双端队列](https://leetcode.com/problems/design-circular-deque)（Facebook 在 1 年内面试中考过）

### 困难：

- [接雨水](https://leetcode.com/problems/trapping-rain-water/)（亚马逊、字节跳动、高盛集团、Facebook 在半年内面试常考）

## 下周预习

### 预习题目：

- [有效的字母异位词](https://leetcode-cn.com/problems/valid-anagram/description/)
- [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
- [最小的 k 个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)


## 本周作业提交内容

### 简单：

#### 1、【待补】用 add first 或 add last 这套新的 API 改写 Deque 的代码

#### 2、分析 Queue 和 Priority Queue 的源码

**见后文源码分析**

#### 3、【√】[删除排序数组中的重复项](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)（Facebook、字节跳动、微软在半年内面试中考过）

```
 static public int removeDuplicates2(int[] nums) {

       if(nums==null || nums.length == 0) return 0;

       int oldLen = nums.length;

       int i = 0;//始终指定着前一个不是重复的位置
       int j = 1;//一直向后走，找到不是重复的位置

       while (j < oldLen){

           //如果不相等
           if(nums[i] != nums[j]){
               nums[i+1] = nums[j];
               i++;
           }
           j++;
       }

       return i+1;

    }
```

#### 4、【√】[旋转数组](https://leetcode-cn.com/problems/rotate-array/)（微软、亚马逊、PayPal 在半年内面试中考过）
```
    public void rotate(int[] nums, int k) {
        int len = nums.length-1;

        //从第k个开始旋转,如果k=3，说明要循环3次
        for (int i = k ; i > 0 ; i--) {
            //临时记录下来需要提到前面的数字
            int temp = nums[len];

            //向后挪动，从第1个位置开始往后挪动
            for (int j = len-1 ; j >= 0 ; j--) {
                nums[j+1] = nums[j];
            }
            nums[0] = temp;
        }
    }
```

#### 5、【√】[合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)（亚马逊、字节跳动在半年内面试常考）


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
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        
        if(l1==null){
            return l2;
        } 

        if(l2==null){
            return l1;
        }

        int v1 = l1.val;
        int v2 = l2.val;
        
        if(v1<v2){
            l1.next = mergeTwoLists(l1.next,l2);
            return l1;
        }else{
            l2.next = mergeTwoLists(l1,l2.next);
            return l2;
        }

    }
}
```

#### 6、【√】[合并两个有序数组](https://leetcode-cn.com/problems/merge-sorted-array/)（Facebook 在半年内面试常考）

```
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        if (m == 0) {
            nums1[0] = nums2[0];
        }
        m--;
        n--;

        while (m >= 0 && n >= 0) {
            if (nums1[m] > nums2[n]) {
                nums1[m + n + 1] = nums1[m];
                m--;
            } else {
                nums1[m + n + 1] = nums2[n];
                n--;
            }
        }

        int index = m + n + 1;
        if (m == -1 && n >= 0) {
            while (n >= 0) {
                nums1[index--] = nums2[n--];
            }
        }

        if (m >= 0 && n == -1) {
            while (m >= 0)
                nums1[index--] = nums1[m--];
        }
    }
}
```


#### 7、【√】[两数之和](https://leetcode-cn.com/problems/two-sum/)（亚马逊、字节跳动、谷歌、Facebook、苹果、微软在半年内面试中高频常考）

```java
package 算法训练营.第一周.练习;

import java.util.Arrays;

public class 两数之和 {
    static public int[] twoSum(int[] nums, int target) {


        for (int i = 0; i < nums.length - 1; i++) {
            for (int j = i+1; j < nums.length ; j++) {
                if(nums[i] + nums[j] == target){
                    return new int[]{i,j};
                }
            }
        }

        return new int[]{};
    }

    public static void main(String[] args) {
        int [] nums = {3,3};
        int target = 6;

        int[] ints = twoSum(nums, target);
        System.out.println(Arrays.toString(ints));
    }
}
```



#### 8、【√】[移动零](https://leetcode-cn.com/problems/move-zeroes/)（Facebook、亚马逊、苹果在半年内面试中考过）



```java
package 算法训练营;

public class moveZeroes {
    static public void moveZeroes(int[] nums) {
        int j = 0;

        for (int i = 0; i < nums.length; i++) {
            //如果遇到的数据为0，就把后面的往前移动。例如：[0,1,0,3,12] -> [1,0,3,12,0]
            if(nums[i]!=0){
                //向前移动
                nums[j] = nums[i];
                if(i != j){
                    nums[i] = 0;
                }
                j++;
            }
        }
    }

    static public int maxArea(int[] height) {

        int max = 0;

        for(int i = 0; i < height.length -1 ; i++){
            for(int j = i + 1 ; j < height.length; j++){
                int area = ( j - i) * Math.min(height[i],height[j]);
                max = Math.max(area,max);
            }
        }

        return max;
    }

    public static void main(String[] args) {

//        int[] array = {4,3,2,1,4};
//        System.out.println(maxArea(array));
        int [] ints = {0,1,0,3,12};
//        int [] ints = {0,0,1};
        moveZeroes(ints);

        for (int anInt : ints) {
            System.out.print(anInt+",");
        }

    }
}
```





#### 9、【√】[加一](https://leetcode-cn.com/problems/plus-one/)（谷歌、字节跳动、Facebook 在半年内面试中考过）





```java
package 算法训练营.第一周.练习;

import java.util.Arrays;

public class 加一 {

   static public int[] plusOne(int[] digits) {

        for (int i = digits.length-1; i >= 0; i--) {
            //从尾部开始+1
            digits[i]++;

            digits[i] %= 10;

            //如果模10之后不等于0，说明不需要进位了，就直接返回现在的数组极客
            if(digits[i]  != 0)
                return digits;
        }

        //说明[9,0,0]出现这种情况了，第1个数为9
        int newIntArray[] = new int[digits.length+1];
        newIntArray[0]=1;

        return newIntArray;
    }

    public static void main(String[] args) {
        System.out.println(Arrays.toString(plusOne(new int[]{9,9})));
    }
}
```



### 中等：

#### 1、[设计循环双端队列](https://leetcode.com/problems/design-circular-deque)（Facebook 在 1 年内面试中考过）
学习的比较经典的一个：

https://leetcode-cn.com/problems/design-circular-deque/solution/shu-zu-shi-xian-de-xun-huan-shuang-duan-dui-lie-by/

```java
//设计实现双端队列。 
//你的实现需要支持以下操作： 
//
// 
// MyCircularDeque(k)：构造函数,双端队列的大小为k。 
// insertFront()：将一个元素添加到双端队列头部。 如果操作成功返回 true。 
// insertLast()：将一个元素添加到双端队列尾部。如果操作成功返回 true。 
// deleteFront()：从双端队列头部删除一个元素。 如果操作成功返回 true。 
// deleteLast()：从双端队列尾部删除一个元素。如果操作成功返回 true。 
// getFront()：从双端队列头部获得一个元素。如果双端队列为空，返回 -1。 
// getRear()：获得双端队列的最后一个元素。 如果双端队列为空，返回 -1。 
// isEmpty()：检查双端队列是否为空。 
// isFull()：检查双端队列是否满了。 
// 
//
// 示例： 
//
// MyCircularDeque circularDeque = new MycircularDeque(3); // 设置容量大小为3
//circularDeque.insertLast(1);                  // 返回 true
//circularDeque.insertLast(2);                  // 返回 true
//circularDeque.insertFront(3);                 // 返回 true
//circularDeque.insertFront(4);                 // 已经满了，返回 false
//circularDeque.getRear();                  // 返回 2
//circularDeque.isFull();                       // 返回 true
//circularDeque.deleteLast();                   // 返回 true
//circularDeque.insertFront(4);                 // 返回 true
//circularDeque.getFront();             // 返回 4
//  
//
// 
//
// 提示： 
//
// 
// 所有值的范围为 [1, 1000] 
// 操作次数的范围为 [1, 1000] 
// 请不要使用内置的双端队列库。 
// 
// Related Topics 设计 队列 
// 👍 65 👎 0


import java.util.Arrays;

//leetcode submit region begin(Prohibit modification and deletion)
class MyCircularDeque {


    private int capacity;
    private int [] arr;
    private int front;
    private int rear;


    /** Initialize your data structure here. Set the size of the deque to be k. */
    public MyCircularDeque(int k) {
        capacity = k +1;
        arr = new int[capacity];
        front = 0;
        rear = 0;
    }

    /** Adds an item at the front of Deque. Return true if the operation is successful. */
    public boolean insertFront(int value) {
        if(isFull()){
            return false;
        }

        front = (front -1 + capacity) % capacity;
        arr[front] = value;
        return true;
    }

    /** Adds an item at the rear of Deque. Return true if the operation is successful. */
    public boolean insertLast(int value) {
        if (isFull()) {
            return false;
        }

        arr[rear] = value;

        rear = (rear +1) %capacity;
        return true;
    }

    /** Deletes an item from the front of Deque. Return true if the operation is successful. */
    public boolean deleteFront() {
        if (isEmpty()) {
            return false;
        }

        front = (front+1) % capacity;
        return true;
    }

    /** Deletes an item from the rear of Deque. Return true if the operation is successful. */
    public boolean deleteLast() {
        if (isEmpty()) {
            return false;
        }
        rear = (rear - 1 + capacity) % capacity;
        return true;
    }

    /** Get the front item from the deque. */
    public int getFront() {
        if (isEmpty()) {
            return -1;
        }
        return arr[front];
    }

    /** Get the last item from the deque. */
    public int getRear() {
        if (isEmpty()) {
            return -1;
        }
        return arr[(rear - 1 + capacity) % capacity];
    }

    /** Checks whether the circular deque is empty or not. */
    public boolean isEmpty() {
        return front == rear;
    }

    /** Checks whether the circular deque is full or not. */
    public boolean isFull() {
        return (rear + 1) % capacity == front;
    }
}

/**
 * Your MyCircularDeque object will be instantiated and called as such:
 * MyCircularDeque obj = new MyCircularDeque(k);
 * boolean param_1 = obj.insertFront(value);
 * boolean param_2 = obj.insertLast(value);
 * boolean param_3 = obj.deleteFront();
 * boolean param_4 = obj.deleteLast();
 * int param_5 = obj.getFront();
 * int param_6 = obj.getRear();
 * boolean param_7 = obj.isEmpty();
 * boolean param_8 = obj.isFull();
 */
//leetcode submit region end(Prohibit modification and deletion)
```



### 困难：

#### 1、[接雨水](https://leetcode.com/problems/trapping-rain-water/)（亚马逊、字节跳动、高盛集团、Facebook 在半年内面试常考）


====================================

###数组、链表、跳表的基本实现和特性
数组 ：插入删除是o（n），lookup是o（1)  
链表：插入，删除都是o(1)，lookup是o（n)  
跳表： 对标平衡树和二分查找。原始的有序序列添加多级索引，升维+空间换时间    
[跳表的论文原文](ftp://ftp.cs.umd.edu/pub/skipLists/skiplists.pdf)

参考链接  
[Java 源码分析（ArrayList）](http://developer.classpath.org/doc/java/util/ArrayList-source.html)  
[Redis - Skip List：跳跃表、为啥 Redis 使用跳表（Skip List）而不是使用 Red-Black？](https://www.zhihu.com/question/20202931)


#分析 PriorityQueue
##一、摘要
PriorityQueue 一个特殊的优先级队列
![PriorityQueue继承关系](/Week_01/doc/PriorityQueue.jpg)
##二、简介
PriorityQueue 并没有直接实现 Queue接口，而是通过继承 AbstractQueue 类来实现 Queue 接口一些方法，在 Java 定义中，PriorityQueue 是一个基于优先级的无界优先队列。
通俗的说，添加到 PriorityQueue 队列里面的元素都经过了排序处理，默认按照自然顺序，也可以通过 Comparator 接口进行自定义排序。

优先队列的作用是保证每次取出的元素都是队列中权值最小的。

如果猿友们了解过 TreeMap 的实现，会发现 PriorityQueue 排序实现与之类似。

PriorityQueue 是采用树形结构来描述元素的存储，具体说是通过完全二叉树实现一个小顶堆，在物理存储方面，PriorityQueue 底层通过数组来实现元素的存储。
###源码介绍
```
public class PriorityQueue<E> extends AbstractQueue<E>
    implements java.io.Serializable {
	
	/**默认容量为11*/
	private static final int DEFAULT_INITIAL_CAPACITY = 11;

	/**队列容器*/
    transient Object[] queue;

	/**队列长度*/
    private int size = 0;

	/**比较器,为null使用自然排序*/
    private final Comparator<? super E> comparator;

	......
}
```
从定义中可以得出，PriorityQueue 有3个比较核心的变量属性，内容如下：

queue：表示存放元素的数组
comparator：表示比较器对象，如果为空，使用自然排序
size：表示队列长度
我们再来看看 PriorityQueue 类的构造方法，PriorityQueue 构造方法分两类，一种是默认初始化、另一种是传入 Comparator 接口比较器，内容如下：

默认初始化，使用自然排序方式进行插入，源码如下：
```
public PriorityQueue() {
	//默认数组长度为11，传入比较器为null
    this(DEFAULT_INITIAL_CAPACITY, null);
}
```
调用的方法，源码如下：
```
public PriorityQueue(int initialCapacity, Comparator<? super E> comparator) {
	//初始化容量小于 1，抛异常
    if (initialCapacity < 1)
        throw new IllegalArgumentException();
    this.queue = new Object[initialCapacity];
    this.comparator = comparator;
}
```
自定义比较器初始化，使用 comparator 接口比较器作为参数传入，源码如下：
```
public PriorityQueue(Comparator<? super E> comparator) {
	//传入比较器 comparator
    this(DEFAULT_INITIAL_CAPACITY, comparator);
}
```
##三、常见方法介绍
3.1、添加方法
PriorityQueue 的添加方法有 2 种，分别是add(E e)和offer(E e)，两者语义相同，都是向优先队列中插入元素，只是Queue接口规定二者对插入失败时的处理不同，前者在插入失败时抛出异常，后则返回false。

3.1.1、offer 方法
offer 方法图解实现流程如下：
![offer 方法图解](/Week_01/doc/offer.jpg)
新加入的元素可能会破坏小顶堆的性质，在 c、d 两步会进行调整。

offer 方法的实现，源码如下：
```
public boolean offer(E e) {
	//不允许放入null元素
    if (e == null)
        throw new NullPointerException();
    modCount++;
    int i = size;
    if (i >= queue.length)
		//自动扩容
        grow(i + 1);
    size = i + 1;
	//队列原来为空，这是插入的第一个元素
    if (i == 0)
        queue[0] = e;
    else
		//调整
        siftUp(i, e);
    return true;
}
```
值得注意的是，插入元素不能为null，否则报空指针异常!

当数组空间不足时，会进行扩容，扩容函数grow()类似于ArrayList里的grow()函数，就是再申请一个更大的数组，并将原数组的元素复制过去，源码如下：
```
private void grow(int minCapacity) {
    int oldCapacity = queue.length;
	//如果旧数组容量小于64，新容量为 oldCapacity *2 +2
	//如果大于64，新容量为 oldCapacity + oldCapacity * 0.5
    int newCapacity = oldCapacity + ((oldCapacity < 64) ?
                                     (oldCapacity + 2) :
                                     (oldCapacity >> 1));
    //判断是否超过最大容量值，设置最高容量值
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        newCapacity = hugeCapacity(minCapacity);
	//复制数组元素
    queue = Arrays.copyOf(queue, newCapacity);
}
```
从源码中可以看出，在计算新容量的时候，如果旧数组的容量小于64，新数组容量为旧容量的2倍➕2；反之，新数组容量的扩容系数为50%。

我们再来看看siftUp(i, e)这个方法，当插入的元素不是顶部位置，会进行内容排序调整，siftUp(i, e)方法就是起到这个作用，源码如下：
```
private void siftUp(int k, E x) {
	//如果使用比较器，采用比较器进行比较
    if (comparator != null)
        siftUpUsingComparator(k, x);
    else
		//没有比较器，采用自然排序
        siftUpComparable(k, x);
}
```
默认调整方式的实现，源码如下：
```
private void siftUpComparable(int k, E x) {
    Comparable<? super E> key = (Comparable<? super E>) x;
    while (k > 0) {
		//parentNo = (nodeNo-1)/2
        int parent = (k - 1) >>> 1;
        Object e = queue[parent];
		//默认自然排序，从小到大
        if (key.compareTo((E) e) >= 0)
            break;
        queue[k] = e;
        k = parent;
    }
    queue[k] = key;
}
```
自定义比较器的实现，调整方式，源码如下：
```
private void siftUpUsingComparator(int k, E x) {
    while (k > 0) {
		//parentNo = (nodeNo-1)/2
        int parent = (k - 1) >>> 1;
        Object e = queue[parent];
		//调用比较器的比较方法
        if (comparator.compare(x, (E) e) >= 0)
            break;
        queue[k] = e;
        k = parent;
    }
    queue[k] = x;
}
```
默认的插入规则中，新加入的元素可能会破坏小顶堆的性质，因此需要进行调整。

调整的过程为：从尾部下标的位置开始，将加入的元素逐层与当前点的父节点的内容进行比较并交换，直到满足父节点内容都小于子节点的内容为止。

当然，也可以依靠自定义比较器，实现自定排序规则。
3.1.2、add 方法
add方法，就比较简单了，直接调用了offer方法，返回false抛异常，源码如下：
```
public boolean add(E e) {
    if (offer(e))
        return true;
    else
        throw new IllegalStateException("Queue full");
}
```
3.1.3 使用方式
自然排序
```
public static void main(String[] args) {
    PriorityQueue<Integer> queue = new PriorityQueue<>();
    System.out.println("插入的数据");
    //随机添加两位数
    for (int i = 0; i < 10; i++) {
        Integer num = new Random().nextInt(90) + 10;
        System.out.print(num + ",");
        queue.offer(num);
    }

    System.out.println("\n输出后的数据");
    while (true){
        Integer result = queue.poll();
        if(result == null){
            break;
        }
        System.out.print(result + ",");
    }
}
```
输出结果：
```
插入的数据
53,97,66,58,69,10,72,27,18,16,
输出后的数据
10,16,18,27,53,58,66,69,72,97,
```
自定义排序
```
public static void main(String[] args) {
    PriorityQueue<Integer> customeQueue = new PriorityQueue<>(new Comparator<Integer>() {
        @Override
        public int compare(Integer o1, Integer o2) {
            //按照大到小排序
            return o2.compareTo(o1);
        }
    });
    System.out.println("插入的数据");
    //随机添加两位数
    for (int i = 0; i < 10; i++) {
        Integer num = new Random().nextInt(90) + 10;
        System.out.print(num + ",");
        customeQueue.offer(num);
    }

    System.out.println("\n输出后的数据");
    while (true){
        Integer result = customeQueue.poll();
        if(result == null){
            break;
        }
        System.out.print(result + ",");
    }
}
```
输出结果：
```
插入的数据
66,39,28,54,56,66,54,77,10,97,
输出后的数据
97,77,66,66,56,54,54,39,28,10,
```
3.2、删除方法
PriorityQueue 的删除方法有 2 种，分别是remove()和poll()，两者语义也完全相同，都是获取并删除队首元素，区别是当方法失败时前者抛出异常，后者返回null。由于删除操作会改变队列的结构，为维护小顶堆的性质，需要进行必要的调整。
3.2.1、poll 方法
poll 方法图解实现流程如下：
![poll 方法图解](/Week_01/doc/poll.jpg)
删除的元素可能会破坏小顶堆的性质，在 b、 c、d 三步会进行调整。

poll 方法的实现，源码如下：
```
public E poll() {
    if (size == 0)
        return null;
    int s = --size;
    modCount++;
	//0下标处的那个元素就是最小的那个
    E result = (E) queue[0];
    E x = (E) queue[s];
    queue[s] = null;
    if (s != 0)
		//调整
        siftDown(0, x);
    return result;
}
```
调整过程与插入的调整过程有些相反！

首先记录数组头部的下标，并用最后一个元素的内容替换数组头部的元素，之后调用siftDown()方法对堆进行调整，最后返回数组头部的元素。

siftDown(int k, E x)方法的实现，源码内容如下：
```
private void siftDown(int k, E x) {
	//判断是否有自定义比较器
    if (comparator != null)
        siftDownUsingComparator(k, x);
    else
        siftDownComparable(k, x);
}
```
与插入的调整类似，首先判断是否有自定义的比较器，如果没有，按照默认的方式进行调整，反之，根据自定义比较器的排序规则进行调整。

默认调整方式，函数siftDownComparable(k, x)，源码如下：
```
private void siftDownComparable(int k, E x) {
    Comparable<? super E> key = (Comparable<? super E>)x;
    int half = size >>> 1;        // loop while a non-leaf
    while (k < half) {
		//首先找到左右孩子中较小的那个，记录到c里，并用child记录其下标
        int child = (k << 1) + 1;
        Object c = queue[child];
        int right = child + 1;
        if (right < size &&
            ((Comparable<? super E>) c).compareTo((E) queue[right]) > 0)
            c = queue[child = right];
        if (key.compareTo((E) c) <= 0)
            break;
        queue[k] = c;//然后用c取代原来的值
        k = child;
    }
    queue[k] = key;
}
```
自定义调整方式，函数siftDownUsingComparator(k, x)，源码如下：
```
private void siftDownUsingComparator(int k, E x) {
    int half = size >>> 1;
    while (k < half) {
		//首先找到左右孩子中较小的那个，记录到c里，并用child记录其下标
        int child = (k << 1) + 1;
        Object c = queue[child];
        int right = child + 1;
        if (right < size &&
            comparator.compare((E) c, (E) queue[right]) > 0)
            c = queue[child = right];
        if (comparator.compare(x, (E) c) <= 0)
            break;
        queue[k] = c;//然后用c取代原来的值
        k = child;
    }
    queue[k] = x;
}
```
默认的删除调整中，首先获取顶部下标和最尾部的元素内容，从顶部的位置开始，将尾部元素的内容逐层向下与当前点的左右子节点中较小的那个交换，直到判断元素内容小于或等于左右子节点中的任何一个为止。

如果有自定义比较器，使用自定义比较器中的排序算法来进行交换。

思路是一样的，只是排序比较算法不一样而已！
3.2.2、remove 方法
remove 方法实现比较简单，直接调用了poll()方法，返回空值抛异常，源码如下：
```
public E remove() {
    E x = poll();
    if (x != null)
        return x;
    else
		//返回空值，抛异常
        throw new NoSuchElementException();
}
```
3.3、查询方法
PriorityQueue 的查询方法有 2 种，分别是element()和和peek()，两者语义也完全相同，都是获取但不删除队首元素，也就是队列中权值最小的那个元素，二者唯一的区别是当方法失败时前者抛出异常，后者返回null。

因为是数组结构，所以查询的时间复杂度log(1)，根据小顶堆的性质，堆顶那个元素就是全局最小的那个，直接返回数组下标为0即可返回队首元素！

3.3.1、peek 方法
peek 方法图解实现流程如下：
![peek 方法图解](/Week_01/doc/peek.jpg)
peek 方法实现，直接返回数组下标为0的元素，源码如下：
```
public E peek() {
    return (size == 0) ? null : (E) queue[0];
}
```
3.3.2、element 方法
element 方法实现也比较简单，直接调用了peek()方法，如果返回空值抛异常，源码如下：
```
public E element() {
    E x = peek();
    if (x != null)
        return x;
    else
		//返回空值，抛异常
        throw new NoSuchElementException();
}
```
##四、总结
在 Java 中 PriorityQueue 是一个使用数组结构来存储元素的优先队列，虽然它也实现了Queue接口，但是元素存取并不是先进先出，而是通过一个二叉小顶堆实现的，默认底层使用自然排序规则给插入的元素进行排序，也可以使用自定义比较器来实现排序，每次取出的元素都是队列中权值最小的。

同时需要注意的是，PriorityQueue 不能插入null，否则报空指针异常！
##五、参考
1、JDK1.7&JDK1.8 源码

2、知乎 - CarpenterLee -深入理解Java PriorityQueue


