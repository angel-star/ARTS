## Algorithm

#### description

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string s, int numRows);
```

**Example 1:**

```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

**Example 2:**

```
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```

#### solution

```
class Solution {
    public String convert(String s, int numRows) {

        // when numRows equal 1,return s
        if(numRows==1)
            return s;

        // init string array for result
        List<StringBuilder> retList = new ArrayList<StringBuilder>();
        for (int i = 0; i < Math.min(numRows, s.length()); i++)
            retList.add(new StringBuilder());

        int len = s.length();
        int step = 1;
        int row = 0;


        for(int i = 0 ; i <len ; i++){
            if(row == 0)
                step = 1;
            if(row == numRows-1)
                step = -1;

            retList.get(row).append(s.charAt(i));

            row+=step;
        }

        StringBuilder ret = new StringBuilder();
        for (StringBuilder sb : retList) 
            ret.append(sb);
        return ret.toString();
           
    }
}
```


## Technique

[3分钟理解 支持向量机中最出神的第一笔](https://mp.weixin.qq.com/s?__biz=MzI3NTkyMjA4NA==&mid=2247485836&idx=1&sn=222020f04cc36452f253eb8ae497656e&chksm=eb7c2447dc0bad512ad91633b06e4cfa85c3b359fae9167475734f0dc6b9fff16bb29ba4cd67&scene=21#wechat_redirect)

本周给大家分享这篇文章，为下周的分享做一下铺垫：
如何理解SVM的目标函数和约束怎么得来的思路。

如果看完这些内容后还可以再自行搜索下以下关键名词，方便我们下周进行理解支持向量机(SVM)

*拉格朗日乘子法，KKT条件，线性和非线性的核函数*


# Review
[Python for data science : Part 3](https://towardsdatascience.com/python-for-data-science-part-3-be9b08660af9)


本文简单介绍了python这门语言在数据科学中的使用，难度偏向入门,本文章和上周分享的 Review 属于同一系列，属于第三部分

本篇文章主要介绍了下面的内容 

1. Pandas Series
2. Querying a Pandas Series
3. Pandas Dataframe
4. Read and write files
5. Indexing Dataframes
6. Merging dataframes
7. Aggregate function
8. Filtering Dataframes


本章内容大体上简述了pandas库的数据结构与基本用法，现在回头看看感觉本系列有点仿照《利用python进行数据分析》一书。。

# Share

比特(bit)是计算机中数据量的单位，也是信息论中使用的信息量的单位。英文字bit来源于binary digit，意思是一个“二进制数字”，因此一个比特就是二进制数字中的一个1或0。
网络技术中的速率指的是连接在计算机网络上的主机在数字信道上传送数据的速率，它也称为数据率(data rate)或比特率(bit rate)。
速率是计算机网络中最重要的一个性能指标。速率的单位是b/s(比特每秒)(或bit/s，有时也写为bps，即bit per second)。当数据率较高时，就可以用kb/s(k = 10^3 = 千)、Mb/s(M = 10^6 = 兆)、Gb/s(G = 10^9 = 吉)或Tb/s(T=10^12=太)，不同于计算机领域中的1Kb=1024b、1Mb=1024Kb、1Gb=1024Mb、1Tb=1024Gb 。
现在人们常用更简单的并且是很不严格的记法来描述网络的速率，如100M以太网，而省略了单位中的b/s，它的意思是速率为100Mb/s的以太网。顺便指出，上面所说的速率往往是指额定速率或标称速率 。
