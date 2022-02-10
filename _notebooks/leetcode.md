----
layout: page
title: Leetcode
permalink: /leetcode/

----


```python
# 2sum
def twosum(nums, target):
    d = {}
    for i in range(len(nums)):
        if target - nums[i] in d:
            return [i,d[target-nums[i]]]
        else:
            d[nums[i]] = i

            
print (twosum([1,2,3,6],5))
```

    [2, 1]



```python

```
