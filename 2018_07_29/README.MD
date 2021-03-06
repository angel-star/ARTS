# Algorithm


**题目描述：**



 涉及一个算法，对给定的一个整型m×n矩阵A，统计这个矩阵中具有下列特征的元素个数并输出它们的坐标及数值：它们既是所在行中的最小值，又死所在列中的最小值；或者它们既是所在行中的最大值，又是所在列中的最大值。假设矩阵中元素各不相同，要求结果在处理过程中用输出语句输出。
 
 
 
**解题思路：**

 需要找出某行上的最小值（最大值），然后判断其是否为对应列上的最小值（最大值），若是则输出。
 
 思路不是很复杂，但是过程看着比较繁琐，比较考研自己的逻辑能力
 
下面给出最普遍的做法的C++实现

```C++


void printmin(int A[][maxSize], int m, int n){
    int i, j, k, min, minj;
    //用minj来记录第i行上最小值的列号
    // min来记录当前行的最小值
    int flag; //用它来进行标注，当前元素是否符合输出的标准。
    for(i = 0; i < m; ++i){
        //找出第i行上的最小值，列号为minj
        min = A[i][0];
        minj = 0;
        for(j = 1; j<n; ++j){
            if(A[i][j]<min){
                min = A[i][j];
                minj = j;

            }
        }
        //进行到此时已经找出了本行最小的元素，并且已经记下了列数，但是还有个问题就是要验证一下这个元素是不是在本列也是最小，如果是，那么符合输出标准，如何不是，那么不符合，继续扫描下一行。
                
        flag = 1;
        for(k=0;k<m;++k){   //判断min是否为minj列上的最小值
            if(min>A[k][minj]){
                flag = 0;
                break;
            }
        }
        if(flag)
            cout<<min<<",["<<i<<","<<minj<<"]"<<"  ";
        //打印最小值，其格式为min, [i,minj]

    }
    cout <<endl;

}

    
void printmax(int A[][maxSize], int m, int n){
    //做法和上面是差不多的，其实可以放到一个循环里，只不过稍稍有点乱，理清一下思路再写就好啦。

    int i,j,k,max,maxj;
    int flag;
    for(i=0;i<m;i++){
        max = A[i][0];
        maxj=0;
        for(j=1;j<n;++j)
            if(A[i][j]>max)
            {
                max = A[i][j];
                maxj = j;
            }
        flag = 1;
        for(k=0;k<m;++k)
            if(max<A[k][maxj]){
            flag = 0;
            break;
        }
        if(flag)
            cout << max << ",[" << i << ", " << maxj << "]" << "  ";
        //打印最大值，其格式为max，[i,maxj]

    }
    cout <<endl;
}




```
# Review
【如何构造一个可以自主思考的机器（第二部分）】[How to make an idea machine, part two](https://towardsdatascience.com/how-to-make-an-idea-machine-part-two-24ba330508d6)




[在上周的 Review](https://github.com/angel-star/ARTS/tree/master/2018_07_22#review)的部分中作者定义了从数据中发现的概念，概述了发现过程目前是如何非常低效的，并提出了一个软件解决方案，用于自动化和加速跨所有行业的发现。


在diss了Excel，Tableau，SAS这几个软件后，吹嘘自己tag.cortex platform的平台，介绍它们是用的是专家领域的语言，这样可以把用户在使用过程中所表现出来的"惧怕犯错"降到最低。


剩下几部分作者分别介绍了自己的平台，谈了谈协议，和两个比较重要的问题：领域专家要深度理解得到的答案、平台必须要兼容任何数据源。

最后抛出了几个比较重要并没有讨论或者没有被解决的问题：

  
  - Using the tag.cortex platform as an API
  - Sharing of reports and collaboration between domain experts
  - Reproducibility of reports and analyses
  - Extending analysis functionality with the tag.algo SDK
  - Graph structures and sequences



# Technique


大数定律和中心极限定理很长，但是要表达的意思很简单。数学就这样，数学家要表达一个很简单的意思，但是为了严谨，他们写出来的公式就很长，很烦人。所以，对于这一章，要先从直观上了解个个定律的实际含义，再记公式。

先看大数定律：不管是什么样的随机变量，对于他们的样本均值，你所取得的样本容量n越大，你的样本均值就越接近总体均值。大数定律跟随的几个定律，伯努利大数定律和辛钦定理其实说的是一个意思，可以看做大数定律的具体描述。 区别在于，伯努利同志告诉我们，独立重复试验的随机变量符合大数定律。辛钦同志告诉我们，不要求独立重复试验，只要是独立同分布的随机变量，就能满足大数定律。所以伯努利大数定律是辛钦定律的特殊情况。辛钦同志更牛逼一些，看到了更一般的情况。


中心极限定理：对于一批随机变量，符合某种条件时，不管这些随机变量如何分布，他们的样本均值的分布就一定是正态分布！！！同样，这一节的所有定理都是在说这个问题，只是给定的限制条件不同，所以明白这些以后课本就比较好懂了。



# Share

> GitHub Awesome Big Data：大数据框架、论文等实用资源集合。
  
[纯碎coding：7个最常用的排序算法](https://mp.weixin.qq.com/s/rQ-dtjpzBfirysqdhsRUIg)

本篇文章介绍了7个常见的排序算法：

- 冒泡排序
- 快速排序
- 直接选择排序
- 堆排序
- 直接插入排序
- 希尔排序
- 归并排序


比较友好的一点就是文章开头定义了一下规范，防止大家语言不通或者有些地方看的不够清楚。





