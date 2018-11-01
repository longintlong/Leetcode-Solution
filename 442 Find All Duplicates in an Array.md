数组题发现都是考思路的啊，知识点倒没啥。

题目大意就事给一个长度为n的数组，数组的元素值域是[1,n]，并且这些每个数存在不超过两次，要求找出出现次数为2的元素。

Given an array of integers, 1 ≤ a[i] ≤ *n* (*n* = size of array), some elements appear **twice**and others appear **once**.

Find all the elements that appear **twice** in this array.

**Example:**

```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```

先来说下我自己的思路，我比较菜，所以是笨办法。用unordered_map,先判断在不在map里，如果不在就加进去，令他等于1.

如果在，就添加到ans数组里。直接看代码吧

```cpp
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        unordered_map<int,int> m;
        vector<int> ans;
        for(int i=0;i<nums.size();i++){
            if(m.find(nums[i])==m.end()){
                m[nums[i]]=1;
            }
            else{
                if(m[nums[i]]>1)continue;
                m[nums[i]]++;
                ans.push_back(nums[i]);
            }
        }
        return ans;
    }
};
```

下面说一下大佬的解法：

大佬说 这道题类似[Find the Duplicate Number]

因为每个元素都是在 [1,n]，所以对于每个nums[i],如果nums[abs(nums[i])-1]<0，说明这是出现了第二次，直接添加到ans数组里。否则就说明是第一次出现，取相反数。死过一。。。。。反正我是不可能想到这种方法的。

```cpp
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
        vector<int> ans;
        for(int i=0;i<nums.size();i++)
        {
            if(nums[abs(nums[i])-1]<0){ans.push_back(abs(nums[i]));}
            else
                nums[abs(nums[i])-1]=-nums[abs(nums[i])-1];
        }
        return ans;
    }
};
```

