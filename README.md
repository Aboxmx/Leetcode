# Leetcode
leetcode做题心得

## 说明
1. 模板代表当前题目的主体结构需要烂熟于心，作为难题的基本构件使用
2. 每个题目尽量给出自己认为比较好的解法

## 一些解题的心得
1. 对于递归算法：（合并有序链表）
  1. 递归流程：
     * 写出当前方法的功能
     * 写出子方法的功能
     * 写出当前方法与子方法的关系
     * 写出关系：减而治之，分而治之
     * 写出递归基
     * 写出返回值
  2. 递归设计策略
     * 写递归算法，即是在找问题的等价说法，并且这个等价说法还是包含这个问题的子问题，可以直接考虑递归算法的子问题，列出子问题，再寻找与问题的关系 

  
2. 对于数组相关的算法：（两数之和）
   * 找到对应的遍历模式（即for循环要写到条件反射的地步），一次遍历，二次遍历（取二元组），双指针......
   * 注意每一次枚举一个元素后，该循环必然执行的代码
   * 再特别注意，每次循环，通过条件判断所需执行的代码
  
3. 对于状态转换的算法：（爬楼梯）
    * 注意循环的时候，是一种转态切换，此时的i没有太多含义，仅仅代表状态变换的次数，与遍历数组不同
    * 一般会初始化状态1，所以对于一个求第n状态的程序，仅仅需要循环n-1次
     * 图：1->2->3->4 对于循环，可能循环体更像->,因为这标志着状态有1切换到2
  
## 一些注意点
1. 对于输入为数组，或字符串这两种引用类型，在赋值为空的情况下（即为初始化），idea会检测出错误，故我在做特判时，已经将这些情况排除在外了
     * 可能在动态生成的数组时，可能传入空参，这里我不会了o(╥﹏╥)o
     * 对于接受TreeNode之类的节点，可以通过在过程中node.left之类的传入参数，所以此时是运行时状态，需手动排除此类情况
