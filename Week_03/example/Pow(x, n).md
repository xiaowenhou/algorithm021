**Pow(x, n)**

**题目:** 实现 pow(x, n) ，即计算 x 的 n 次幂函数.

**解法一:** 递归

```java
class Solution {
    public double myPow(double x, int n) {
        //将参数转化为long类型, 因为当n = Integer.MIN_VALUE, -n的值还是Integer.MIN_VALUE
        long param = n;
        return myPow(x, param);
    }

    private double myPow(double x, long n) {
        if (n == 0) {
            return 1;
        }
        x = n > 0 ? x : 1 / x;
        n = n > 0 ? n : -n;
        return n % 2 == 0 ? myPow(x * x, n/2) : x * myPow(x * x, n/2);
    }
}
```

时间复杂度: O(logn)

空间复杂度:O(logn)



**解法二: 迭代**

```java
class Solution {
    public double myPow(double x, int n) {
        long m = n;

        x = m > 0 ? x : 1 / x;
        m = m > 0 ? m : -m;
        double result = 1.0;
        while (m > 0) {
            result = (m & 1) == 1 ? result * x : result;
            x *= x;
            m /= 2;
        }
        return result;
    }
}
```

时间复杂度: O(logn)

空间复杂度: O(1)