
# Algorithm

[637. Average of Levels in Binary Tree](https://leetcode.com/problems/average-of-levels-in-binary-tree/description/)

- 分析:定义一个map,层数作为key,value保存每层的元素个数和所有元素的和,遍历这个树,把map里面填值,遍历结束后,再遍历这个map,把每层的平均数放到数组里,最后数组转为list返回,不用考虑list里的排序了.

下面给出java实现

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        
        Map<Integer, TreeLevel> store = new HashMap<>();
        init(root, store, 1);
        Double[] arr = new Double[store.size()];
        for (Map.Entry<Integer, TreeLevel> entry : store.entrySet()) {
            arr[entry.getKey() - 1] = entry.getValue().getAverage();
        }
        return Arrays.asList(arr);
    }
    
    void init(TreeNode root, Map<Integer, TreeLevel> store, int level) {
        if (root == null) return;
        TreeLevel treeLevel = store.get(level);
        if (treeLevel == null) {
            treeLevel = new TreeLevel();
            store.put(level, treeLevel);
        }
        treeLevel.count++;
        treeLevel.sum+=root.val;
        init(root.left, store, level+1);
        init(root.right, store, level+1);
    }
    
    // 定义一个类存储每一层的信息
    class TreeLevel {
        int count; // 该层有多少元素
        double sum; // 该层所有元素的和,这个要用double类型来保存,eg:[2147483647,2147483647,2147483647]
        
        // 返回该层的平均数
        Double getAverage() {
            return sum / count;
        }
    }
}

```





# Review
【Kaggle与开源数据集】[Open Source Datasets with Kaggle
](http://blog.kaggle.com/2018/06/21/open-source-datasets-with-kaggle/)

本文来自于斯坦福大学的一名软件工程师。


文章开篇作者给出了一般情况下数据集在被采用的整个过程（“sharing operation” ）
![](http://s5047.pcdn.co/wp-content/uploads/2018/06/IMAGE-A-1184x126.png)

作者指出了其中存在的些许问题并提出她在本篇文章中虽然没有成熟的生产解决方案可以分享，但是会展示出入以kaggle数据集的形式来共享数据，在文章后面他逐步优化了上面的步骤并提出了自己的思路。

其实本文更像是一个广告，他在本文后面着重宣传了一下他们（实验室）需要的工程师和协作平台的各种需求。


关键词：kaggle  数据共享


# Technique

下面分享一道链表操作题

- 题目描述：

A和B是两个单链表（带表头结点），其中元素递增有序。设计一个算法，将A和B归并成一个按元素值非递减有序的链表C，C由A和B中的结点组成。

- 题目分析：

已知A和B中的元素递增有序，要使归并后的C中的元素依然有序，可以从A、B中的所有蒜素都插入到C中时，C一定是有递增有序的。** 很明显 ，由于A、B是递增的，因此A中的最小元素是其开始结点中的元素，B也一样。只需从A、B的开始结点中选出一个较小的来插入C的尾部即可。** 这里还需注意，A和B中的元素有可能一个已经全部被插入到C中，另一个还没有插完，如A中所有元素已经全部被插入到C中，而B还没有插完，这说明B中的所有元素都大于C中的元素，因此只要将将B链接到C的尾部即可。如果A没有插完，则用类似的方法来解决。

- 代码实现：


```c++
#include<iostream>
#define N 50
using namespace std;
typedef struct LNode
{
    int data;
    struct LNode *next;

} LNode;

void merge(LNode * A, LNode *B, LNode  *&C )
{
    LNode * p = A->next;
    LNode *q = B->next;
    LNode *r;
    C = A;
    C->next = NULL;
    free(B);
    r = C;
    while (p != NULL && q != NULL)
    {
        if (p->data <= q->data)
        {
            r = r->next;
        }
        else
        {
            r->next = q;
            q = q->next;
            r = r->next;
        }
    }
    r->next = NULL;
    if (p != NULL) r->next = p;
    if (q != NULL) r->next = q;
}
``` 


- 总结：

本题主要涵盖了两个知识点：一个是尾插法简历单链表；另一个是单链表的归并操作。



# Share

最近在用sublime发现了一个不错的简书作者，里面关于它有很多插件的介绍，在这里分享给大家。

[Sublime Text：学习资源篇](https://www.jianshu.com/p/d1b9a64e2e37)

[Sublime插件：增强篇](https://www.jianshu.com/p/5905f927d01b)

[Sublime插件：Markdown篇](https://www.jianshu.com/p/aa30cc25c91b)

[Sublime插件：C语言篇](https://www.jianshu.com/p/595975a2a5f3)

[Sublime插件：主题篇](https://www.jianshu.com/p/13fedee165f1)

[Sublime插件：Git篇](https://www.jianshu.com/p/3a8555c273d8)

[Sublime 小技巧：文本自动换行显示？](Sublime 小技巧：文本自动换行显示？)

[Sublime插件：Markdown篇](https://www.jianshu.com/p/aa30cc25c91b)
