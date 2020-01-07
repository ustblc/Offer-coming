#### 和为S的两个数字

##### 题目描述

输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。

<!--more-->

##### 法一：这一题和leetcode上的Two Sum完全一样，只不过这一题还伪装了一下，让我们输出两个数乘积最小的（其实乘积最小的就是位于外围的两个数），你可以证明一下，设左边小的数为m，右边大的数为n，那么它们内部的乘积为(m+1)*(n-1) = nm + n - m - 1，原来的是nm，所以我们只需要观察(n - m - 1)，别忘了我们的前提，n > m，所以(n - m - 1)≥0的，当n=m+1的时候等号成立，此时没有内部，所以外围乘积一定是小于内部乘积的。那么因为是有序的，所以直接本能的想到双指针（二分），如果这两个数之和>sum，右边界-1，反之左边界+1，相等时插入到结果数组即可。

```java
public ArrayList<Integer> FindNumbersWithSum(int [] array,int sum) {
    if (array == null || array.length == 0) {
        return new ArrayList();
    }
    ArrayList<Integer> ans = new ArrayList<>();
    int l = 0, r = array.length - 1;
    while (l < r) {
        int curSum = array[l] + array[r];
        if (curSum == sum) {
            ans.add(array[l]);
            ans.add(array[r]);
            break;
        } else if (curSum > sum) {
            r--;
        } else {
            l++;
        }
    }
    return ans;
}
```

又是一道双指针的题目，很经典，尤其是"乘积最小的这一伪装"！

