+++
author = "Ymmald"
title = "各种排序算法的整理"
date = "2023-2-27"
description = "还需要完善～"

+++

# 排序整理
 
 ## 冒泡排序

 ### 基本思路
 - n-1趟将n个数据排序
 - 每次交换相邻数据，将最大的数冒泡到最后

 ### C语言实现
```c
#include <stdio.h>
void bubble(int *arr, int len);
int main(){
    int arr[] = {11, 3, 5, 18, 20, 34, 54, 23, 7, 6};
    int len = (int)sizeof(arr)/sizeof(*arr);//计算数组长度
    printf("len = %d\n", len);
    bubble(arr, len);
    for(int i = 0; i < len; i ++){
        printf("%d%c", arr[i], " \n"[i == len - 1]);
    }
}

void bubble(int *arr, int len){
    int temp;
    for(int i = len; i > 1; i --)//走n-1遍，每次冒泡所得为len - 1
    {
        for(int j = 0; j < i; j ++)//冒泡到i-1（len-1）
        {
            if(arr[j] > arr[j + 1]){
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}
```

### 遇到的问题
- 计算数组长度
- 处理内外两循环的终点/次数


## 选择排序

### 基本思路
- 寻找一组数据中最大的数，与最后一个数交换
- 对剩下的数重复

### C语言实现
```c
#include <stdio.h>
void swap(int *a, int *b);
void option(int arr[], int len);

int main(){
    int arr[] = {1, 4, 2, 78, 34, 45, 98, 23, 89, 23, 45, 54, 34};
    int len = (int)sizeof(arr) / sizeof(*arr);
    option(arr, len);
    for(int i = 0; i < len; i ++){
        printf("%d%c", arr[i], " \n"[i == len - 1]);
    }
    return 0;
}

void swap(int *a, int *b){
    int temp = *a;
    *a = *b;
    *b = temp;
}

void option(int arr[], int len)
{
    int max = 0;;
    for(int i = len - 1; i > 0; i --)
    {
        for(int j = 1; j <= i; j ++)
        {
            if(arr[j] > arr[max])
                max = j;
        }
        swap(&arr[max], &arr[i]);
        max = 0;
    }
}
```

## 快排

### 基本思路
- 找到一个标准，将比它小的数放到左边，比它大的数放到右边
- 在新区域中继续划定区域，直至区域长度缩小为2



### 算法实现
```c
#include <stdio.h>
#include <stdlib.h>
typedef struct range{
    int start, end;
}Range;

void exchange(int *m, int *n)
{
    int temp = *n;
    *n = *m;
    *m = temp;
}

Range give(int start, int end)
{
    Range range;
    range.start = start;
    range.end = end;
    return range;
}

void quick(int *arr, int len);

int main()
{
    int arr[] = {1, 34, 65, 45, 39, 23, 44, 5, 6, 245, 56, 34, 26, 90};
    int len = (int)sizeof(arr) / sizeof(*arr);
    printf("len = %d\n", len);
    quick(arr, len);
    for(int i = 0; i < len; i ++)
    {
        printf("%d%c", arr[i], " \n"[i == len - 1]);
    }
    return 0;
}

void quick(int *arr, int len)
{
    if(len < 0)
    {
        return ;
    }
    Range r[len];
    int p = 0;
    r[p ++] = give(0, len - 1);
    while(p)
    {
        printf("p = %d\n", p);
        Range region = r[--p];
        if(region.start > region.end)
            continue;
        int mid = arr[(region.start + region.end) / 2];
        printf("mid = %d\n", mid);
        int left = region.start, right = region.end;
        printf("left = %d, right = %d\n", left, right);
        do
        {
            while(arr[left] < mid)
                left ++;
            while(arr[right] > mid)
                right --;
            printf("left = %d, right = %d\n", left, right);
            if(left <= right)
            {
                exchange(&arr[left], &arr[right]);
                left ++;
                right --;
            }
            for(int i = 0; i < len; i ++)
            {
                printf("%d%c", arr[i], " \n"[i == len - 1]);
            }
        } while (left <= right);
        if(left < region.end)
            r[p++] = give(left, region.end);
        if(right > region.start)
            r[p++] = give(region.start, right);
        for(int i = 0; i < len; i ++)
        {
            printf("%d%c", arr[i], " \n"[i == len - 1]);
        }
    } 
}
```

### 遇到的问题
- 用p控制循环是否结束，只有当p=0，而且p没有自加1的时候才会结束


## 计数排序

### 基本思路
- 给定排序的数在一定范围内
- 从小到大统计每个数的数目
- 将数按顺序记录到另一个数组中，完成排序

### c语言实现
```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
void arrange(int *arr, int *sort, int n);

int main()
{
    int n = 10;
    srand(time(0));
    int *arr = (int *) malloc(sizeof(int) * n);
    int *sort = (int *) malloc(sizeof(int) * n);
    for(int i = 0; i < n; i ++)
    {
        arr[i] = rand() % 100;
    }
    arrange(arr, sort, n);
    for(int i = 0; i < n; i ++)
    {
        printf("%d%c", sort[i], " \n"[i == n - 1]);
    }
    free(arr);
    free(sort);
}

void arrange(int *arr, int *sort, int n)
{
    int *count = (int *)malloc(sizeof(int) * 100);//需要被排列的数的范围是100以内
    for(int i = 0; i < 100; i ++)
    {
        count[i] = 0;
    }
    for(int i = 0; i < 10; i ++)
    {
        count[arr[i]] ++;
    }
    for(int i = 0; i < 10;)
    {
        for(int j = 0; j < 100; j ++)
        {
            while(count[j] > 0)
            {
                sort[i] = j;
                count[j] --;
                i ++;
            }
        }
    }
    free(count);
}
```

## 桶排序

### 基本思路
- 就是计数排序嘛……

### c语言实现
```c
#include <stdio.h>
#include <stdlib.h>
void arrange(int *arr, int *sort, int len);
int main()
{
    int arr[] = {1, 8, 23, 44, 29, 23, 94, 38, 22, 33, 44};
    int len = sizeof(arr) / sizeof(int);
    //printf("len = %d\n", len);
    int *sort = (int *)malloc(sizeof(int) * len);
    arrange(arr, sort, len);
    for(int i = 0; i < len; i ++)
    {
        printf("%d%c", sort[i], " \n"[i == len - 1]);
    }
    free(sort);
}

void arrange(int *arr, int *sort, int len)
{
    int max = arr[0];
    for(int i = 1; i < len; i ++)
    {
        if(arr[i] > max)
            max = arr[i];
    }
    int *count = (int *) malloc(sizeof(int) * (max + 1));
    for(int i = 0; i <= max; i ++)
    {
        count[i] = 0;
    }
    for(int i = 0; i < len; i ++)
    {
        count[arr[i]] ++;
    }
    for(int i = 0; i < len; )
    {
        for(int j = 0; j <= max; j ++)
        {
            while(count[j] > 0)
            {
                sort[i] = j;
                i ++;
                count[j] --;
            }
        }
    }
    free(count);
}
```

### 出现的问题

- 申请的桶应该比最大的数多一个，循环也应该循环到等于最大的数的时候


## 堆排序

### 基本思路
- 两个一组，与前面的数比较，将比较大的数放到前面
- 将第一个最大的数移到最后
- 将第一个数和最后一个数交换
- 缩小范围，重复操作


### c语言实现
```c
#include <stdio.h>
#include <stdlib.h>
void swap(int *x, int *y)
{
    int temp = *y;
    *y = *x;
    *x = temp;
}

void arrange(int *arr, int len);
void lit(int *arr, int start, int end);

int main()
{
    int arr[] = {1, 5, 2, 3, 35, 32, 55, 66, 45, 98, 34, 45, 55, 66, 77, 34, 38, 92};
    int len = (int)sizeof(arr) / sizeof(*arr);
    arrange(arr, len);
    for(int i = 0; i < len; i ++)
    {
        printf("%d%c", arr[i], " \n"[i == len - 1]);
    }
    return 0;
}

void arrange(int *arr, int len)
{
    for(int i = len/2 - 1; i >= 0; i --)
    {
        lit(arr, i, len - 1);
    }
    for(int j = len - 1; j > 0; j --)
    {
        swap(&arr[0], &arr[j]);
        lit(arr, 0, j - 1);
    }
}

void lit(int *arr, int start, int end)
{
    int dad = start;
    int son = dad * 2 + 1;
    while(son <= end)
    {   if(son + 1 <= end && arr[son] < arr[son + 1])
        {
            son ++;
        }
        if(arr[dad] > arr[son])
        {
            return;
        }
        else
        {
            swap(&arr[son], &arr[dad]);
            dad = son;
            son = dad * 2 + 1;
        }
    }
}
```

### 遇到的问题
- 当son > end的时候应该停止，否则会打乱后面已经排好的顺序

 ## 插入排序

 ### 基本思路
 - 第一个元素视为有序
 - 从第二个元素开始，直到最后一个元素，将每个元素插入前面的有序序列中

 ### c语言实现

 ```c
 #include <stdio.h>
void insert(int *arr, int len);
int main(){
    int arr[] = {1, 34, 56, 32, 21, 12, 3, 7, 9, 5, 34, 77, 18, 25};
    int len = (int)sizeof(arr) / sizeof(*arr);
    insert(arr, len);
    for(int i = 0; i < len; i ++){
        printf("%d%c", arr[i], " \n"[i == len - 1]);
    }
    return 0;
}

void insert(int *arr, int len){
    int num;
    for(int i = 1; i < len; i ++)
    {
        num = arr[i];
        int j;
        for(j = i - 1; j >= 0; j --)
        {
            if(arr[j] < num){
                arr[j + 1] = num;
                break;
            }
            else{
                arr[j + 1] = arr[j];
            }
        }
        if(j < 0)
        {
            arr[0] = num;
        }
    }
}
```

### 遇到的问题
- 本来应该在遇到小于arr[i]的数的时候插入，但可能arr[i]就是最小的数，这时候要判断一下，把arr[i]放到arr[0]的位置


## 希尔排序
### 基本思路
- 将数据划分区块，分别进行插入排序

### c语言实现
```C
#include <stdio.h>
void range(int *arr, int len);
int main()
{
    int arr[] = {1, 4, 2, 9, 15, 98, 34, 56, 34, 55, 66, 64, 90, 43, 25, 44};
    int len = (int)sizeof(arr) / sizeof(*arr);
    //printf("len = %d\n", len);
    range(arr, len);
    for(int i = 0; i < len; i ++)
    {
        printf("%d%c", arr[i], " \n"[i == len - 1]);
    }
}

void range(int *arr, int len)
{
    int gap, i, j;
    for(gap = len >> 1; gap > 0; gap >>= 1)
    {
        for(int t = 0; t < len; t ++){
            printf("%d%c", arr[t], " \n"[t == len - 1]);
        }
        for(i = gap; i < len; i ++)
        {
            int temp = arr[i];
            for(j = i - gap; arr[j] > temp && j >= 0; j -= gap)
            {
                arr[j + gap] = arr[j]; 
            }
            arr[j + gap] = temp;//如果要插入的数最小，退出循环时，j<0，j+gap为第一个数；如果插入的数不是最小，退出循环时，j对应的数应在插入的数前面
        }
    }
}

```

### 遇到的问题
- 解决需要插入的数最小的问题
- 在最内层循环中 arr[i]的值不断变化，需要在进内层循环之时，将arr[i]记录为temp


## 归并排序

### 基本思路
- 借助另一个数组，逐层进行选择排序




### c语言实现


#### 迭代
```c
#include <stdio.h>
#include <stdlib.h>
void arrange(int *arr, int len);

int main()
{
    int arr[] = {1, 34, 23, 78, 34, 44, 32, 87, 95, 47, 34, 23, 38, 40, 24};
    int len = (int)sizeof(arr) / sizeof(*arr);
    printf("len = %d\n", len);
    arrange(arr, len);
    for(int i = 0; i < len; i ++){
        printf("%d%c", arr[i], " \n"[i == len - 1]);
    }
}

void arrange(int *arr, int len)
{
    int *copy = malloc(len * sizeof(int));//malloc的用法
    for(int seg = 1; seg <= len/2; seg <<= 1)
    {
        printf("seg = %d\n", seg);
        int place = 0;
        for(int first = 0; first < len; first += seg * 2)
        {
            int i = 0, j = 0;
            while((i < seg && i + first < len) || (j < seg && first + j + seg < len))
            {    
                printf("i = %d, j = %d\n", i, j);
                if(i == seg)
                {
                    while(j <= seg - 1 && j + first  + seg < len)
                    {
                        copy[place] = arr[first + seg + j];
                        j ++;
                        place ++;
                    }
                }
                else if(j == seg)
                {
                    while(i <= seg - 1)
                    {
                        copy[place] = arr[first + i];
                        i ++;
                        place ++;
                    }
                }
                else
                {   
                    if(arr[first + i] < arr[first + seg + j])
                    {
                        printf("arr[first + i] = %d\n", arr[first+i]);
                        copy[place] = arr[first + i];
                        i ++;
                        place ++;
                    }
                    else
                    {
                        printf("arr[first + seg + j] = %d\n", arr[first + seg + j]);
                        copy[place] = arr[first + seg + j];
                        j ++;
                        place ++;
                    }
                }
            }
        }
        for(int i = 0; i < len; i ++)
        {
            arr[i] = copy[i];
            printf("%d%c", arr[i], " \n"[i == len - 1]);
        }
    }
}
```

### 遇到的问题