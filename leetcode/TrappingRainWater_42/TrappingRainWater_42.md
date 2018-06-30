![](https://upload-images.jianshu.io/upload_images/9942378-d18e29f28d4453d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
  
首先想到从做到右减和加，遇到大值记录大值，但是有缺陷就是右边没有大值了怎么办水都漏了。  
然后想到从右到左减和加，emmm，一样啊，左边没大值水会流掉。  
既然这样的话那就先找到最大值。。然后呢，思路断了。其实可以找到最大值然后分别递归往左往右找第二大的值，找到后就不怕水漏了。不过没想出来这个方法，而且这个方法是O(n2)貌似很复杂。  
最后想到从底往上计算，每次把所有数组都减一，然后用两个指针从头尾大于等于0的地方开始计算小于0的元素的数量，直到指针相撞即所有元素都小于0。这些计算出来的数量累加起来就是结果了。假设最大值是m则O(mn)，需要遍历m次。m超大的时候就gg了。  
![](https://upload-images.jianshu.io/upload_images/9942378-8c6003576ef8757a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)  
上面的这些想法都是局限于题目给的规则了，其实可以想想怎么修改规则，改成便于自己计算的规则。  
  
>**拿到题先看能不能改规则，改成便于自己计算的规则。**  
  
怎么改？？随缘  
  
从找峰值改为-->看在i位置上能放多少水。  
**在i位置左右两边找最大值，取两个最大值的小值，减去arr[i]就是位置i能放的水量了。如果该值小于等于arr[i]，那么位置i不能储水,储水量为0。**  
  
将遍历找最大值改为O(1)的方法：  
1. 需要两个数组l、r分别存放从左边到当前位置的最大值和从右边到当前位置的最大值，这样arr[i]的左边最大值是l[i],右边最大值是r[i]。  
2. 用一个变量代替数组l，因为i遍历的时候就能够知道左边到i的最大值了。  
  
**不用辅助空间**的方法，设两指针l,r，l指向头部往右移动，r指向尾部往左移动。设两变量lmax，rmax分别记录l遍历过的值的最大值和r遍历过的最大值。  
  - ~~选择l r指向的下一个值中的小值，记为x~~。两指针指向的下一个值，选择lmax和rmax较小的一边的那个（最低瓶颈的一边的值能先得出储水量），记为x  
  - 让x跟min(lmax,rmax)比较，小于的话相减后的值是该位置的储水量，否则就是不能储水，x是左值更新lmax，右值更新rmax。  
  - x是左值指针l向右移一位，是右值的话r向左移一位。  
```java  
    public int trap(int[] height) {  
    	if(height==null || height.length==0) return 0;  
    	int l = 0;  
    	int r = height.length-1;  
    	int lmax = height[0];  
    	int rmax = height[r];  
    	int sum = 0;  
    	while(l<r-1){//两指针相邻就可以跳出循环了  
    		//选择两值较小的那一边  
    		if(lmax<rmax){  
    			sum += Math.max(0, lmax-height[++l]);  
    			lmax = Math.max(lmax, height[l]);  
    		}else{  
    			sum += Math.max(0, rmax-height[--r]);  
    			rmax = Math.max(rmax,height[r]);  
    		}  
    	}  
        return sum;  
    }  
```  
在leetcode上看到更简单容易理解的方法：  
- 先找出最大值的位置，遍历一次  
- 从左开始遍历到最大值的位置，lmax记录沿途的最大值，arr[i]与lmax相减就能得到位置i上的储水量。大于lmax就更新arr[i]。  
- 然后从右开始遍历到最大值的位置，rmax记录沿途的最大值，arr[i]与rmax相减就能得到位置i上的储水量。大于rmax就更新arr[i]。  
```java  
   public int trap(int[] height) {  
    	if(height==null || height.length==0) return 0;  
    	int maxIndex = 0;  
    	int max = height[0];  
    	for(int i=1;i<height.length;i++){  
    		if(height[i]>max){  
    			max = height[i];  
    			maxIndex = i;  
    		}  
    	}  
    	int sum = 0;  
    	int lmax = height[0];  
    	for(int i=1;i<maxIndex;i++){  
    		if(height[i]>lmax){  
    			lmax = height[i];  
    		}else{  
    			sum += lmax - height[i];  
    		}  
    	}  
    	int rmax = height[height.length-1];  
    	for(int i = height.length-2;i>maxIndex;i--){  
    		if(height[i]>rmax){  
    			rmax = height[i];  
    		}else{  
    			sum += rmax - height[i];  
    		}  
    	}  
    	return sum;  
    }  
```