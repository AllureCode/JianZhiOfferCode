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
