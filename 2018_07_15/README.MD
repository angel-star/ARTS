
# Algorithm

[709. To Lower Case](https://leetcode.com/problems/to-lower-case/description/)
题目描述：
Implement function ToLowerCase() that has a string parameter str, and returns the same string in lowercase.


 
 
下面给出最普遍的做法的C++实现

```C++
class Solution {
public:
    string toLowerCase(string str) {
        string result = "";
        for (auto s : str) {
            if (s >= 'A' && s <= 'Z') {
                result += 'a' + s - 'A';
            } else result += s;
        }
        return result;
    }
};

```


本周的`Algorithm`环节划个水，下周来两道。


# Review
【为什么做木工可以让你成为个更好的程序员】[Why Woodworking Will Make You a Better Coder](https://towardsdatascience.com/why-woodworking-will-make-you-a-better-coder-adb91cbcaafd)


本文内容概要：

> I’ve found that dissimilar hobbies can lead to unexpected transfer learning. In the following essay, I share an example of this lateral thinking; how skills in one area can inform learning and decision making in another.

本文通过五个方面阐述了做一个"木工"为什么会让自己在敲程序方面有所建树，他给出了五个理由：


- It will teach you utility

- It will teach you to troubleshoot

- It will teach you bootstrapping

- It will teach you progress

- It will teach you work backwards



** 本篇文章阐述了作者在通过日常生活中的接触到的"木工"工作，引发的一系列的思考——它和coding很像，并且可以在某方面给你更新的思考 **
正如文章开头所说的那样

> Many adept technologists agree that being good at one thing is the same as being good at none; “two is one and one is none”. Those who can work across many disciplines — the polymaths — will dominate the future of business. 

关键词：`ProgrammingData`  `Science` `LifeCodeComputer` `Science`
 


# Technique
**什么是分布式文件系统？**

分布式文件系统。可以拆分为三个词，分布式、文件和文件系统。

什么是分布式？简单来说就是用一批机器通过网络进行协同统一提供某种服务，这种服务的内部细节通常是对外透明的，外部只能感知到这个系统是提供某个可靠的服务，而不关心内部的节点状态，副本，分割等等。

什么是文件？对于linux系统来说，一切都是文件。那什么是文件呢？无论什么文件，都可以看成很大很大的二进制数组。

什么是文件系统？首先系统就是多个组件有机结合的产物，文件系统则是系统中负责管理和存储文件信息的子系统。

所以什么叫分布式文件系统？

就是一个利用一批机器通过网络方式，以统一透明的服务对外提供文件存储和文件管理的系统。


下面就开始练级了，能学到哪算哪，今天只搞搞 Level1。

JDK是8，依赖使用maven 管理，先看看maven 依赖，只依赖了一个guava 包，用来方便处理各种集合。


```xml

<dependency>
   <groupId>com.google.guava</groupId>
   <artifactId>guava</artifactId>
   <version>25.1-jre</version>
</dependency>

```

- Level 1 搞一个简单的内存分布式存储器

```java
package com.bigbanana.lab.lab3.dajiao.step1;

import com.google.common.primitives.Bytes;

import java.util.*;

public class SimpleDistributeFSInMemory {

   public static Map<String,Map<String,List<Byte>>> servers= new HashMap<>();
   public static Integer serverSize = 3;

   static {
      /**
       * 初始化三台虚拟的机器
       */
      for(int i = 0 ; i < serverSize ;i++){
         Map<String,List<Byte>> server = new HashMap<>();
         servers.put(i+"",server);
      }

   }

   public static void main(String[] args){
      /**
       * 命令行初始化
       */
      Scanner scanner = new Scanner(System.in);

      while (scanner.hasNextLine()){
         String command  = scanner.nextLine();
         String[] commandArray = command.split(" ");

         String targetCommand = commandArray[0];
         String fileName = commandArray[1];

         /**
          * 根据文件名找到文件所在的服务器，并获得对应文件池的索引
          */
         int serverIndex = getServerIndex(fileName);
         Map<String,List<Byte>> serverFile = servers.get(serverIndex+"");

         if("get".equals(targetCommand)){
            println("getting file from server "+serverIndex +"....");

            /**
             * 如果是get 从文件桶中找到对应名称的文件，并把它转成String 输出出来。
             */
            println(new String(Bytes.toArray(serverFile.getOrDefault(fileName,new ArrayList<>()))));

         }else if("put".equals(targetCommand)){
            /**
             * 如果是put 把文件(这里是 String)转换成 byte 数组，并把它保存到文件桶中
             */
            println("putting file to server "+serverIndex +"....");
            String file = commandArray[2];
            List<Byte> fileBytes = Bytes.asList(file.getBytes());

            serverFile.put(fileName,fileBytes);

            println("success");
         }
      }

   }

   /**
    * 打印的工具类
    */
   public static void println(Object o){
      System.out.println(o);
   }

   /**
    * 根据hash获取文件服务的编号
    */
   public static Integer getServerIndex(String fileName){
      return fileName.hashCode() % serverSize;
   }
}
```

在命令行中敲一下自己刚刚实现的文件系统，可以看到我们已经实现了最最基础的功能，即 get 和 put。




put banana.git banananisToooBig
putting file to server 1....
success
get banana.get
getting file from server 0....

get banana.git
getting file from server 1....
banananisToooBig


**实现的思路是怎样的呢？**
1、初始化整个服务器集群，这里用了3，Level 2 中这里会将服务器抽象成单独的实体。


```java
public static Map<String,Map<String,List<Byte>>> servers= new HashMap<>();
public static Integer serverSize = 3;

static {
   /**
    * 初始化三台虚拟的机器
    */
   for(int i = 0 ; i < serverSize ;i++){
      Map<String,List<Byte>> server = new HashMap<>();
      servers.put(i+"",server);
   }

}

```

2、定义服务器的分桶方式，这里使用文件名 hash 然后取 mod 的方式进行服务器寻址。

```java
/**
 * 根据hash获取文件服务的编号
 */
public static Integer getServerIndex(String fileName){
   return fileName.hashCode() % serverSize;
}
```  
3、获取对应的服务器，根据我们前边定义的方式，我们这里直接从 Map 里边取出来了。



```java

/**
 * 根据文件名找到文件所在的服务器，并获得对应文件池的索引
 */
int serverIndex = getServerIndex(fileName);
Map<String,List<Byte>> serverFile = servers.get(serverIndex+"");
```  

4、定义put 操作。取到对应的文件(这里把文件简化为String了)，然后获取文件对应的 byte 数组，把它们的格式进行统一之后，写入到服务器的文件桶里。

```java
else if("put".equals(targetCommand)){
   /**
    * 如果是put 把文件(这里是 String)转换成 byte 数组，并把它保存到文件桶中
    */
   println("putting file to server "+serverIndex +"....");
   String file = commandArray[2];
   List<Byte> fileBytes = Bytes.asList(file.getBytes());

   serverFile.put(fileName,fileBytes);

   println("success");
}
```  

5、定义 get 操作。跟put 操作一样，先找到文件服务器，再找到文件桶，然后从桶里按照 文件名 取得对应的 byte List，转换成byte数组然后 转换成 String，打印出来。


```java
if("get".equals(targetCommand)){
   println("getting file from server "+serverIndex +"....");

   /**
    * 如果是get 从文件桶中找到对应名称的文件，并把它转成String 输出出来。
    */
   println(new String(Bytes.toArray(serverFile.getOrDefault(fileName,new ArrayList<>()))));

}
```  

6、向外暴露 client ，这里是使用 Scanner 来扫描系统输入，然后按照  "command  文件名 文件内容" 的方式来组织这个过程。

```java
Scanner scanner = new Scanner(System.in);

while (scanner.hasNextLine()){
   String command  = scanner.nextLine();
   String[] commandArray = command.split(" ");

   String targetCommand = commandArray[0];
   String fileName = commandArray[1];
}
```  


至此，我们分布式文件系统 LEVEL 1就愉快地结束了，希望对你有帮助，想让我实现 LEVEL 2说一下，因为这个版本是最简单的，LEVEL 2 会将各个服务进行抽象，方便我们后面对各个服务进行单独部署和协同，定义多一个 append 的api，当然还是以内存的格式，因为一开始就陷入文件流网络的操作，会让你很迷糊。当然我也放到github上了，就下边这个练级项目，在lab3里边。




 Java 练级项目我已经建立了，[https://github.com/CallMeDJ/BananaLab.git](https://github.com/CallMeDJ/BananaLab.git)

- 那么如何操作呢？

1. 新建一个自己的package，并拷贝dajiao文件夹的demo类

2. 实现类里边需要你实现的功能

3. 跑 test ，通过之后可以提交。

4. 写一个 MD文件，描述一下你的思路以及注意点。

5. 提交你的PR，我会看情况 merge，目前已经有8位小伙伴一起练级啦。


转载自公众号《一名叫大蕉的程序员》


# Share

> 今天的主角是 Wide & Deep Model，在推荐系统和 CTR 预估中都有应用。万字长文，墙裂推荐！
  
本文来自于公众号《AI前线》

开篇介绍了几个名词解释  `Memorization 和 Generalization` 、`Wide 和 Deep` 、 `Cross-product transformation`

然后介绍了两种推荐系统：`CF-Based（协同过滤）`、`Content-Based（基于内容的推荐）`

在简单概述系统实践后又提到了适用范围与优缺点 并在大篇幅地介绍了代码实现：

>  https://github.com/gutouyu/ML_CIA/tree/master/Wide%26Deep
   
>  数据集：https://archive.ics.uci.edu/ml/machine-learning-databases/adult
   
>  代码主要包括两部分：Wide Linear Model 和 Wide & Deep Model。

[『CTR预估专栏 | 详解Wide&Deep理论与实践』](https://mp.weixin.qq.com/s/5wdGemYBtkYUvq1n5ioyFg)

注：本文原发于公众号《机器学习荐货情报局》，感兴趣的同学们可以去查一下其他几篇专栏文章


----


另外安利大家一篇文章 ，是瓜哥发在群里的


[如何阅读一篇论文](http://www.cs.princeton.edu/courses/archive/fall13/cos597E/papers/howtoread.pdf)
