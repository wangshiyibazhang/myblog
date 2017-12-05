---
title: java常用类与对象池
date: 2017-10-07 15:58:57
tags: [javase, 常用类]
categories: javase
---
<h2>常用类</h2>
<ul>
	<li>在java中方法是对象的，属性是没有方法的，基本类型的变量只代表一个数值、字符、true/false;对象又要通过引用类型来调用
  </li>
	<li>java给8种基本类型提供了对应的引用类型称为包装器类：byte(Byte),int(Integer),short(Short),long(Long),float(Float),double(Double),char(character),boolean(Boolean);包装器是为了将8种数据类型能进行再对象上面的操作</li>
	<li>任何基本类型遇到字符串结果都是字符串</li>
	<li>两个Integer类型相加时会进行自动拆箱成int，如果返回类型为int时又会自动装箱，也就是Integer可以直接当做int类型使用</li>
</ul>
<!--more-->
```
public  static  void  test1(){
		//int 转换成Integer 的操作
		int i = 10;
		Integer j =  new Integer(i);
		Integer k = Integer.valueOf(i);
		Integer m = i;//JVM自动转换
		
		//Integer 转换成 int 的操作
     //	int h = x;//JVM自动转换	
	}
```
<h5>数值的精确运算</h5>
进行精确运算时应该将一个double转换成字符串然后将字符串转换成BigDecimal类型进行运算

```
//精确的除法运算
	public static double test2(double x1,double x2,int fale){
	//fale参数表示精确到小数点后的位数
      if(fale<0){
			throw new IllegalArgumentException();
		}
		BigDecimal b1 = new BigDecimal(Double.toString(x1));
		BigDecimal b2 = new BigDecimal(Double.toString(x2));
		return b1.divide(b2, fale, BigDecimal.ROUND_HALF_UP).doubleValue();
		
	}
```
<h5>格式化数值</h5>
格式化数值之前首先应该建立模板，可以通过相应的API文档查看用法
```
int value = 1332164648.123;
DecifalFormat df1 = new DecifalFormat("000,000,000,000,000.000");//表示没有数值时强制显示0，有数值显示数值；
DecifalFormat df1 = new DecifalFormat("###,###,###,###.###)；//表示有数值显示数值没数值就不显示；
String str = df1.format（value）；
```
<hr/>
<h2>对象池</h2>
在java中只要用到“ ”，来创建字符串对象，则该对象均会在对象池中出现，对象池是共享的，字符串底层实际就是char组成的
```
//以下代码创建了两个对象，一个对象池中，一个堆中；
	  String str = new String("Hello");
     //以下代码创建了3个对象，一个对象池，两个堆中
	  String str1 = new String("Hello");
	  String str2 = new String("Hello");
     *字符串对象一旦创建好其内容就不可改变
     //用这种拼接字符串的方式，如果拼接少量字符串比较方便  但是拼接大量字符串时会造成大量垃圾
	  String str3 = "Hello";
	  str3  = str3 +  "world";
```
字符串对象可以比较大小，也就是为字符串对象排序做好准备（compareTo）；