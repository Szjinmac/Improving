# DAY2

## 977.有序数组的平方

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int len = nums.length;
        int[] result = new int[len];
        int k = len-1;

        //双指针
        int left = 0;
        int right = len-1;

        while(left<right&&k>0){
            if(nums[left]*nums[left]>=nums[right]*nums[right]){
                result[k] = nums[left]*nums[left];
                left = left+1;
                k = k-1;
            }else{
                result[k] = nums[right]*nums[right];
                right-=1;
                k=k-1;
            }
        }

        result[k] = nums[left]*nums[left];

        return result;

    }
}
```

## 209.长度最小的子数组

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int i = 0; //指针起始位置

        int result = Integer.MAX_VALUE;

        int sum =0; //滑动区间的和

        for(int j=0;j<nums.length;j++){
            sum+=nums[j];
            while(sum>=target){
                int temp = j-i+1;
                result = result<temp?result:temp;
                sum = sum - nums[i++];
            }
        }

        result = result == Integer.MAX_VALUE?0:result;

        return result;

    }

    
}
```

## 59.螺旋矩阵

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] mat = new int[n][n];

        int top=0,right=n-1,down=n-1,left = 0;

        int num = 1;

        int tar = n * n;

        while(num<=tar){
            //向右循环
            for(int i=left;i<=right;i++){
                mat[top][i] = num++;
                
            }
            top++;
            //向下循环
            for(int i=top;i<=down;i++){
                mat[i][right] = num++;
                
            }
            right--;
            //向左循环
            for(int i=right;i>=left;i--){
                mat[down][i] = num++;
                
            }
            down--;
            //向上循环
            for(int i=down;i>=top;i--){
                mat[i][left] = num++;
            }
            left++;
        }

        return mat;
    }
}
```

