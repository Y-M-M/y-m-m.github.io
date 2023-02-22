+++
title = "排序的整理"
description = "Ymmald, an interesting person."
date = "2023-2-22"

author = "Ymmald"
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

 ## 桶排序

 ## 堆排序

 ## 插入排序

 ### 基本思路
 - 第一个元素视为有序
 - 从第二个元素开始，直到最后一个元素，将每个元素插入前面的有序序列中

 ### C语言实现

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
