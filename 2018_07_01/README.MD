
# ARTS
-----

- 每周至少做一个leetcode 的算法题，(Algorithm)
- 阅读并点评至少一篇英文技术文章，(Review)
- 学习至少一个技术技巧，(Technique)
- 至少分享一篇有观点和思考的技术文章。(Share)

# Algorithm

[1. Two Sum](https://leetcode.com/problems/two-sum/description/)

之前还想不用LeetCode了，后来做了下比较其他平台或者其它地方的题库都没有它做的好，所以还是用它吧。本周从第一题开始。过去做过的很多题都是用Python做的，现在用C++重新实现一遍。


下面给出C++实现

```C++
using namespace std;

class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> ns;

        for(auto i = 0;i < nums.size(); i++){
            for(auto y = i+1; y<nums.size(); y++){
                if(nums[i]+nums[y]==target){
                    ns.push_back(i);
                    ns.push_back(y);  
                    return ns;}
            }
        }
        
    }
};


}

````
Complexity Analysis:
- Time complexity: <a href="http://www.codecogs.com/eqnedit.php?latex=O(N^{2})" target="_blank"><img src="http://latex.codecogs.com/gif.latex?O(N^{2})" title="O(N^{2})" /></a>
 


- Space complexity:<a href="http://www.codecogs.com/eqnedit.php?latex=O(1)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?O(1)" title="O(1)" /></a>


另外一种方法：

```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> map;

        for (int i = 0; i < nums.size(); i ++) {
            auto it = map.find(target - nums[i]);

            if (it != map.end()) {
                return { i, it->second };
            }

            map[nums[i]] = i;
        }

        return { 0, 0 };        
    }
}; 



```

Complexity Analysis:
- Time complexity:<a href="http://www.codecogs.com/eqnedit.php?latex=O(N)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?O(N)" title="O(N)" /></a>
 


- Space complexity:<a href="http://www.codecogs.com/eqnedit.php?latex=O(N)" target="_blank"><img src="http://latex.codecogs.com/gif.latex?O(N)" title="O(N)" /></a>



# Review
【在"大公司"工作将会很有趣，除非……】[Working for a “Big Company” Can Be Fun, If . . .](https://hackernoon.com/working-for-a-big-company-can-be-fun-if-8eaf1eb560d9)

本文来自于斯坦福大学的一名软件工程师。


作者首先指出了小公司比大公司有更多的发展机会，相比之下如果大公司想要摒弃这些弊端，就需要构建一个"智能平台"（Intelligent Platform）

并在定义Intelligent Platform后，给出四个重要的组成要素，分别是：可靠的技术、充分的沟通、正确的价值观与具有创新精神的领导力


关键词：Intelligent Platform  


# Technique


大家可能对top监控软件比较熟悉，今天我为大家介绍另外一个监控软件Htop，姑且称之为top的增强版，相比top其有着很多自身的优势。如下：

这是最近室友推荐给我的神器，今天推荐给大家：


- 两者相比起来，top比较繁琐
- 默认支持图形界面的鼠标操作
- 可以横向或纵向滚动浏览进程列表，以便看到所有的进程和完整的命令行
- 杀进程时不需要输入进程号等
- htop 支持鼠标操作。


官网：[请点击这里](http://hisham.hm/htop/)

顺便说一句，目前最新的版本是：2.2.0.

安装命令：
> yum install htop 

或

> apt-get install htop 

 MAC端可以用
 > brew install htop
 
 

# Share

在初步接触机器学习的时候，对于已经学过线性代数很多年的我们往往会在最开始的地方卡住——PCA，特征值分解……

于是我极力推荐大家读一下下面这篇文章

[特征值分解、奇异值分解、PCA概念整理](https://blog.csdn.net/jinshengtao/article/details/18448355)

这篇文章介绍了这几个名词并给出了相应的代码示例，相信会对大家有所启发。
