# 冒泡排序

```
public class BubbleSort{        
  public int[] sort(int[] a) {              
  int[] array=a.clone(); // 将传递的数组参数a克隆对象，不改变a数组的值              
  for (int i = 0; i<array.length-1;i++) { //总共进行length -1 趟排序                       
    for (int j = 0; j <array.length-1-i;j++) {                                
        if (array[j + 1] < = array[j]) {                                      
           int temp = array[j];                                        
           array[j] = array[j + 1];                                        
           array[j + 1] = temp;                                
        }                         
    }                 
  }             
  return  array;       
 }
}
```
