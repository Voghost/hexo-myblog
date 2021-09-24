---
title: 算法与数据结构
date: 2021-04-20 18:58:46
katex: true
tags: 
    - 算法
categories:
    - 算法与数据结构
---

## 1. 线性表 `line-list`
### 1.1 顺序表
#### 1.1.1. 实现代码
```java
/**
 * 顺序表
 */
public class SeqList {

    private static final int MAX_SIZE = 1024;
    private final int[] lis = new int[MAX_SIZE];
    private int size;

    public SeqList() {
        size = 0;
    }

    /**
     * 在指定位置插入数据
     *
     * @param data     要插入的数据
     * @param position position 要插入的位置
     */
    public boolean insert(int data, int position) {
        if (position >= MAX_SIZE || position < 0) {
            System.out.println("位置参数错误");
            return false;
        }
        if (size >= MAX_SIZE) {
            System.out.println("位置已满");
            return false;
        }
        for (int i = size; i > position; i--) {
            lis[i] = lis[i - 1];
        }
        lis[position] = data;
        size++;
        return true;
    }

    /**
     * 根据位置删除数据
     *
     * @param position 删除位置
     * @return 是否删除成功
     */
    public boolean delete(int position) {
        if (position > size || position < 0) {
            System.out.println("位置参数错误");
            return false;
        }

        for (int i = position; i < size; i++) {
            lis[i] = lis[i + 1];
        }
        size--;
        return true;
    }

    /**
     * 根据位置获取数据
     * @param position 获取位置
     * @return 位置
     */
    public int get(int position) {
        if (position > size || position < 0) {
            System.out.println("位置参数错误");
            return -1;
        }
        return lis[position];
    }

}
```

#### 1.1.2 效率分析
1. 插入操作： 
    * 最好情况 从position = size , 最坏情况 position = 0
    * 设元素个数为$n$ 插入元素的位置有n+1种情况，当插入的位置等概率时, 有$p_i = \frac{1}{n+1}$.
    * 则需要移动元素的平均次数为 $\sum^{n}_{i=0}p_i(n-i)=\frac{1}{n+1}\sum^n_{i=0}(n-i)=\frac{n}{2}$

2. 删除操作:
    * 最好情况 从position = size - 1 , 最坏情况 position = 0
    * 设元素个数为$n$ 删除元素的位置有n种情况，当删除的位置等概率时, 有$p_i = \frac{1}{n}$.
    * 则需要移动元素的平均次数为 $\sum^{n}_{i=0}p_i(n-i)=\frac{1}{n}\sum^n_{i=0}(n-i)=\frac{n-1}{2}$
3. 综上， 无论删除或添加元素时间复杂度都为 $O(n)$







