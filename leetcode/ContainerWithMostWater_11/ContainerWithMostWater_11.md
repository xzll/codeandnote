这个比[Trapping Rain Water](https://github.com/xzll/codeandnote/blob/master/leetcode/TrappingRainWater_42/TrappingRainWater_42.md)简单（但是我还是没想出来），两头指针，一个变量记录最大值，不纠结怎么找到，确保去掉没有意义的组合就行了。  

l，r分别指向头尾，相乘后更新最大值，因为小的是瓶颈，移动大的指针没有意义，移它的话一边高度一定是小于等于的瓶颈的而且距离缩短了，最后相乘出来的面积一定是比之前小的，所以要移动小的那个指针。  
