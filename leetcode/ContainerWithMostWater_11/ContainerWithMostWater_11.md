这个比[Trapping Rain Water](https://github.com/xzll/codeandnote/blob/master/leetcode/TrappingRainWater_42/TrappingRainWater_42.md)简单（但是我还是没想出来），两头指针，一个变量记录最大值，不纠结怎么找到，确保去掉没有意义的组合就行了。  

l，r分别指向头尾，相乘后更新最大值，然后移动较小值的指针。  
因为两个指针指向的值中较小的那个值是瓶颈，所以移动较大值指针没有意义。  
移动大值指针的话，移动后面积中的高度一定是小于等于瓶颈的而且距离又缩短了，最后相乘出来的面积一定比之前的小。  
所以要移动指向较小值的那个指针。  
