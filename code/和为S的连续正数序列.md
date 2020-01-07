#### 和为S的连续正数序列

##### 题目描述

小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck!

<!--more-->

##### 法一：暴力的话就不说了，双循环，时间复杂度为O(n^2)，你要只会这个，这道题就代表你不会做。这一题采用双指针技巧，真是很妙，如果当前窗口的和大于sum，左边界+1，如果当前窗口的和小于sum，右边界+1，如果等于直接插入到结果数组。

```java
public ArrayList<ArrayList<Integer>> FindContinuousSequence(int sum) {
    if (sum <= 2) {
        return new ArrayList();
    }
    int left = 1, right = 2;
    ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
    ArrayList<Integer> window = new ArrayList<>();
    window.add(left);
    window.add(right);
    //当前窗口的和
    int curWindowSum = left + right;
    while (left < right) {
        if (curWindowSum < sum) {
            window.add(++right);
            //加上新的右边界
            curWindowSum += right;
        } else if (curWindowSum > sum) {
            window.remove(0);
            //减去原来的原边界
            curWindowSum -= left;
            left++;
        } else {
            //这一步很关键，java中的arraylist是引用类型，你要直接插入window，后期window的改动，会影响你之前插入的window的值，是会变的！
            ans.add(new ArrayList<>(window));
            window.remove(0);
            //减去原来的原边界
            curWindowSum -= left;
            left++;
        }
    }
    return ans;
}
```

这一题本质上来说有点类似滑动窗口的感觉，使用双指针（这个trick十分的巧妙，能提高时间量级）