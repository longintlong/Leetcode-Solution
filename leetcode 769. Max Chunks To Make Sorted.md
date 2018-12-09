# ​leetcode 769. Max Chunks To Make Sorted

题目大意就是一个数组分块，每一块排序后，在拼接起来后的数组是 将原来数组升序排序的结果。如果理解起来有点困难，看样例就会明白。我把这个块叫 独立块，(个人理解)

Example 1:

Input: arr = [4,3,2,1,0]
Output: 1
Explanation:
Splitting into two or more chunks will not return the required result.
For example, splitting into [4, 3], [2, 1, 0] will result in [3, 4, 0, 1, 2], which isn't sorted.
Example 2:

Input: arr = [1,0,2,3,4]
Output: 4
Explanation:
We can split into two chunks, such as [1, 0], [2, 3, 4].
However, splitting into [1, 0], [2], [3], [4] is the highest number of chunks possible.
思路：

想象有一个窗口在数组上移动，只需要考虑窗口的右侧就可以，这个右侧用指针r表示。

两层循环遍历数组，对于每个arr[i]，让r=arr[i],就相当于找到了窗口的最右端。这说明 在 [i,r]这个区间肯定是不能再分块了。

子循环遍历从[i+1,r]的元素，看这个窗口是否会变大。变大的条件就是arr[j]>r。

当子循环指针 j>r时，说明生成了一块独立快。将窗口左侧移动到r+1;

AC代码：

```C++
class Solution {
public:
    int maxChunksToSorted(vector<int>& arr) {
        int ans=0,r=0;
        for(int i=0;i<arr.size();i++){
            r=arr[i];
            for(int j=i+1;j<=r;j++){
                if(arr[j]>r)r=arr[j];
            }
            ans++;
            i=r;
        }
        return ans;
    }
};	
```

