
# Algorithm

[804. Unique Morse Code Words](https://leetcode.com/problems/unique-morse-code-words/description/)

题目描述：

International Morse Code defines a standard encoding where each letter is mapped to a series of dots and dashes, as follows: "a" maps to` ".-"`, `"b"` maps to` "-..."`, `"c" `maps to `"-.-."`, and so on.


For convenience, the full table for the 26 letters of the English alphabet is given below:

> [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."]

ow, given a list of words, each word can be written as a concatenation of the Morse code of each letter. For example, "cab" can be written as "-.-.-....-", (which is the concatenation "-.-." + "-..." + ".-"). We'll call such a concatenation, the transformation of a word.

Return the number of different transformations among all words we have.

> Example:
  Input: words = ["gin", "zen", "gig", "msg"]
  Output: 2
  Explanation: 
  The transformation of each word is:
  "gin" -> "--...-."
  "zen" -> "--...-."
  "gig" -> "--...--."
  "msg" -> "--...--."
   There are 2 different transformations, "--...-." and "--...--.".
   

Note:

The length of `words` will be at most `100`.
Each `words[i]` will have length in range `[1, 12]`.
`words[i]` will only consist of lowercase letters.
  
  

 
 
下面给出最普遍的做法的C++实现

```C++
class Solution {
public:
    string morses[26] = {".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--.."};//keep morse code for letter from a-z
    int uniqueMorseRepresentations(vector<string>& words) {
        unordered_set<string> setW;//morse code set from words
        for(auto w : words){
            int n = w.size();
            string s = "";//store morse code for a word
            for(auto c : w) s += morses[c-'a'];
            setW.insert(s);
        }
        return setW.size();
    }
};


```


在内部，unordered_set中的元素不是按照任何特定的顺序排序的，而是根据它们的哈希值来组织成桶，以便通过它们的值直接访问单个元素(平均时间复杂度为常数)。
所以它比普通的`set`速度要快，
[http://www.cplusplus.com/reference/unordered_set/unordered_set/](http://www.cplusplus.com/reference/unordered_set/unordered_set/)

这道题提高效率的地方主要在于两点：

1.利用char字符型的'a'快速定位ASCII

2.要学会用容器进行快速去重。









# Review


# Technique

室友发了一个关于"if怪"的图片，表示在交接代码时受不了同事了，然后另一个室友发出了自己的代码，表示自己其实就是一个"if怪"、
![123](https://github.com/angel-star/ARTS/blob/master/2018_07_22/QQ20180720-0.jpg)
于是我建议他用如下方法
![12334](https://github.com/angel-star/ARTS/blob/master/2018_07_22/QQ20180720-151738%402x.png)

就轻松解决了，调用的时候可以直接用key对字典进行索引，这样一来方便向反转前的字典中加入新的`key`或`value`，方便维护又美观。

另外关于字典反转，看到了下面几个文章，比较不错，虽然没有用到，但是希望以后有时间回过头看看。

[Python反转/反转映射](http://bbs.bugcode.cn/t/4155)

还有这篇文章，也可以进行字典反转，不过相当于我的工作的逆操作（也就是dict2->dict1）

[dictionary - 如何反转具有重复值的字典( python )](https://ask.helplib.com/python/post_12757987)




# Share

> GitHub Awesome Big Data：大数据框架、论文等实用资源集合。
  
[非常全的大数据相关资源整理](http://suanfazu.com/t/topic/13659/1)

其中包括：

- 关系数据库管理系统(RDBMS)
- 框架
- 分布式编程
- 分布式文件系统
- 键-值数据模型
- 图形数据模型
- Columnar Databases
- SQL-like processing
- Data Ingestion
- Service Programming
- Scheduling
- Machine Learning
- Benchmarking
- Security
- System Deployment
- Applications
- Search engine and framework
- MySQL forks and evolutions
- PostgreSQL forks and evolutions
- Memcached forks and evolutions
- Embedded Databases
- Business Intelligence
- Data Visualization
- Internet of things and sensor data
- Interesting Readings
- Interesting Papers
