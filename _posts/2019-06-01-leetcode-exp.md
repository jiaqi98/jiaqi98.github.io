---
layout: post
title: 刷题笔记 LeetCode217：存在重复
---

#刷题笔记 LeetCode217：存在重复
##题目
<https://leetcode-cn.com/explore/interview/card/top-interview-questions-easy/1/array/24/>

这道题是LeetCode“初级算法”专题中的一题


这学期上数据结构，写课程设计的时候深感自己代码能力欠缺，思维也比较弱，准备利用大二这个暑假好好学习一下算法，注册了新的OJ账号，打算从LeetCode, Vjudge上的基础题做起。

因为之前做算法题**遇到不会都是看看别人的题解然后感觉自己会了，结果第二天再写发现还是写不出来**。所以这次我要一道题先自己想40分钟到1个小时写写看，实在没有思路再看博客和题解，自己AC了的题也要学习别人的优化思路，同时把自己的思路和心得（~~坑~~）记录下来，希望一个假期下来我的水平能有所提高。
##我的思路
这道题一想肯定是用一个“桶”存放数字，当有该数字时，该数字下标的数组元素+1，于是很快写出了代码，之前没怎么用过`vector`，特意上网搜了一下，其实用法并不难，不知道当时学C++的时候为什么我一直不敢用...心魔也是需要克服滴...
```C++
bool containsDuplicate(vector<int>& nums) {
        int a[100] ;
        memset(a,0,100);
        int flag = 0;
        vector<int>::iterator t;
        for(t = nums.begin(); t != nums.end(); t++){
            a[*t]++;
        }
        for(int i = 0;i < 100;i++){
            if(a[i] > 1){
                flag = 1;
                break;
            }else{
                flag = 0;
            }
        }
        if(flag == 1){
            return true;
        }else{
            return false;
        }
    }
```
```
//测试用例
[1,2,3,1]
[1,2,3,4]
[1,1,1,3,3,4,3,2,4,2]
```
测试用例:过过过
提交！

**Runtime Error**....

“最后执行的输入:”
```
[1,5,-2,-4,0]
```
没有想到负数（我思维真的弱）...但是负数怎么用“桶”呢？？？这就触及到了我的知识盲区......
##暴力尝试
桶方案暂时没有新思路

我选择再用一个`vector:b`存放已经输入的数字，当前`nums`内数字与`b`内已经存放的数字逐个比较，有相等的则`return true`

```C++
bool containsDuplicate(vector<int>& nums) {
        vector<int> b;
        int flag = 0;
        vector<int>::iterator t;
        vector<int>::iterator s;
        for(t = nums.begin(); t != nums.end(); t++){
            for(s = b.begin(); s != b.end(); s++){
                if(*t == *s){
                    flag = 1;
                    break;
                }
            }
            b.push_back(*t);
        }
        if(flag == 1){
            return true;
        }else{
            return false;
        }
    }
```
测试用例：过过过
提交！

**TLE**......
意料之中，有一个10000个数据的测试点，$O\left ( n^{2} \right )$ 肯定过不了...

黔驴技穷（我是真的菜）...是时候看一波题解了

