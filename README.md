# JianZhiOfferCode
剑指Offer题解

   * [JianZhiOfferCode](#jianzhioffercode)
      * [题目](#题目)
         * [1.二位数组中的查找](#1二位数组中的查找)
         * [2.替换空格](#2替换空格)
         * [3.从位到头打印链表](#3从位到头打印链表)
         * [4.重建二叉树](#4重建二叉树)
         * [5.用两个栈实现队列](#5用两个栈实现队列)
         * [6.旋转数组的最小数字](#6旋转数组的最小数字)
         * [7.斐波那契数列](#7斐波那契数列)
         * [8.跳台阶](#8跳台阶)
         * [9.变态跳台阶](#9变态跳台阶)
         * [10.矩形覆盖](#10矩形覆盖)
         * [11.二进制中1的个数](#11二进制中1的个数)
         * [12.数值的整数次方](#12数值的整数次方)
         * [13.调整数组序列使奇数位于偶数前面](#13调整数组序列使奇数位于偶数前面)
         * [14.链表中倒数第k个节点](#14链表中倒数第k个节点)
         * [15.反转链表](#15反转链表)
         * [16.合并两个有序链表](#16合并两个有序链表)
         * [17.树的子结构](#17树的子结构)
         * [18.二叉树的镜像](#18二叉树的镜像)
         * [19.顺时针打印矩阵](#19顺时针打印矩阵)
         * [20.包含min函数的栈](#20包含min函数的栈)
         * [21.栈的压入弹出序列](#21栈的压入弹出序列)
         * [22.从上往下打印二叉树](#22从上往下打印二叉树)
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
### 3.从位到头打印链表
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-09-30 17:31
 * 输入一个链表，按链表从尾到头的顺序返回一个ArrayList。
 *
 * 个人解题思路：
 * Ⅰ：首先题目是需要将链表倒序打印且封装为一个ArrayList返回，
 * 我们就会想到在ArrayList中有一个void add(int index, E element)方法
 * 此方法会将我们插入的值倒序存储，因此我们可以对原始链表进行遍历，每遍历一个值将其add即可。
 * Ⅱ：题目要求是倒序打印，我们不难想到一个数据结构（栈），因为我们可以使用栈来完成
 * 先遍历原始链表，将其每个值进行入栈操作
 * 然后对栈进行pop即可
 **/
public class Topic3 {
    public static void main(String[] args) {
        LinkedList linkedList = new LinkedList();
        LinkedList init = linkedList.Init();
        linkedList.show(init);

        ArrayList<Integer> arrayList = printListFromTailToHead2(init);
        System.out.println(arrayList.toString());
    }

    /**
     * 利用栈
     * @param listNode
     * @return
     */
    public static ArrayList<Integer> printListFromTailToHead2(LinkedList listNode) {
        ArrayList<Integer> arrayList = new ArrayList<>();
      //  LinkedList temp =  listNode.next;
        LinkedList temp =  listNode;
        Stack<Integer> stack = new Stack();
        while (temp!=null){
            stack.push(temp.value);
            temp = temp.next;
        }
        while (stack.size()>0){
            arrayList.add(stack.pop());
        }
        return  arrayList;
    }

    /**
     * 倒序打印链表
     * @param listNode
     * @return
     */
    public static ArrayList<Integer> printListFromTailToHead(LinkedList listNode) {
        ArrayList<Integer> arrayList = new ArrayList<>();
        if (listNode==null||listNode.next==null){
            return arrayList;
        }
        //  LinkedList temp =  listNode.next;
        LinkedList temp = listNode;
        while (temp!=null){
            arrayList.add(0, temp.value);
            temp = temp.next;
        }
        return  arrayList ;
    }
}

/**
 * 节点
 */
class LinkedList {
     int value;
     LinkedList next;

    public LinkedList(int value) {
        this.value = value;
    }

    public LinkedList() {

    }

//    public int getValue() {
//        return value;
//    }

    /**
     * 显示链表
     * @return
     */
    public void show(LinkedList node) {
        if (node.next == null) {
            System.out.println("链表为空");
            return;
        }
        LinkedList temp = node.next;
        while (temp != null) {
            System.out.println(temp);
            temp = temp.next;
        }
    }

    /**
     * 初始化链表
     *
     * @return
     */
    public LinkedList Init() {
        //头节点
        LinkedList head = new LinkedList();
        LinkedList temp = head;
        while (true) {
            Scanner sc = new Scanner(System.in);
            int val = sc.nextInt();
            //输入0退出输入循环
            if (0 == val) {
                break;
            }
            LinkedList linkedList = new LinkedList(val);
            temp.next = linkedList;
            temp = linkedList;
        }
        return head;
    }

//    public void setValue(int value) {
//        this.value = value;
//    }
//
//    public LinkedList getNext() {
//        return next;
//    }
//
//    public void setNext(LinkedList next) {
//        this.next = next;
//    }

    @Override
    public String toString() {
        return "LinkedList{" +
                "value=" + value +
                ", next=" + next +
                '}';
    }
}
```
### 4.重建二叉树
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-02 16:14
 * 输入某二叉树的前序遍历和中序遍历的结果，
 * 请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。
 * 例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，
 * 则重建二叉树并返回。
 * 
 * 个人解题思路：
 * 题目要求重建二叉树，给了前序和中序遍历的结果，
 * 我们很容易根据前序得到此二叉树的根节点，根据中序可以对二叉树进行左右子树的划分。
 * 在二叉树中，我们一般都是使用递归的方式完成二叉树的各种操作，因此，此题我们只需要
 * 找到递归的条件即可。比如先找到前序左子树和右子树的数组，然后找到中序左子树和右子树的数组，
 * 进行条件递归即可。
 * 方法一是将没一步进行细化，可以更好的给大家提供一个思路，
 * 方法二则是对方法一某些步骤的简化。
 **/
public class Topic4 {
    public static void main(String[] args) {
        int[]pre={1,2,4,7,3,5,6,8};
        int[]in={4,7,2,1,5,3,8,6};
        TreeNode treeNode = reConstructBinaryTree(pre, in);
        System.out.println(treeNode);
        TreeNode treeNode2 = reConstructBinaryTree2(pre, in);
        System.out.println(treeNode2);
    }

    /**
     * 方法二：使用Arrays工具类对方法一进行简化
     * @param pre
     * @param in
     * @return
     */
    public static TreeNode reConstructBinaryTree2(int [] pre,int [] in) {
        if (pre.length==0 || in.length==0){
            return null;
        }
        //找到二叉树的根
        TreeNode root = new TreeNode(pre[0]);
        for (int i = 0; i < in.length ; i++) {
            //找到划分左右递归子树的地方
            //copyOfRange 左闭右开
            if (pre[0]==in[i]){
                root.left=reConstructBinaryTree(Arrays.copyOfRange(pre, 1, i+1),Arrays.copyOfRange(in, 0, i));
                root.right=reConstructBinaryTree(Arrays.copyOfRange(pre, i+1, pre.length),Arrays.copyOfRange(in, i+1, in.length));
            }
        }
        return root;
    }

    /**
     * 方法一
     * @param pre
     * @param in
     * @return
     */
    public static TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        if (pre.length!=0 && in.length!=0){
            //先根据前序遍历找到根节点
            TreeNode root = new TreeNode(pre[0]);
            //根据中序遍历划分左右子树
            int i=0;
            while (pre[0]!= in[i]){
                i++;
            }
            //根据i定义中序遍历数组
            int[]inLeft = new int[i];
            int[]inRight = new int[in.length-i-1];
            //给中序遍历左子树赋值
            for (int j = 0; j < inLeft.length ; j++) {
                inLeft[j] = in[j];
            }
            //给中序遍历右子树赋值
            for (int j = 0; j < inRight.length ; j++) {
                inRight[j] = in[inLeft.length+j+1];
            }
            //根据i定义前序遍历数组
            int[]preLeft= new int[i];
            int[]preRight = new int[in.length-i-1];
            //给前序遍历左子树赋值
            for (int j = 0; j < preLeft.length ; j++) {
                preLeft[j] = pre[j+1];
            }
            //给前序遍历右子树赋值
            for (int j = 0; j < preRight.length ; j++) {
                preRight[j] = pre[j+preLeft.length+1];
            }
            //左右递归
            root.left = reConstructBinaryTree(preLeft,inLeft);
            root.right = reConstructBinaryTree(preRight,inRight);
            return root;

        }else {
            return null;
        }

    }
}

class TreeNode {
     int val;
     TreeNode left;
     TreeNode right;
     TreeNode(int x) { val = x; }

    @Override
    public String toString() {
        return "TreeNode{" +
                "val=" + val +
                ", left=" + left +
                ", right=" + right +
                '}';
    }
}
```
### 5.用两个栈实现队列
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-02 17:09
 * 用两个栈来实现一个队列，完成队列的Push和Pop操作。
 * 队列中的元素为int类型。
 *
 * 个人解题思路：
 * 我们知道栈是先进后出的数据结构，而队列是先进先出的数据结构
 * 因此，我们可以利用一个栈来push原始数据然后再将第一个栈的数据在出栈时候再让其入第二栈
 * 然后对第二栈进行pop即可实现队列。
 * 比如原始数据：1 2 3 4
 * 1 2 3 4：入stack1后出stack1：4 3 2 1
 * 4 3 2 1：入stack2后出stack2：1 2 3 4
 * 即相当于队列操作：入队列1 2 3 4 出队列1 2 3 4
 **/
public class Topic5 {
    public static void main(String[] args) {
        StackToQueue stackToQueue = new StackToQueue();
        stackToQueue.push(1);
        stackToQueue.push(2);
        int pop = stackToQueue.pop();
        System.out.println(pop);
        int pop2 = stackToQueue.pop();
        System.out.println(pop2);
    }
}
class StackToQueue{
    Stack<Integer> stack1 = new Stack<>();
    Stack<Integer> stack2 = new Stack<>();
    public void push(int node) {
        stack1.push(node);
    }
    public int pop() {
        //先判断stack2是否为空
        if (stack2.isEmpty()){
            //stack2为空，当stack1不为空一直push
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        //stack2不为空先将里面的数据弹栈 
        return  stack2.pop();
    }
}
```
### 6.旋转数组的最小数字
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-03 09:36
 * 把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
 * 输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。
 * 例如数组[3,4,5,1,2]为[1,2,3,4,5]的一个旋转，该数组的最小值为1。
 * NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。
 * 
 *个人解题思路：
 * 第一种方式:我们可以使用方法一的思想，逐个遍历数组找出最小值
 * 第二种：利用二分查找法的思想
 **/
public class Topic6 {
    public static void main(String[] args) {
        int[]arr = {3,4,5,1,2};
        System.out.println(minNumberInRotateArray(arr));
        System.out.println(minNumberInRotateArray2(arr));

    }

    /**
     * 二分查找
     * @param array
     * @return
     */
    public static int minNumberInRotateArray2(int [] array) {
        int left = 0;
        int right = array.length-1;
        while (left<=right){
            int mid = (left+right)/2;
            //小的值在中间值的左边
            if (array[mid]<array[right]){
                right = mid;
            } 
            //小的值在中间值的右边
            else if(array[mid]>array[right]){
                left = mid+1;
            }
            else {
                right--;
            }
        }
        return array[left];
    }

    /**
     * 暴力法
     * @param array
     * @return
     */
    public static int minNumberInRotateArray(int [] array) {
        int temp=array[0];
        for (int i = 1; i < array.length ; i++) {
            if (temp>array[i]){
               temp = array[i];
            }
        }
        return temp ;
    }
}

```
### 7.斐波那契数列
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-03 15:09
 * 大家都知道斐波那契数列，现在要求输入一个整数n，
 * 请你输出斐波那契数列的第n项（从0开始，第0项为0，第1项是1）。
 *
 * 解题思路:
 * 斐波那契数列即：1 1 2 3 5 ....
 * 我们可以发现前两个数相加即是第三个数的值
 * 因此我们可以递归和非递归的方法实现
 **/
public class Topic7 {
    public static void main(String[] args) {
        System.out.println(Fibonacci2(4));
    }
    /**
     * 递归实现
     * @param n
     * @return
     */
    public static int Fibonacci2(int n) {
        if (n<=2 && n>0){
            return 1;
        }
        if (n<=0){
            return 0;
        }
        return Fibonacci2(n-2)+Fibonacci2(n-1);
    }

    /**
     * 非递归实现
     * @param n
     * @return
     */
    public static int Fibonacci(int n) {
        if (n<=2 && n>0){
            return 1;
        }
        if (n<=0){
            return 0;
        }
        int temp = 0;
        int a = 1,b = 1;
        while (n>2){
            temp = a+b;
            a = b;
            b = temp;
            n--;
        }
        return temp;
    }
}

```
### 8.跳台阶
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-03 15:29
 * 一只青蛙一次可以跳上1级台阶，也可以跳上2级。
 * 求该青蛙跳上一个n级的台阶总共有多少种跳法（先后次序不同算不同的结果）。
 *
 * 个人解题思路：
 *  台阶数       跳跃方式
 *    1          1
 *    2          11  2
 *    3          111  12 21
 *    4          1111 112 121 211 22
 *    ....        ....
 *    可以发现台阶数和跳跃方式之间存在函数关系
 *    x<=1---------->F(x)=1
 *    (x>2)--------->F（x）=F(x-2)+F(x-1)
 *
 **/
public class Topic8 {
    public static void main(String[] args) {
        System.out.println(JumpFloor(2));
    }

    /**
     * 使用递归
     * @param target
     * @return
     */
    public static int JumpFloor(int target) {
        if (target<=1){
            return 1;
        }
        return JumpFloor(target-2)+JumpFloor(target-1);
    }
}

```
### 9.变态跳台阶
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-03 19:57
 *
 * 一只青蛙一次可以跳上1级台阶，
 * 也可以跳上2级……它也可以跳上n级。
 * 求该青蛙跳上一个n级的台阶总共有多少种跳法。
 * 个人解题思路：
 *  台阶数       跳跃方式
 *    1          1
 *    2          11  2
 *    3          111  12 21  3
 *    4          1111 112 121 211 22 13 31 4
 *    ....        ....
 *    可以发现台阶数和跳跃方式之间存在函数关系
 *    x<=1---------->F(x)=1
 *    (x>2)--------->F（x）=2*F(x-1)
 *
 **/
public class Topic9 {
    public static void main(String[] args) {
        System.out.println(JumpFloorII(4));
    }
    /**
     * 递归
     * @param target
     * @return
     */
    public static int JumpFloorII(int target) {
        if (target<=1){
            return 1;
        }
        return 2*JumpFloorII(target-1);
    }
}

```
### 10.矩形覆盖
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-03 20:01
 * 我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形
 * 请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？
 *
 * 个人解题思路：
 *  其实就是类似于一个斐波那契数列
 **/
public class Topic10 {
    public static void main(String[] args) {
        System.out.println(RectCover(5));
    }

    /**
     * 递归
     * @param target
     * @return
     */
    public static int RectCover(int target) {
        if (target==1){
            return 1;
        }
        if(target<1){
            return 0;
        }
        if(target==2){
            return 2;
        }
        return RectCover(target-2)+RectCover(target-1);
    }
}
```
### 11.二进制中1的个数
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-03 20:14
 * 输入一个整数，输出该数32位二进制表示中1的个数。其中负数用补码表示。
 *
 *个人解题思路：
 * 首先我们会想到用这个数%2 然后统计 但是这样的算法可以满足大于0的数，
 * 对于负数显然无法满足。所以该算法被舍弃
 * 其次我们会发现在计算机中，一个数&这个数-1 即可抵消一位1
 * 例如：
 * 7----------->0111 要统计其中1的个数，显然有三个
 * 我们让7&6
 * 6----------->0110
 *    0111
 *   &0110
 *  --------
 *    0110
 * 我们会发现此时抵消了末位上的1 .根据这个规律 我们只需要判断当
 *  n>0 且每次让 n = n & n-1 然后统计次数即可。
 **/
public class Topic11 {
    public static void main(String[] args) {
        System.out.println(NumberOf1(7));
    }
    public static int NumberOf1(int n) {
        int count = 0;
        while (n>0){
            n = n & n-1;
            count++;
        }
        return count;
    }
}

```
### 12.数值的整数次方
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-05 17:06
 *
 * 给定一个double类型的浮点数base和int类型的整数exponent。
 * 求base的exponent次方。
 * 保证base和exponent不同时为0
 *
 * 个人解题思路：
 *  首先需要考虑base情况
 *  当base>0  base的exponent次方就是exponent个base相乘的结果
 *  当base=0  base的exponent次方就是0
 *  当base<0  base的exponent次方就是exponent个base相乘分之一的结果
 *  其次考虑exponent情况
 *  当exponent>0 base的exponent次方就是exponent个base相乘的结果
 *  当exponent=0 base的exponent次方就是1
 *  当exponent<0 base的exponent次方就是exponent个base相乘的结果
 *  最后考虑base和exponent同时为0 返回-1即可
 *  其实我们只需要考虑exponent的情况即可不需要考虑base>0&&base<0的情况；
 *  因为这两种情况在exponent情况中已经被考虑到。
 **/
public class Topic12 {
    public static void main(String[] args) {
        System.out.println(Power(-2.0, -3));
    }
    public static double Power(double base, int exponent) {
        if (base==0 && exponent==0){
            return -1;
        }
        if (exponent==0){
            return 1.0D;
        }
        if (base==0){
            return 0.0D;
        }
        double result = 1.0D;
        if (exponent>0 ){
            while (exponent>0){
                result*=base;
                exponent--;
            }
            return result;
        }else {
            exponent=(-1)*exponent;
            while (exponent>0){
                result*=base;
                exponent--;
            }
            return 1.0/result;
        }
    }
}
```
### 13.调整数组序列使奇数位于偶数前面
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-05 19:01
 * 输入一个整数数组，实现一个函数来调整该数组中数字的顺序，
 * 使得所有的奇数位于数组的前半部分，
 * 所有的偶数位于数组的后半部分，并保证奇数和奇数，
 * 偶数和偶数之间的相对位置不变。
 *
 * 个人解题思路：
 *  定义一个跟原始数组大小一样的数组用来存放新数组
 *  遍历数组看是奇数还是偶数，然后放在对应的数组中
 *  最后覆盖原始数组即可
 **/
public class Topic13 {
    public static void main(String[] args) {
        int[] arr ={1,2,3,4,5,6,7};
        reOrderArray(arr);
    }
    public static void reOrderArray(int [] array) {
        int []arr = new int[array.length];
        int j = 0,k=0;
        /**
         * 判断数组中的奇偶放入对应的数组
         */
        for (int i = 0; i < array.length ; i++) {
            if (array[i]%2!=0){
                array[j] = array[i];
                j++;
            }else {
                arr[k] = array[i];
                k++;
            }
        }
        for (int i = 0; i < arr.length; i++) {
            if (arr[i]==0)break;
            array[j] = arr[i];
            j++;
        }
        System.out.println(Arrays.toString(array));
    }
}

```
### 14.链表中倒数第k个节点
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-06 19:47
 *
 * 输入一个链表，输出该链表中倒数第k个结点。
 *
 * 个人解题思路：
 * 可以先遍历链表得到的链表的总长度length
 * 然后遍历到链表的length-k位置返回
 * 得到的值即是满足要求的值
 * 假如链表为：1--->2---->3--->4---->5---->null   k：2
 * 返回的值应该为4 因为倒数第2个值为4
 *  我们先遍历链表的长度为5 然后遍历到5-2即3的位置返回
 *  即可得到4
 *
 **/
public class Topic14 {
    public static void main(String[] args) {
        ListNode listNode = new ListNode().initList();
        listNode.show(listNode);
        System.out.println(FindKthToTail(listNode, 7));
    }

    /**
     * 剑指Offer提交代码： 因为剑指中头节点包含有效元素
     * 所以遍历应该算上头节点
     * @param head
     * @param k
     * @return
     */
    public static ListNode FindKtToTail2(ListNode head,int k){
        if (head==null || head.next==null){
            return null;
        }
        ListNode temp = head;
        int length=0;
        while (temp!=null){
            length++;
            temp = temp.next;
        }
        if (k>length){
            return null;
        }
        //从新指向头节点
        temp = head;
        for (int i = 0; i < length-k ; i++) {
            temp = temp.next;
        }
        return temp;
    }

    public static ListNode FindKthToTail(ListNode head,int k) {
        if (head.next==null){
            return null;
        }
        ListNode temp = head.next;
        int length=0;
        while (temp!=null){
            length++;
            temp = temp.next;
        }
        //判断是否超出链表长度
        if (k>length){
            return null;
        }
        //从新指向头节点
        temp = head.next;
        for (int i = 0; i < length-k ; i++) {
            temp = temp.next;
        }
        return temp;
    }
}

/**
 * 链表节点
 */
class ListNode{
    int value;
    ListNode next;

    public ListNode() {
    }
    public ListNode(int value) {
        this.value = value;
    }

    @Override
    public String toString() {
        return "ListNode{" +
                "value=" + value +
                ", next=" + next +
                '}';
    }

    /**
     * 初始化链表
     */
    public ListNode initList(){
        ListNode head = new ListNode();
        ListNode temp = head;
        while (true){
            Scanner scanner = new Scanner(System.in);
            int i = scanner.nextInt();
            if (i==0){
                break;
            }
            ListNode listNode = new ListNode(i);
            temp.next = listNode;
            temp = listNode;
        }
        return head;
    }
    /**
     * 显示链表
     * @return
     */
    public void show(ListNode node) {
        if (node.next == null) {
            System.out.println("链表为空");
            return;
        }
        ListNode temp = node.next;
        while (temp != null) {
            System.out.println(temp);
            temp = temp.next;
        }
    }
}
```
### 15.反转链表
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-07 14:01
 * 输入一个链表，反转链表后，输出新链表的表头。
 *
 *个人解题思路：
 * 定义一个新链表，然后从头到尾遍历old链表，每遍历一个将其取出，放在新链表的最前端
 **/
public class Topic15 {
    public static void main(String[] args) {
        ListNode listNode = new ListNode().initList();
        listNode.show(listNode);
        System.out.println(ReverseList(listNode));
    }
    public static ListNode ReverseList(ListNode head) {
        if(head==null || head.next==null){
            return head;
        }
        ListNode newListNode = null;
        ListNode nextListNode = null;
        ListNode temp = head;
        while(temp!=null){
            nextListNode = temp.next;
            temp.next = newListNode;
            newListNode = temp;
            temp = nextListNode;
        }
        return newListNode;
    }
}
```
### 16.合并两个有序链表
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-07 19:04
 *
 * 输入两个单调递增的链表，输出两个链表合成后的链表，
 * 当然我们需要合成后的链表满足单调不减规则。
 *
 * 个人解题思路；
 *  我们可以判断两个链表的第一个节点大小，谁小就放前面
 *  然后再判断当前链表的节点大小和第二个链表的下一个节点大小
 *  谁小就把谁放前面 递归执行即可
 *  比如：
 *  链表一：1 2 3 4     链表二：6 7 8 9
 *  第一次:判断链表一的第一个元素1和链表二的第一个元素6的大小显然1<6
 *  所以1为第一个节点
 *  第二次：判断链表一的第二个元素2和链表二的第一个元素6的大小 显然2<6
 *  所以2为第二个节点
 *  以此递归即可
 **/
public class Topic16 {
    public static void main(String[] args) {
        ListNode listNode1 = new ListNode().initList();
        ListNode listNode2 = new ListNode().initList();
        System.out.println(Merge(listNode1, listNode2));
    }
    public static ListNode Merge(ListNode list1,ListNode list2) {
        if (list1==null){
            return list2;
        }
        if (list2==null){
            return list1;
        }
        //链表一的值小于链表二
        if (list1.value<=list2.value){
            //开始递归
            list1.next = Merge(list1.next, list2);
            return list1;
        }else {
            list2.next = Merge(list1, list2.next);
            return list2;
        }
    }
}

```
### 17.树的子结构
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-08 16:
 * 输入两棵二叉树A，B，判断B是不是A的子结构。
 * （ps：我们约定空树不是任意一个树的子结构）
 * <p>
 * 解题思路：
 * 1.找到A中和B的根节点相同的节点，然后进行判断是否相同。
 * 2.如果不同再拿A的左子树和B进行比较。
 * 3.如果仍不同再拿A的右子树与B进行比较。
 * 4.如果仍未找到，则A中不包含B。
 * 判断两个根节点相同的两个树是否包含：
 * 1.先判断B,如果B为空说明包含。
 * 2.再判断A，如果A为空就说明不包含。
 * 3.如果A的值与B的值相同，然后继续进行此判断。
 **/
public class Topic17 {
    /**
     * 遍历大树判断
     * @param root1
     * @param root2
     * @return
     */
    public static boolean HasSubtree(TreeNode root1, TreeNode root2) {
        if (root1 == null || root2 == null) {
            return false;
        }
        //根节点相同
        if (root1.val == root2.val) {
            //向下继续遍历小树
            if (isContain(root1, root2)) {
                return true;
            }
        }
        //根节点不相同，遍历左右子树看是否有相同的
        return HasSubtree(root1.left, root2) || HasSubtree(root1.right, root2);
    }
    /**
     * 遍历小树判断
     *
     * @param root1
     * @param root2
     * @return
     */
    public static boolean isContain(TreeNode root1, TreeNode root2) {
        if (root2 == null) {
            return true;
        }
        if (root1 == null) {
            return false;
        }
        //遍历小树根节点相同
        if (root1.val == root2.val) {
            //遍历左右孩子
            return isContain(root1.left, root2.left) && isContain(root1.right, root2.right);
        }
        return false;
    }
}
```
### 18.二叉树的镜像
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-09 19:01
 * 操作给定的二叉树，将其变换为源二叉树的镜像。
 *
 * 个人解题思路：
 * 先前序遍历这棵树的每个结点，如果遍历到的结点有子结点，就交换它的两个子节点，
 * 当交换完所有的非叶子结点的左右子结点之后，就得到了树的镜像
 **/
public class Topic18 {

    public void Mirror(TreeNode root) {
        if (root == null){
            return;
        }
//        if (root.left==null && root.right==null){
//            return;
//        }
        //创建临时节点进行左右子树交换
        TreeNode temp = root.left;
        root.left = root.right;
        root.right = temp;
        //左右递归进行
        if (root.left!=null) {
            Mirror(root.left);
        }
        if (root.right!=null) {
            Mirror(root.right);
        }
    }
}
```
### 19.顺时针打印矩阵
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-09 19:16
 * 输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，
 * 例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
 * 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.
 *
 * 个人解题思路：
 *   1  2  3  4
 *   5  6  7  8
 *   9  10 11 12
 *   13 14 15 16
 *  我们可以按照一种魔方的思路 每次打印第一行数据后将数组逆时针旋转90°然后再打印第一行
 *  依次重复即可
 *
 **/
public class Topic19 {
    public static void main(String[] args) {
    int[][]arr = {{1,2,3,4},{5,6,7,8},{9,10,11,12},{13,14,15,16}};
        System.out.println(printMatrix(arr));
    }
    public static ArrayList<Integer> printMatrix(int [][] matrix) {
        ArrayList<Integer> arrayList = new ArrayList<>();
        int row = matrix.length;
        while (row > 0){
            for (int i = 0; i < matrix[0].length ; i++) {
                arrayList.add(matrix[0][i]);
            }
            matrix = reverseArray(matrix);
            row = matrix.length;
            if (row==1){
                for (int i = 0; i < matrix[0].length ; i++) {
                    arrayList.add(matrix[0][i]);
                }
                break;
            }
        }
        return  arrayList;
    }
    public static int[][] reverseArray(int[][]arr){
        int[][]newArr = new int[arr[0].length][arr.length-1];
        for (int i = 0; i < newArr.length ; i++) {
            for (int j = 0; j < newArr[0].length ; j++) {
                newArr[i][j] = arr[j+1][newArr.length-1-i];
            }
        }
        return newArr;
    }
}

```
### 20.包含min函数的栈
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-10 09:
 *
 * 定义栈的数据结构，
 * 请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。
 *
 * 个人解题思路：
 * 对于push操作
 * 每次压入的数据newNum都push进数据栈中，然后判断最小栈是否为空，如果为空那也把newNum同步压入
 * 最小栈中如果不为空，就先比较newNum和最小栈中栈顶元素的大小，如果newNum较大，那就不压入最小栈里，否则
 * 就同步压入最小栈里
 *
 **/
public class Topic20 {
    public static void main(String[] args) {
        Solution solution = new Solution();
        solution.push(3);
        solution.push(4);
        solution.push(5);
        solution.push(1);
        solution.push(2);
        solution.push(1);
        System.out.println(solution.min());
        System.out.println(solution.minData);
        System.out.println(solution.data);
    }
}
class Solution {
    //数据栈
    Stack<Integer> data = new Stack();
    //最小值栈
    Stack<Integer> minData = new Stack();

    public void push(int node) {
        data.push(node);
        if (minData.isEmpty()){
            //最小栈为空则push
            minData.push(node);
        }else {
            //取出最小栈顶的最小值与node比较
            int min = minData.peek();
            if (node <= min) {
                minData.push(node);
            }else {
                minData.push(min);
            }
        }
    }

    public void pop() {
        data.pop();
        minData.pop();
    }

    public int top() {
        return data.pop();
    }

    public int min() {
        return minData.peek();
    }
}
```
### 21.栈的压入弹出序列
```java
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-13 08:30
 *
 *
 * 输入两个整数序列，第一个序列表示栈的压入顺序，
 * 请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。
 * 例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，
 * 但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）
 **/
public class Topic21 {
    public static void main(String[] args) {
        int []arr = new int[]{1,2,3,4,5};
        int []arr2 = new int[]{4,3,5,1,2};
        System.out.println(IsPopOrder(arr, arr2));
    }
    public static boolean IsPopOrder(int [] pushA,int [] popA) {
        if (pushA.length==0 || popA.length==0){
            return false;
        }
        int index = 0;
        Stack<Integer> stack = new Stack<>();
        //将pushA中的元素依次入栈 如果遇到栈顶元素和popA数组中的元素一样时，则出栈
        for (int i = 0; i < pushA.length; i++) {
            stack.push(pushA[i]);
            //判断栈是否为空 以及栈顶元素是否和popA中的元素相等
            while (!stack.isEmpty() && (stack.peek()== popA[index])){
                stack.pop();
                index++;
            }
        }
        return stack.isEmpty();
    }
}
/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-13 08:30
 *
 *
 * 输入两个整数序列，第一个序列表示栈的压入顺序，
 * 请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。
 * 例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，
 * 但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）
 **/
public class Topic21 {
    public static void main(String[] args) {
        int []arr = new int[]{1,2,3,4,5};
        int []arr2 = new int[]{4,3,5,1,2};
        System.out.println(IsPopOrder(arr, arr2));
    }
    public static boolean IsPopOrder(int [] pushA,int [] popA) {
        if (pushA.length==0 || popA.length==0){
            return false;
        }
        int index = 0;
        Stack<Integer> stack = new Stack<>();
        //将pushA中的元素依次入栈 如果遇到栈顶元素和popA数组中的元素一样时，则出栈
        for (int i = 0; i < pushA.length; i++) {
            stack.push(pushA[i]);
            //判断栈是否为空 以及栈顶元素是否和popA中的元素相等
            while (!stack.isEmpty() && (stack.peek()== popA[index])){
                stack.pop();
                index++;
            }
        }
        return stack.isEmpty();
    }
}

```
### 22.从上往下打印二叉树
```java
import java.util.ArrayList;

/**
 * @program: Arithmetic
 * @description:
 * @author: wang_sir
 * @create: 2020-10-22 16:05
 *
 *
 * 从上往下打印出二叉树的每个节点，同层节点从左至右打印。
 **/
public class Topic22 {
    ArrayList<Integer> arrayList = new ArrayList<>();
    public  ArrayList<Integer> PrintFromTopToBottom(TreeNode root) {
        /**判断根节点是否为空*/
        if (root==null){
            return arrayList;
        }
        /**添加根节点进集合*/
        arrayList.add(root.val);
        bfs(root);
        return arrayList;
    }
    /**
     * 定义bfs方法 递归搜索左右子树
     * @param root
     */
    public void bfs(TreeNode root){
        if (root==null){
            return;
        }
        if (root.left!=null){
            arrayList.add(root.left.val);
        }
        if (root.right!=null){
            arrayList.add(root.right.val);
        }
        bfs(root.left);
        bfs(root.right);
    }
}

```
