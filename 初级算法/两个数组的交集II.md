#### 题目
> 题目链接：https://leetcode-cn.com/explore/interview/card/top-interview-questions-easy/1/array/26/


题目描述：给定两个数组，编写一个函数来计算它们的交集。
```
示例 1:
   输入: nums1 = [1,2,2,1], nums2 = [2,2]
   输出: [2,2]
```



#### 1. 我的代码
思路： 遍历其中一个数组，在第二个数组中寻找元素，找到了就存进新数组，并删除第二个数组中的该元素
```javascript
function intersect(nums1, nums2) {
        let same = [];
        nums1.forEach((v)=>{
            let index = nums2.indexOf(v);
            if (index > -1) {
                nums2.splice(index, 1);
                same.push(v);
            }
        });
        return same;
    }

let nums1 = [1,2,2,1], nums2 = [2,2];
intersect(nums1, nums2); // [2,2]
```
