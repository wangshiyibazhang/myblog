---
title: 数组
date: 2017-10-07 15:08:07
tags: [javase, Array]
categories: javase
---
<h2>基本类型数组</h2>
*数组就是一种容器，可以用来保存多个相同类型的数据，数组中的数据被称为元素；<br/>
*数组中的数据可以是基本类型的数据也可以是引用类型是数据；<br/>
*数组本身就是一种引用类型分为引用和对象两部分<br/>

<!--more-->

*数组有一个从0开始按1递增的索引也叫数组下标<br/>
*动态初始化：我们将数组的声明，数组的创建，数组的初始化时分别进行的就叫数组的动态初始化
<h2>引用类型数组</h2>
在引用数组对相同中数组元素是一个个的引用，该引用分别指向一个个的该类型的对象<br/>
注意：在引用类型的数组中，数组元素永远都是一个个的引用；是绝对 不能存放对象的
<h2>数组的两种简单排序</h2>
1．冒泡排序：N个元素的数组要比较N-1轮，总共比较的次数N*（N-1）/2，交换多次；
```
public void sort(int [] arr){
//外面的for循环控制的是比较的轮数;例如6个元素5轮比较
for(int i= arr.length-1;i>0;i--){
	//里面的for控制循环次数
	for(int j=0;j<i;j++){
		if(arr[j]>arr[j+1]){
		int temp = arr[j];
		arr[j]= arr[j+1];
		arr[j+1]=temp;				
}}}}
```

2.选择排序法：N个元素的数组要比较N-1轮，总共比较的次数N*（N-1）/2，交换次数少于冒泡排序
```
public void sort2(int [] arr){
		for(int i= 0;i<arr.length;i++){
			int min = i;
			for(int j=i+1;j<arr.length;j++){
				if(arr[min]>arr[j]){
					min = j;
				}
			}
			if(min!=i){
				int temp =arr[min];
				arr[min]=arr[i];
				arr[i]=temp;
			}
		  }
		}
```
<hr/>
<b>数组的缺点:数组对象一旦被创建就不可以在改变其长度,也就是说数组中只能存放一组数目固定的数据</b>
