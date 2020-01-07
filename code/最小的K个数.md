#### 最小的K个数

##### 题目描述

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。

<!--more-->

##### 法一：排序的我就不说了，直接调sort，时间复杂度为O(nlogn)。我的最开始的想法，就是维护一个K长度的大根堆，如果下一个数字比堆顶（最大的数字小），那就将堆顶删除，当前数字入堆，大根堆使用优先队列（最大的先出队）。但是这样，因为插入到优先队列的时间复杂度是logk，所以这种方法也并没有提升到O(n)的性能，最终时间复杂度为O(nlogk)。

```java
public ArrayList<Integer> GetLeastNumbers_Solution(int [] input, int k) {
    if (input == null || input.length == 0 || input.length < k || k <= 0) {
        return new ArrayList<Integer>();
    }
    Queue<Integer> maxHeap = new PriorityQueue<>(new Comparator<Integer>() {
        @Override
        public int compare(Integer a, Integer b) {
            return b - a;
        }
    });
    ArrayList<Integer> ans = new ArrayList<>();
    for (int i = 0; i < input.length; i++) {
        if (maxHeap.size() < k) {
            maxHeap.offer(input[i]);
            ans.add(input[i]);
        } else if (maxHeap.peek() > input[i]) {
            ans.remove(maxHeap.peek());
            maxHeap.poll();
            maxHeap.offer(input[i]);
            ans.add(input[i]);
        }
    }
    return ans;
}
```

小结：

这一题主要考察各种排序，方法，通过这一题，最好将各种排序方法实现，并且非常熟悉个排序算法的时间复杂度。