# [剑指 Offer 05. 替换空格](https://leetcode.cn/problems/ti-huan-kong-ge-lcof/)

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

**示例 1：**

```
输入：s = "We are happy."
输出："We%20are%20happy."
```

**限制：**

```
0 <= s 的长度 <= 10000
```

## 解法

### 1. 借助API

```java
public String replaceSpace(String s) {
    return s.replaceAll(" ", "%20");
}
```

### 2. 借助数组

先遍历一遍字符串，确定空格的数量。这样就可以计算出结果字符数组的长度。然后从后向前遍历把每个字符串填入数组中，遇到空格则填充%20。使用StringBuilder进行拼接也是相同思路。

```java
public String replaceSpace(String s) {
    int count = 0;
    for (int i = 0; i < s.length(); i++) {
        if (s.charAt(i) == ' ') {
            count++;
        }
    }
    // 这里容易习惯性地 * 3
    char[] res = new char[s.length() + count * 2];
    int j = 0;
    for (int i = 0; i < s.length(); i++) {
        if (s.charAt(i) == ' ') {
            res[j++] = '%';
            res[j++] = '2';
            res[j++] = '0';
        } else {
            res[j++] = s.charAt(i);
        }
    }
    return new String(res);
}
```

### 3. 双指针

如下思路可以借鉴一下，在数组上原地调整，不如方法2好。

![替换空格](images/剑指Offer-05-1.gif)



