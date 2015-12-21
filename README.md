# java_algorithm

[![Support](https://img.shields.io/badge/IDE-Eclipse-blue.svg?style=flat)]()
[![Support](https://img.shields.io/badge/Lanuge-Java-blue.svg?style=flat)]()
[![Travis](https://img.shields.io/travis/rust-lang/rust.svg)]()
###java算法

`

package algorithm.minggo.sort;

/**
 * 测试各种排序算法，主要从下面几个方面说明 1.算法的稳定性 2.算法的时间复杂度 3.算法的空间复杂度。
 * 稳定性：1223 排序过程中第一个2和第二个2会交换位置。
 * 选择排序：选定数组第一个脚标当前最小开始，拿其他的逐一对比，选出最小作为当前最小最后放在第一个脚标位置。
 * 冒泡排序：选定数组第一个脚标当前最小，从数组尾部开始，相邻两个元素对比调整位置，一直往前滚动，直到脚标为当前脚标。
 * 插入排序：选定数组第二个脚标作为第一段数据，从选定数组的尾开始，相邻两元素比较调整位置，一轮一轮的滚动。
 * 快速排序：选出数组的中间脚标的数放到数组尾部，用A脚标为当前数组的0，B脚标为当前数组的尾脚标，两脚标相对前进直到A>B
 */
public class VarySort
{
    public static void main (String[] args)
    {
        int[] data = new int[]{3, 5, 1, 0, 8, 7, 9, 4, 5, 6};

        selectSort(data);//测试选择排序
       
        //bubbleSort(data);//测试冒泡排序
       
        //insertSort(data);//测试插入排序
       
        //shellSort(data);//测试希尔排序
       
        //quickSort(data);//测试快速排序
       
        //improvedQuickSort(data);
    }
   
    /**
     * 选择排序 1.稳定性:不稳定   2.时间复杂度:o(n2) 3.空间复杂度:o(1)
     * 算法思想简单描述：
     * 在要排序的一组数中，选出最小的一个数与第一个位置的数交换；
     * 然后在剩下的数当中再找最小的与第二个位置的数交换，如此循环
     * 到倒数第二个数和最后一个数比较为止。
     * @param data
     */
    public static void selectSort (int[] data)
    {  
     
        int lowIndex = 0;
       
        System. out.println ("before select sort" );
        printArr(data);

        for (int i = 0; i < data.length; i++)
        {
            lowIndex = i;
            for (int j = i + 1; j < data.length; j++)
            {
                if(data[j] < data[lowIndex])
                {
                    lowIndex = j;
                }
            }
            if(lowIndex != i)
            {
                swap(data, i, lowIndex);
              
            }
        }
       
        System. out.println ("\nafter select sort" );
        printArr(data);
    }
   
    /**
     * 冒泡排序   1.稳定性：稳定  2时间复杂度：o(n2)  3.空间复杂度o(1)
     * 算法思想简单描述：
     * 在要排序的一组数中，对当前还未排好序的范围内的全部数，自上
     * 而下对相邻的两个数依次进行比较和调整，让较大的数往下沉，较
     * 小的往上冒。即：每当两相邻的数比较后发现它们的排序与排序要
     * 求相反时，就将它们互换。
     * @param data
     */
    public static void bubbleSort (int[] data)
    {
      System. out.println ("before bubble sort" );
      printArr(data);
     
      for( int i=0; i<data.length ; i++)
      {
          for(int j=data.length-1; j>i; j--)
          {
              if(data[j] < data[j-1])
              {
                  swap(data, j, j-1);
              }
          }
      }
     
      System. out.println ("\nafter bubble sort" );
      printArr(data);
 
    }

    /**
     * 直接插入排序1.稳定性:稳定 2.时间复杂度:o(n2)  3.空间复杂度:o(1)
     * 在要排序的一组数中，假设前面(n -1) [n>=2] 个数已经是排
     * 好顺序的，现在要把第n个数插到前面的有序数中，使得这n个数
     * 也是排好顺序的。如此反复循环，直到全部排好顺序。
     * @param data
     */
    public static void insertSort(int[] data)
    {
        System. out.println ("before insert sort" );
        printArr(data);
        for(int i=1; i<data.length; i++)
        {
            for(int j=i; (j>0) && (data[j] < data[j-1]); j-- )
            {
                swap(data, j, j-1);
            }
        }
        System. out.println ("\nafter insert sort" );
        printArr(data);
    }
   
    /**
     * 希尔排序1稳定性:不稳定  2.时间复杂度:不确定  3.空间复杂度
     * 先将要排序的一组数按某个增量d分成若干组，每组中
     * 记录的下标相差d.对每组中全部元素进行排序，然后再用一个较小的增量
     * 对它进行，在每组中再进行排序。当增量减到1时，整个要排序的数被分成
     * 一组，排序完成。
     * @param data
     */
    public static void shellSort(int[] data)
    {
        System. out.println ("Before shell sort" );
        printArr(data);
       
        for(int i=data.length/2; i>2; i/=2)
        {
            for (int j=0; j<i; j++)
            {
                insertSort(data, j, i);
            }
        }
        insertSort (data, 0, 1);
       
        System. out.println("\nAfter shell sort" );
        printArr(data);
    }
   
    /**
     * 这是希尔排序中用到的一个辅助方法，是对数组中指定的一部分元素进行排序
     * 实质上是一个插入排序和重载的insertSort不同的是内循环中的条件，这个方法中
     * 的要求是变量大于等于步长，而另外一个是要求变量大于0
     * @param data 需要排序的数组
     * @param start 需要排序部分的开始
     * @param increament 步长
     */
    private static void insertSort(int[] data, int start, int increament)
    {
        for(int i=start+increament; i<data.length; i+=increament)
        {
            for(int j=i; (j>=increament) && (data[j] < data[j-increament]); j-=increament)
            {
                swap(data, j, j-increament);
            }
        }
    }
    /**
       * 递归快速排序
       * 1.取数组的中数，并与当前数组的最后元素调换位置。
       * 2.从数组的左脚标开始判断与中数大小，直到找到大于中数的元素停止，取该元素的脚标为当前左脚标。
       * 3.从数组的有脚标开始判断与中数大小，直到找到小于中数的元素停止，取钙元素的脚标为当前右脚标。
       * 4.交换左右脚标的元素（形成左边的元素小于中数，右边的元素大于中数），判断当前的左脚标是大于右脚标，退出循环。
       * 5.交换左右脚标的元素（循环中的最后一对左脚标和右脚标的元素肯定是做小右大，所以退出循环还原就是了）。
       * 6.将当前的左脚标元素与当前数组的最后一个元素位置调换。
       * 7.根据分开的两边数组进行递归到底，程序结束。
       * @param data
       * @param i 数组脚标被选择的最左边脚标值
       * @param j 数组脚标被选择的最右边脚标值
       */
     public static void quickSort(int[] data, int i,int j){
       int left = i-1;
       int right = j;
       int index = (i+j)/2;
       swap(data, index, j);
       do{
                 while(data[++left]<data[j]);
                 while(right!=0&&data[--right]>data[j]);
            swap(data, left, right);
       } while(left<right);
       swap(data, left, right);
       swap(data, left, j);
       if (left-i>1)
            quickSort(data, i, left-1);
       if (j-left>1)
            quickSort(data, left+1, j);
    }
    /**
     * 快速排序1稳定性：不稳定 2.时间复杂度：理想情况下是o(nlogn),最差为o(n2)  3.空间复杂度:o(logn)
     * 快速排序是对冒泡排序的一种本质改进。它的基本思想是通过一趟
     * 扫描后，使得排序序列的长度能大幅度地减少。在冒泡排序中，一次
     * 扫描只能确保最大数值的数移到正确位置，而待排序序列的长度可能只
     * 减少1。快速排序通过一趟扫描，就能确保某个数（以它为基准点吧）
     * 的左边各数都比它小，右边各数都比它大。然后又用同样的方法处理
     * 它左右两边的数，直到基准点的左右只有一个元素为止。
     * @param data
     */
    public static void quickSort(int[] data)
    {
        System. out.println("before quick sort" );
        printArr(data);
       
        quickSort(data, 0, data.length-1);
       
        System. out.println("\nafter quick sort" );
        printArr(data);
    }
   
   /* *//**
     * 快速排序的实现方法
     * @param data
     * @param i
     * @param j
     *//*
    private static void quickSort(int[] data, int i, int j)
    {
        int pivotIndex = (i + j) / 2;
        swap(data, pivotIndex, j);
        int k = partion(data, i-1, j, data[j]);
        swap(data, k, j);
        if((k-i)>1) quickSort(data,i,k-1);   
        if((j-k)>1) quickSort(data,k+1,j);   
    }
   */
    /**
     * 根据一个轴线，将数组分成两部分，并使左边的一部分数值都比轴线的数值小
     * 右边一部分的数值比轴线的数值大
     * @param data
     * @param l left
     * @param r right
     * @param pivot
     * @return
     */
    private static int partion(int[] data, int l, int r, int pivot)
    {
        do
        {
            while(data[++l] < pivot);//先++在判断的，如果++后符合条件会再++再判断。
            while(r!=0 && data[--r] > pivot);
            swap(data, l, r);
        }
        while(l < r);
        swap(data, l, r);
        return l;
    }
   
    /**
     * 改进后的快速排序
     * @param data
     */
    public static void improvedQuickSort(int[] data)
    {
        final int maxStackSize = 4096;
        final int threshold = 10;
       
        int[] stack = new int[maxStackSize];
       
        int top = -1;
        int pivot;
        int pivotIndex;
        int l, r;
       
        stack[++top] = 0;
        stack[++top] = data. length - 1;
       
        while(top > 0)
        {
            int j = stack[top--];
            int i = stack[top--];
           
            pivotIndex = (i + j) / 2;
            pivot = data[pivotIndex];
           
            swap(data, pivotIndex, j);
           
            l = i - 1;
            r = j;
           
            do
            {
                while(data[++l] < pivot);
                while(r != 0 && data[--r] > pivot);
                swap(data, l, r);
            }
            while(l < r);
            swap(data, l, r);
            swap(data, l, j);
           
            if((l - i) > threshold)
            {
                stack[++top] = l + i;
                stack[++top] = l - 1;
            }
            if((j - l) > threshold)
            {
                stack[++top] = l + 1;
                stack[++top] = j;
            }
        }
        insertSort(data);
    }
  
    /*
     * 还有归并排序，堆排序，基数排序
     * 以后再写
     * http://student.csdn.net/space.php?uid=42710&do=blog&id=23695
     * http://topic.csdn.net/u/20081220/16/fd902f7e-cba0-4adf-8812-e4cc48810830.html
     */
   
 
   
  
 
    //--------------------------------------------------------------------------------------//
    /**
     * 输出一个数组
     * @param data
     */
    private static void printArr(int[] data)
    {
        for(int i=0; i<data.length; i++)
        {
            System. out.print (data[i] + "    " );
        }
    }

    /**
     * 交换一个数组中的两个元素的位置
     * @param data
     * @param i
     * @param j
     */
    private static void swap(int[] data, int i, int j)
    {
        int temp = data[i];
        data[i] = data[j];
        data[j] = temp;
       
    }
}


`
