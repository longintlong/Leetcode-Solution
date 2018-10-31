这个题没啥知识点，就是思路问题，还是笨啊。。。

题目大意就是返回一个数组，数组里的每个元素等于原来数组除了对应的索引的元素之外的所有元素的乘积

Given an array `nums` of *n* integers where *n* > 1,  return an array `output` such that `output[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

**Example:**

```
Input:  [1,2,3,4]
Output: [24,12,8,6]
```

本题不让用除法，如果用除法就很简单了，算出总乘积每次除以当前元素就可以了。然鹅不能用乘法。

这样想，每一个元素A[i]应该等于两部分的乘积，i-1个的乘积和后n-i个元素的乘积，最后在将这两部分相乘就可以。

那么我开两个数组pre[n]和next[n]，对应上面说的两部分，用两个for，算出每一个pre和next。



```cpp
pre[i]=pre[i-1]*nums[i-1];

next[i]=next[i+1]*nums[i+1];
```


最后再来一个for 计算出每一个pre和next的乘积。

AC的代码：

```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int s=nums.size();
        int pre[s],next[s];
        pre[0]=1;next[s-1]=1;  
        for(int i=1;i<s;i++){
            pre[i]=pre[i-1]*nums[i-1];
        }
        for(int i=s-2;i>=0;i--){
            next[i]=next[i+1]*nums[i+1];
        }
        for(int i=0;i<s;i++){
            nums[i]=pre[i]*next[i];
        }
        return nums;
    }
};
```

