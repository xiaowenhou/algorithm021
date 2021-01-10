**不同路径II**

**题目：**

**解法一：动态规划 ， 额外定义DP数组**

子结构：

状态数组：从起点到i，j点的路径和

dp方程： 

如果某点是障碍物，那么到该点的路径为0

if (obstacleGrid[i,j] == 1)

​	dp[i,j] = 0;  

如果i == 0， 则dp[i,j] = dp[i, j - 1];

如果j == 0,    则dp[i,j] = dp[i - 1, j];

一般情况

​    dp[i,j] = dp[i - 1, j] + dp[i, j -1]

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int[][] dp = new int[obstacleGrid.length][obstacleGrid[0].length];

        for (int i = 0; i < obstacleGrid.length; i++) {
            for (int j = 0; j < obstacleGrid[0].length; j++) {
                if (obstacleGrid[i][j] == 1) {
                    dp[i][j] = 0;
                    continue;
                }
                
                if (i == 0 && j == 0) {
                    dp[i][j] = 1;
                } else if (i == 0) {
                    dp[i][j] = dp[i][j - 1];
                } else if (j == 0) {
                    dp[i][j] = dp[i - 1][j];
                } else {
                    dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
                }
            }
        }
        
        return dp[obstacleGrid.length - 1][obstacleGrid[0].length - 1];
    }
}
```

时间复杂度：O（mn），m和n分别为obstacleGrid的行和列长

空间复杂度：O（mn）

解法二：动态规划，不使用额外的数组，直接用原数组当作状态数组

```java
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        for (int i = 0; i < obstacleGrid.length; i++) {
            for (int j = 0; j < obstacleGrid[0].length; j++) {
                if (obstacleGrid[i][j] == 1) {
                    obstacleGrid[i][j] = 0;
                } else if (i == 0 && j == 0) {
                    obstacleGrid[i][j] = 1;
                } else if (i == 0) {
                    obstacleGrid[i][j] = obstacleGrid[i][j - 1];
                } else if (j == 0) {
                    obstacleGrid[i][j] = obstacleGrid[i - 1][j];
                } else {
                    obstacleGrid[i][j] = obstacleGrid[i - 1][j] + obstacleGrid[i][j - 1];
                }
            }
        }
        return obstacleGrid[obstacleGrid.length - 1][obstacleGrid[0].length - 1];
    }
}
```

时间复杂度：O（mn）

空间复杂度：O（1）