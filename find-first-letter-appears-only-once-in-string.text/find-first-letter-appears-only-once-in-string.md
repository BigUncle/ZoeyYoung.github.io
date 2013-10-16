Title: [笔试] 在一个字符串中找到第一个只出现一次的字符
Date: 2013-10-10
Tags: 笔试,面试,Python
Slug: find-first-letter-appears-only-once-in-string
Author: Zoey Young
Summary: 在一个字符串中找到第一个只出现一次的字符

题目: 在一个字符串中找到第一个只出现一次的字符. 如输入abaccdeff, 则输出b.

Python写算法真是太爽了...

    :::python
    def find(str_):
        d = {}
        for s in str_:
            if s in d:
                d[s] += 1
            else:
                d[s] = 1
        for s in str_:
            if d[s] == 1:
                print(s)
                break

    find("abaccdeff")

可惜笔试基本要求用C或Java...
