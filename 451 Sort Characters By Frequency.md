Given a string, sort it in decreasing order based on the frequency of characters.

**Example 1:**

```html
Input:
"tree"

Output:
"eert"
```

本题就是要把字符串里的数字按频率降序输出。注意题目中说，**频率相同的字母顺序随便排都是合理答案**。

一看次数，直接想到哈希表，所以我用了map，发现其实好多map不知道的基础知识，有时间了在补一补吧。先说思路

map建立字符和出现次数的关系，map<char,int>.然后在根据value对map进行降序排列就可以了。难点就是如何降序排列。

可以先看一下这篇博客<https://blog.csdn.net/qq_26399665/article/details/52969352>。基本思想就是将map放进vector中，在对vector进行排序。

排完之后直接输出就可以，但是注意的是，输出的时候遇到每个字符多次的要输出多次该字符，就是在要嵌套一层循环，否则就只会输出一个该字符。

AC代码：

```cpp
class Solution {
public:
    static bool cmp(const pair<char,int> &p1,const pair<char,int> &p2) 
    {
	    return p1.second>p2.second;
    }
    string frequencySort(string s) {
        map<char,int> m;
        for(int i=0;i<s.length();i++){
            m[s[i]]++;
        }
        vector<pair<char,int>> arr;
        for (map<char,int>::iterator it=m.begin();it!=m.end();++it){
   	        arr.push_back(make_pair(it->first,it->second));
        }
        sort(arr.begin(),arr.end(),cmp);
        int i=0;
        for(vector<pair<char,int>>::iterator it=arr.begin();it!=arr.end();++it){
            for(int j=0;j<it->second;j++){
                s[i++]=it->first;   
            }
        }
        return s;
    }
};
```

