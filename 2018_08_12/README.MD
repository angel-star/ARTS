
## Algorithm

[LeetCode 33-SearchIn Rotated Sorted Array](https://my.oschina.net/liufq/blog/1833370)

### Problem description
```
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

Example 1:

Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4
Example 2:

Input: nums = [4,5,6,7,0,1,2], target = 3
Output: -1

```

### Solution Self

看到这个题目，头脑中第一个蹦出来的就是找到rotated的元素，然后两边分别做binary search就可以了。

第一版代码
```java
class Solution {
    public int search(int[] nums, int target) {
        if (nums.length == 0) {
            return -1;
        }
        if (nums.length == 1){
            return nums[0] == target ? 0 : -1;
        }
        int pivot = binarySearchPivot(nums, 0, nums.length);
        if (pivot == -1){
            return searchIndex(nums, 0, nums.length, target);
        }
        int index = searchIndex(nums, 0, pivot, target);
        if (index != -1) {
            return index;
        }

        return searchIndex(nums, pivot, nums.length, target);
    }
    private int searchIndex(int[] nums, int low, int high, int target) {
        if (high <= low) {
            return -1;
        }
        int middle = (low + high) /2;
        if (nums[middle] == target) {
            return middle;
        }
        if (nums[middle] < target) {
            return searchIndex(nums, middle + 1, high, target);
        }
        return searchIndex(nums, low, middle, target);
    }
    private int binarySearchPivot(int[] nums, int low, int high) {
        if (high <= low) {
            return -1;
        }

        int middle = (low + high) / 2;
        if (middle > 0
                && nums[middle] < nums[middle - 1]) {
            return middle;
        }
        int leftSearch = binarySearchPivot(nums, low, middle);
        if (leftSearch != -1) {
            return leftSearch;
        }
        return binarySearchPivot(nums, middle + 1, high);
    }
}
```

分两步：
1：找到pivot，就是rotated的那个点，
2：左右两侧分别使用binarySearch来寻找元素，找到返回index，未找到返回-1

提交到LeetCode，Accepted！

不过上面这个程序有一个问题，问题描述中要求算法的复杂度需为log(n)，在搜索pivot的过程中，一直是先搜索左侧，再搜索右侧，这导致当pivot在最右侧的时候，这个`binarySearchpivot`算法的复杂度为O(n),很明显LeetCode没有强大到计算你程序的复杂度。


改进一版：

```java

package com.dylan.leetcode;

import org.junit.Assert;
import org.junit.Test;

/**
 * Created by liufengquan on 2018/6/20.
 */
public class SearchInRotatedSortedArray {
    public int search(int[] nums, int target) {
        if (nums.length == 0) {
            return -1;
        }
        if (nums.length == 1){
            return nums[0] == target ? 0 : -1;
        }
        int pivot = binarySearchPivot(nums, 0, nums.length);
        if (pivot == -1){
            return searchIndex(nums, 0, nums.length, target);
        }
        int index = searchIndex(nums, 0, pivot, target);
        if (index != -1) {
            return index;
        }

        return searchIndex(nums, pivot, nums.length, target);
    }

    private int searchIndex(int[] nums, int low, int high, int target) {
        if (high <= low) {
            return -1;
        }
        int middle = (low + high) /2;
        if (nums[middle] == target) {
            return middle;
        }
        if (nums[middle] < target) {
            return searchIndex(nums, middle + 1, high, target);
        }
        return searchIndex(nums, low, middle, target);
    }
    private int binarySearchPivot(int[] nums, int low, int high) {
        if (high <= low) {
            return -1;
        }

        int middle = (low + high) / 2;
        if (middle > 0
                && nums[middle] < nums[middle - 1]) {
            return middle;
        }
        if (nums[middle] <= nums[high - 1]) {
            return binarySearchPivot(nums, low, middle);
        }
        return binarySearchPivot(nums, middle + 1, high);
    }

    @Test
    public void test() {
        SearchInRotatedSortedArray searchInRotatedSortedArray = new SearchInRotatedSortedArray();
        int[] nums = new int[]{4, 5, 6, 7, 0, 1, 2};
        Assert.assertTrue( searchInRotatedSortedArray.search(nums, 0) == 4);
        Assert.assertTrue(searchInRotatedSortedArray.search(nums, 3) == -1);
        nums = new int[]{5, 4};
        org.junit.Assert.assertTrue(searchInRotatedSortedArray.binarySearchPivot(nums, 0, 2) == 1);
        org.junit.Assert.assertTrue(searchInRotatedSortedArray.search(nums, 4) == 1);
        org.junit.Assert.assertTrue(searchInRotatedSortedArray.search(nums, 5) == 0);

        nums = new int[]{1, 3};
        Assert.assertTrue(searchInRotatedSortedArray.binarySearchPivot(nums, 0, 2) == -1);
        Assert.assertTrue(searchInRotatedSortedArray.search(nums, 0) == -1);

        nums = new int[]{3, 4, 5, 6, 1, 2};
        System.out.println(searchInRotatedSortedArray.binarySearchPivot(nums, 0, nums.length));
        Assert.assertTrue(searchInRotatedSortedArray.binarySearchPivot(nums, 0, nums.length) == 4);
        Assert.assertTrue(searchInRotatedSortedArray.search(nums, 2) == nums.length -1);
    }
}


```

基于pivot元素的左右两侧都比它大的原则，以及pivot左右都是升序的题设，检查了一下，对于检测middle左侧还是右侧有一个判定，这样程序的执行时间复杂度就是O(log(n))了。


### Solution Others

其实在寻找pivot的过程中我们已经看到了，对于搜索左侧还是右侧我们是可以根据middle跟high的元素大小来判定出来的，因此这个pivot其实没有必要搜索出来，直接根据target的值做二分搜索就可以了。看了一下Discuss里面的网友上传解决方法，一般都是用这种。

在这贴一个他人的解决方法：

```java
class Solution {
    public int search(int[] nums, int target) {
        int start = 0;
        int end = nums.length - 1;
        while (start <= end) {
            int mid = (start + end) / 2;
            if (nums[mid] == target) return mid;
            if (nums[mid] > target) {
                if (nums[start] <= nums[mid] && nums[end] <= nums[start] && nums[start] > target)
                    start = mid + 1;
                else end = mid - 1;
            }
            else {
                if (nums[mid] <= nums[end] && nums[end] <= nums[start] && nums[end] < target)
                    end = mid - 1;
                else start = mid + 1;
            }
        }
        return -1;
    }
}


```


### DONE

考察要点：二分搜索
# Review
[Python for data science : Part 2](https://towardsdatascience.com/python-for-data-science-part-2-373d6473fa40)


本文简单介绍了python这门语言在数据科学中的使用，难度偏向入门,本文章和上周分享的 Review 属于同一系列，属于第二部分

本篇文章主要介绍了下面的内容 

Numpy创建、访问和操作数组和一些常规操作，具体的例子相对来说比较详细，所以在这里分享给大家。

## Technique

ping的底层协议实现：

ping使用ICMP(Internet Control Message Protocol)协议测试一台主机是否可达。使用的ICMP回显请求和回显应答报文如下：

![icmp报文](http://processors.wiki.ti.com/images/6/61/Frame_format_icmp.png)

ping的ICMP Type为0或8，ICMP Code为0；unix系统中将Identifier(标识符)置为发送进程的ID，以识别出不同的ping程序返回的信息；Sequence-Number从0开始，每发送一次新的回显请求就加1.

ping输出
```
> ping baidu.com
PING baidu.com (123.125.115.110) 56(84) bytes of data.
64 bytes from 123.125.115.110: icmp_seq=1 ttl=49 time=13.3 ms
64 bytes from 123.125.115.110: icmp_seq=2 ttl=49 time=16.8 ms
64 bytes from 123.125.115.110: icmp_seq=3 ttl=49 time=17.9 ms
^C
--- baidu.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2387ms
rtt min/avg/max/mdev = 13.336/16.059/17.995/1.987 ms
```

可以看到ICMP发送的报文大小为56字节，加上20字的IP首部和8字节ICMP首部，IP数据包总长度为84字节。time输出的是报文的往返时间，这里涉及到RTT的概念，可以查看wiki [RTT](https://en.m.wikipedia.org/wiki/Round-trip_delay_time)


在这里我们注意到`ping www.baidu.com`与`ping baidu.com`的输出是不同的。`ping www.baidu.com`会打印一个`www.a.shifen.com`的域名，网友们也对这个有过不少讨论，大家可以看[关于百度DNS的解析过程](http://zhan.renren.com/starshen?gid=3602888498023142484&checked=true) 和
 [尝试Ping百度域名后的思考](https://blog.csdn.net/Wu_Roc/article/details/77168426) 我尝试了一下`www.a.shifen.com`是不可访问的，但是`https://www.shifen.com/`会出现Nginx首页

现在有很多服务器设置为拒绝被ping，百度一直保留着可能是方便我们测试网络连通性吧。


# Share

以太网的硬件地址，即MAC地址实际上就是适配器地址或适配器标识符，与主机所在的地点无关。源地址和目的地址都是48位长。

> 嘉定链接在局域网上的一台计算机的适配器坏了，而我们更换了一个新的适配器，那么这台计算机的局域网的"地址"也就改变了，虽然这台计算机的地址为只一点也没有变化，所介入的局域网也没有任何变化。

> 嘉定我们把位于北京的某局域网上的以太笔记本电脑携带到北京，并连接在北京的某局域网上。虽然这台电脑的地理位置改变了，但只要电脑中的适配器不便，那么该电脑在北京的局域网中的"地址"仍然和它在南京的局域网中的"地址"一样。

所以严格的讲：局域网的地址应当是每一个站的名字或标识符【PERL00】
