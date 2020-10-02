# JianZhiOfferCode
剑指Offer题解
## 题目
### 1.二位数组中的查找
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-09-30 16:34
 * 在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，
 * 每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。
 * 
 *个人解题思想：
 * 一看到题目，我们第一思想是使用暴力循环去查找。
 * 但是看到给定的数组是有序的，又因为本题是查找（我们会立刻联想到二分查找）
 * 所以我们可以根据二分查找的思想按行去查询
 **/
public class Topic1 {
    public static void main(String[] args) {
        int[][] arr = {{1,2,3},{4,5,6},{7,8,9}};
        System.out.println(Find(12, arr));
    }

    /**
     * 方法一：暴力搜素
     * @param target
     * @param array
     * @return
     */
    public static boolean Find(int target, int [][] array) {
        for (int[]arr:array) {
            for (int num:arr){
                if (num==target){
                    return true;
                }
            }
        }
        return false;
    }
   /**
     * 因为给定数组是有序，可以对每一行使用二分查找
     * @param target
     * @param array
     * @return
     */
    public static boolean Find2(int target, int [][] array) {
        for (int i = 0; i < array.length ; i++) {
            int left = 0;
            int right = array[i].length-1;
            while (left<=right){
                int mid = (left+right)/2;
                if (array[i][mid]==target){
                    return true;
                }else if (array[i][mid]<target){
                    left = mid+1;
                }else {
                    right = mid - 1;
                }
            }
        }
        return false;
    }
}
```
### 2.替换空格
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-09-30 17:10
 * 请实现一个函数，将一个字符串中的每个空格替换成“%20”。
 * 例如，当字符串为We Are Happy.
 * 则经过替换之后的字符串为We%20Are%20Happy。
 *
 * 个人解题思路：
 * 看到题目给定的是一个字符串且要将空格进行替换
 * 我们可以将字符串转为字符数组然后进行遍历再判断当遇到空格时，
 * 将其替换为题目的要求即可
 **/
public class Topic2 {
    public static void main(String[] args) {
        StringBuffer stringBuffer = new StringBuffer("We Are Happy.");
        String replaceSpace = replaceSpace(stringBuffer);
        System.out.println(replaceSpace);
    }

    /**
     * @param str
     * @return
     */
    public static String replaceSpace(StringBuffer str) {
        StringBuffer sb = new StringBuffer();
        for (int i = 0; i < str.length() ; i++) {
            if (str.charAt(i)==' '){
                sb.append("%20");
            }else {
                sb.append(str.charAt(i));
            }
        }
        return sb.toString();
    }
}
```

