#### 包含min函数的栈

##### 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

<!--more-->

##### 法一：我们看到得到最小元素的min函数要求时间复杂度是O(1)，所以我们只能借助一个辅助栈来实现（可能你会想，每次push的时候，将栈中所有元素取出来，找个最小值，pop的时候，再取出来，找个最小值，（这个最小值是全局变量）虽然说这样也行，min函数时间复杂度也是O(1)，但是时间开销在push和pop的过程中会很大，不是很好）。所以我们可以借助 一个单调栈来实现，栈顶永远是最小的一个，并且push和pop也是O(1)级别的。

```java
Deque<Integer> stack = new LinkedList<>();
Deque<Integer> minStack = new LinkedList<>();
public void push(int node) {
    stack.push(node);
    //我们只有在node的数值比当前最小栈（从栈顶单调递增）栈顶元素小的时候，才入栈。
    if (minStack.isEmpty() || minStack.peek() > node) {
        minStack.push(node);
    }
}

public void pop() {
    if (!stack.isEmpty()) {
        //这里要注意，删除栈顶元素的时候，一定要判断删除的元素是不是当前的最小元素，如果是，需要更新。
        if (!minStack.isEmpty() && minStack.peek().equals(stack.peek())) {
            minStack.pop();
        }
        stack.pop();
    }
}

public int top() {
    if (!stack.isEmpty()) {
        return stack.pop();
    } else {
        throw new RuntimeException("Stack is empty!");
    }
}

public int min() {
    if (!minStack.isEmpty()) {
        return minStack.peek();
    } else {
        throw new RuntimeException("Stack is empty!");
    }
}
```

##### 法二：另外一种方法，也是维护一种单调栈，只不过有个小技巧，可以保持最小栈和正常栈同样的大小，细节看代码。

```java
Deque<Integer> stack = new LinkedList<>();
Deque<Integer> minStack = new LinkedList<>();
public void push(int node) {
    stack.push(node);
    //如果node比当前最小栈栈顶元素小，就入栈，否则将栈顶元素再次入栈。
    if (minStack.isEmpty() || minStack.peek() > node) {
        minStack.push(node);
    } else {
        minStack.push(minStack.peek());
    }
}

public void pop() {
    if (!stack.isEmpty() && !minStack.isEmpty()) {
        minStack.pop();
        stack.pop();
    }
}

public int top() {
    if (!stack.isEmpty()) {
        return stack.pop();
    } else {
        throw new RuntimeException("Stack is empty!");
    }
}

public int min() {
    if (!minStack.isEmpty()) {
        return minStack.peek();
    } else {
        throw new RuntimeException("Stack is empty!");
    }
}
```

小结：

单调栈的使用，单调队列的使用，都是一个小trick，需要掌握，这在我们求解最值问题是，是很可能会用到的优化时间的结构。