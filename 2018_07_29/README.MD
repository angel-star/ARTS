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





