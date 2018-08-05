
# Algorithm

[461. Hamming Distance](https://leetcode.com/problems/hamming-distance/description/)

题目描述：

The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.

Note:
0 ≤ x, y < 2**31.


> 
>     Example:
>   
>   Input: x = 1, y = 4
>   
>   Output: 2
>    
>     Explanation:
>     1   (0 0 0 1)
>     4   (0 1 0 0)
>            ↑   ↑
>    
>     The above arrows point to positions where the corresponding bits are different.

 由描述可知，汉明距离（Hamming Distance）就是比较两个整数的二进制表示中，不同的位的总数。下面是AC的代码：
 
 
 
下面给出最普遍的做法的C++实现

```C++
#include<iostream>
#include<iomanip>
#include<cmath>
#include<string>
#include<cstring>
#include<cstdlib>
#include<climits>
#include<vector>

using namespace std;

int main(){
    int x,y;
    cout<<"Please input two integers:"<<endl;
    cin>>x>>y;
    /*算法1
    int a=x^y,answer=0;
    while(a!=0){
        answer++;
        a&=a-1;
    }
    */
    //算法二
    int answer=0;
    while(x!=y){
        answer+=(x&1)^(y&1);
        x>>=1; 
        y>>=1;
    }
    cout<<"Those two integers'' Hamming Distance is:"<<answer<<endl;
    return 0;
}


```



算法一是将x和y异或操作之后计算其中二进制中1的个数，其计算的方法是通过自身和自身减一的二进制数逐位相与，然后减一之后继续循环直至为0，这样也就将其二进制中1的个数计算出来；
算法二是将x和y的最后一位异或操作然后将其都右移一位以后再次计算其异或操作的和，直至两个数相等。


 从算法复杂度来看，两种算法的复杂度均为O(n)。

 整体来看，虽然实现方法不同，但两个算法都是通过异或操作计算其汉明距离，这也主要是由于汉明距离的定义所致。








# Review
[Python for data science : Part 1](https://towardsdatascience.com/python-for-data-science-part-1-759524eb493b)


本文简单介绍了python这门语言在数据科学中的使用，难度偏向入门

有如下内容

1. Python function

2. Data types and sequences

3. Date and time

4. Lambda

5. Map

6. Filter

7. Reduce

8. Zip

9. For loop

可以说还是比较基础的，下周会分享出来他关于本系列的最新的几个文章。



# Technique

在用python进行数据分析的过程中我们大多会选择jupyter(ipython)这个工具来进行，它比较方便。

但是在某些时候它显得不是那么好用，比如在用到matplotlib时，它就显得比较"僵"

这里就要引出我们今天的主角了



利用 Jupyter 交互式小部件框架，jupyter-matplotlib 可以在 Jupyter notebook 和 Jupyterlab 中实现 matplotlib 的交互功能。

此外，canvas 是一个合适的 Jupyter 交互式小部件，可以定位在交互部件的 Layout 上。

**Github 链接：**

https://github.com/matplotlib/jupyter-matplotlib

**用法：**

要启用 jupyter-matplotlib 后端，只需使用 matplotlib：

`%matplotlib widget`

**示例：**

![12334](https://github.com/matplotlib/jupyter-matplotlib/blob/master/matplotlib.gif)


下面是github地址，来个star支持下作者吧

[jupyter-matplotlib](https://github.com/matplotlib/jupyter-matplotlib)




# Share
今天的分享来自于云栖社区

  
[Tensorflow 分布式原理理解](https://yq.aliyun.com/articles/620563?spm=a2c4e.11157919.spm-cont-list.249.146c27aeUUOo3D)

在介绍了基本概念和运行机制后还给出了两个示例代码

示例代码1 自动节点分配策略----简单的贪婪策略代价模型估计
示例代码2 用户限制的节点分配策略
