## 二、数据结构

### 1、排序算法

#### 1）冒泡排序

```C++
for (int i = 0; i < arr.length-1; i++) {
    for(int j=arr.length-1;j>i;j--){
       if(arr[j]<arr[j-1]) {
         int temp=arr[j];
         arr[j]=arr[j-1];
         arr[j-1]=temp;
       }
    }
}
```





















