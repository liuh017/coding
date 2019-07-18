## 题目：给出一个元素无序的数组，求出一个数，使得其左边的数都小于它，右边的数都大于等于它。

举例：2,2,3,1,4,7,5,6 返回下标4（数字为4）。

### 思路（1）：

朴素算法，对于每一个数，都检测它的左边和右边是否满足题意。

时间复杂度为O（n^2）

### 思路（2）

使用变量求解：

（1）目前找到符合题意的候选值，nCandid

（2）目前已遍历数组的最大值，nMax：为了选下一次的候选值

（3）目前的候选值是否有效，flag：检测是否需要重新选择候选值

思路：如果候选值有效，可以继续遍历下面的数据

如果候选值小于目前的值，则该候选失效。之后遍历元素时，就要重新选择候选值

选择候选值时，对于某一个元素，如果该元素比之前遍历过元素的最大值还要大nMax，则该元素就为候选。

复杂度：遍历一遍数组即可，时间：O（n），空间O（1）

```c++
#include <iostream>
#include <stack>
using namespace std;
int FindNum(int nArr[],int nLen)
{
    int flag=1;
    int nmax=nArr[0];
    int ncandidate=nArr[0];
    int npos=0;
    
    for (int i=1; i<nLen; i++) {
        //cout<<"flag"<<flag<<endl;
        if (flag==1) {
            if (ncandidate>nArr[i]) {
                flag=0;
            }
            else
            {
                nmax=nArr[i];
            }
        }
        else
        {
            if (nArr[i]>=nmax) {
                flag=1;
                nmax=nArr[i];
                npos=i;
                ncandidate=nArr[i];
            }
        }
        }
    return flag? npos:-1;
}
int main(int argc, const char * argv[]) {
    int nArr[8]= {2,2,3,1,4,7,5,6};
    cout<<FindNum(nArr, 8);
}

```

