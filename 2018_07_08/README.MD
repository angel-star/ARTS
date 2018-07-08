
# Algorithm

[771. Jewels and Stones](https://leetcode.com/problems/jewels-and-stones/description/)

题目描述：
You're given strings J  representing the types of stones that are jewels, and S representing the stones you have.  Each character in S is a type of stone you have.  You want to know how many of the stones you have are also jewels.

The letters in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive, so "a" is considered a different type of stone from "A".

Example 1: 

> Input: J = "aA", S = "aAAbbbb"
> Output: 3
  
Example 2:

>Input: J = "z", S = "ZZ"
 Output: 0
 
 Note:
 
 S and J will consist of letters and have length at most 50.
 The characters in J are distinct.
 
 
下面给出最普遍的做法的C++实现

```C++
class Solution {
public:
    int numJewelsInStones(string J, string S) {
    int u=0;
        for(int i=0;i<J.length();i++)
        {
            for(int k=0;k<S.length();k++)
            {
                if(S[k]==J[i])
                {
                    u++;
                }
            }
        }
        return u;
    }
};


```

下面是本题的最优解（在leetcode中100%）



```C++
class Solution {
public:
    int numJewelsInStones(string J, string S) {
        int count = 0;
        for(char &c:S){
            if(J.find(c)!=string::npos)
                count++;
        }
        return count;
    }
};
}

````

```c++
class Solution {
public:
    int numJewelsInStones(string J, string S) {
        set<char> jewels;
        for (char j : J) {
            jewels.insert(j);
        }
        
        int num_jewels = 0;
        for (char s : S) {
            if (jewels.find(s) != jewels.end())
                num_jewels++;
        }
        
        return num_jewels;
    }
};

```



# Review
【KMP算法之我见】[The Knuth-Morris-Pratt Algorithm in my own words](http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/)


本文内容概要：

> "I’m not going to explain why it’s more efficient than na”ive string matching; that’s explained perfectly well in a multitude of places. I’m going to explain exactly how it works, as my brain understands it."

本文通过三个部分向大家展示了它对KMP算法的理解：

- 部分匹配表

- 部分匹配表是如何得出的

- 结论

** 对于数据结构基础薄弱的同学或者字符串方面的相关知识点已经遗忘的人建议好好读一下本篇文章 **


关键词：Knuth-Morris-Pratt Algorithm, KMP, The Partial Match Table
 


# Technique

最近在刷leetcode的时候经常遇到的情况就是会卡在一个题中一个多小时没有思路，或者说有了一个答案但并不是最优解，这时候是否应该去看答案的问题。

在网上有同学问出了同样的问题：
> 大家好,
  小弟我這週開始刷題,我發現很多 Medium 級別的題目我想了大概5個小時都想不出解答,
  看了解答真心覺得我要自己想出解法可能至少要折騰個10幾小時,感覺真的沒效率阿..
  很多題的解法都很巧妙,沒做過實在想不出來 
  可是如果是看解答而非自己做出來的,那就淪為背解答了...
  求問各位大神剛開始刷leetcode時該用什麼策略來達到最大的學習效率?
  
然后下面有个答案说的特别好，分享给大家，希望在算法的道路上越走越远。

> 个人建议，你先自己全力想一下，但是时间不要超过以半小时。如果半小时之内甚至没有一点点思路，就先扫一眼Leetcode讨论区。讨论区里满是诸如“Share my 10-line Java DP solution, O(N^2)”的标题。这等于是给了DP和O(N^2)运行时间两个提示，然后再用半小时，看在这个提示下能想出多少。这一小时过完，如果已经有明确的思路，就先写出代码。如果还是没有明确的答案，那么马上看别人的解答。即使自己写出来了，也要去看高手的解法，找差距。

> “背解答”并非不好的事情。你现在处于原始积累阶段，正需要看的大量解答。学写程序其实和学写诗文是差不多的道理，古人为什么写诗又快又好？因为他们脑中有大量的现成的片段，对仗关系等等，所以说出上句马上就能接出下句。如果你见过大量的优秀代码，你就会对在什么场景下该怎么写这件事有更深的认识，遇到问题就能够更快地解决。


 
 

# Share

> 当训练数据词表增大到成百上千万时，如果不做任何剪枝处理，深度学习模型可能会拥有上百亿、甚至是几千亿个参数。
  
> 为了提高深度学习模型的训练效率，减少训练时间，我们普遍会采用分布式技术来执行训练任务——同时利用多个工作节点，分布式地、高效地训练出性能优良的神经网络模型。分布式技术是深度学习技术的加速器，能够显著提高深度学习的训练效率、进一步增大其应用范围。

[分布式深度学习新进展：让“分布式”和“深度学习”真正深度融合
](https://mp.weixin.qq.com/s?__biz=MzAwMTA3MzM4Nw==&mid=2649444062&idx=1&sn=53cf03f9930f62f62cb71aead6a8b242&chksm=82c0a75ab5b72e4c0601476c168e69e2ee7313871e1ce1bcf600f86886253841447b14e4868f&scene=38#wechat_redirect)

