## 买卖股票的最佳时机
### [121. 买卖股票的最佳时机-easy](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入股票前卖出股票。

示例 1:
```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。
```
示例 2:
```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int temp=0,maxp=0;
        for(int i=1;i<prices.size();i++)
        {
           temp=prices[i]-prices[i-1]+temp<0?0:prices[i]-prices[i-1]+temp;
            maxp=max(maxp,temp);
        }
        return maxp;
    }
};
```

### [122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

示例 1:
```
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。
```
示例 2:
```
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```
示例 3:
```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```
```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int temp=0,maxp=0,maxsum=0,flag=0;
        for(int i=1;i<prices.size();i++)
        {
            if(prices[i]>=prices[i-1])
            {
                maxp=prices[i]-prices[temp];
                flag=1;
            }
            
            else
            {
                temp=i;
                if(flag==1)
                    maxsum+=maxp;
                flag=0;
            }
        }
        if(flag==1)
            maxsum+=maxp;
        return maxsum;
    }
};
```


[123. 买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)
给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 两笔 交易。

注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

示例 1:
```
输入: [3,3,5,0,0,3,1,4]
输出: 6
解释: 在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
     随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。
```
示例 2:
```
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。   
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。   
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。
```
示例 3:
```
输入: [7,6,4,3,1] 
输出: 0 
解释: 在这个情况下, 没有交易完成, 所以最大利润为 0。
```

**思路**:
[买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/solution/yi-ge-fang-fa-tuan-mie-6-dao-gu-piao-wen-ti-by-l-3/)
dp

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.empty())
            return 0;       
        vector<vector<vector<int>>> dp(prices.size(),vector<vector<int>>(3,vector<int>(2,0)));  
        for(int i = 0 ; i <= 2;++i){
            dp[0][i][0] = 0;
            dp[0][i][1] = -prices[0];
        }
        
        for(int i = 1 ; i < prices.size();++i){
            for(int j = 2 ; j >= 1;--j){
                dp[i][j][0] = max(dp[i-1][j][0],dp[i-1][j][1] + prices[i]);
                dp[i][j][1] = max(dp[i-1][j][1],dp[i-1][j-1][0] - prices[i]); 
            }
        }  
        return dp[prices.size()-1][2][0];
    }
};
```


[188. 买卖股票的最佳时机 IV](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/)
给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你最多可以完成 k 笔交易。

注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

示例 1:
```
输入: [2,4,1], k = 2
输出: 2
解释: 在第 1 天 (股票价格 = 2) 的时候买入，在第 2 天 (股票价格 = 4) 的时候卖出，这笔交易所能获得利润 = 4-2 = 2 。
```
示例 2:
```
输入: [3,2,6,5,0,3], k = 2
输出: 7
解释: 在第 2 天 (股票价格 = 2) 的时候买入，在第 3 天 (股票价格 = 6) 的时候卖出, 这笔交易所能获得利润 = 6-2 = 4 。
     随后，在第 5 天 (股票价格 = 0) 的时候买入，在第 6 天 (股票价格 = 3) 的时候卖出, 这笔交易所能获得利润 = 3-0 = 3 。
```

**思路**：相当于III里面2->k
注意考虑k太大超时情况：
```c++
 if(k>=prices.size()/2) 
            return process(prices);
            
  int process(vector<int>& prices)
    {
    int res=0;
    for(int i=1;i<prices.size();i++){
        if(prices[i]>prices[i-1])res+=prices[i]-prices[i-1];
    }
    return res;
```

```c++
class Solution {
public:
    int process(vector<int>& prices)
    {
    int res=0;
    for(int i=1;i<prices.size();i++){
        if(prices[i]>prices[i-1])res+=prices[i]-prices[i-1];
    }
    return res;
} 
    
    int maxProfit(int k, vector<int>& prices) {
       
         if(prices.empty())
            return 0; 
        if(k>=prices.size()/2) 
            return process(prices);
        
        int len=int (prices.size());
        int dp[len][k+1][2];
        for(int i = 0 ; i <= k;++i){
            dp[0][i][0] = 0;
            dp[0][i][1] = -prices[0];
        }
        for(int i=0;i<prices.size();i++)
            dp[i][0][0]=0;
        
        for(int i=1;i<prices.size();i++)
            for(int j=1;j<=k;j++)
            {dp[i][j][0]=max(dp[i-1][j][0],dp[i-1][j][1]+prices[i]);
                dp[i][j][1]=max(dp[i-1][j][1],dp[i-1][j-1][0]-prices[i]);}
        return dp[prices.size()-1][k][0];
   
    }
};
```





