---
title: 集合(1)
date: 2017-10-11 17:54:28
tags: [javase, collection, List, set, hashset, Treeset]
categories: javase
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在javase中我们可以选择用数组来储存数据，但是我们知道数组在创建之后是不能改变其大小，所以我们只能在数组中储存固定长度的数据；相对于数组来说javase中给我们提供了更为方便的储存数据的方式集合。
<br/>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;集合是一种容器用来存放一种数目不固定的数据，集合满了之后可以自动扩充，而且只能存放引用类型的数据，不能存放基本类型的数据，对于基本类型的数组，存放基本类型数据后会自动装箱。<br/>

<!--more-->

 对集合的操作就是增，删，改，查，遍历<br/>
规定集合中只能装String类型数据，这就叫做泛型
```
	  Set<String> set = new HashSet<String>();
```

<br/>
首先我给出一个集合中的层次关系图：<br/>
注意：实现代表继承，虚线代表实现接口<br/>
![](http://ox8t0ws1t.bkt.clouddn.com/image/collection/%E9%9B%86%E5%90%88%E5%85%B3%E7%B3%BB%E5%9B%BE1.png)<br/>
通过上图我们可以看到collection为根接口;
<h2>Set</h2>
<ul>
<li>
在set集合中规定存放的数据的无序且不可重复的</li>
<li>set中添加数据的不可重复是指添加对象内容的不可重复，并不是值对象引用的不可重复</li>
</ul>
<h5>hashset</h5>
&nbsp;&nbsp;&nbsp;&nbsp;在hashset中直接实现了set接口，那么hashset是如何保证数据的不可重复性的？
<br/>
<ol>
	<li>将一个对象给hashset()中添加的时候，hashset自动调用该对象的hashcode()；给hashset()中添加第一个数据的时候它调用hashcode()方法得到一个int值num1,然后hashset()将得到的这个num1就进行了一系列的操作得到了一个num2，然后用num2%16，最后得到的这个结果就是hashset集合索引的位置，然后hashset就将这个数组放到了这个位置；</li>
	<li>当hashcode不同的时候，数据直接进入集合；当hashcode相同的时候，hashset()就会再次调用equals()，当equals返回true的时候不让对象进入集合，当返回false时，数据进入集合并以链表的方式尽心保存</li>
	<li>hashset()，就是用以上方法保证数据无序的进入集合中的</li>
<li>向hashset()中添加，查询和删除数据都会比较它的规则，即调用equals()和hashcode()方法；</li>
<li>如果要将一个对象加入hashset集合中就必须在这个对象中重写hashcode和equals方法；</li>
</ol>
以下就是在类中覆盖equals()和hashcode()的方法：


```
@Override
     public boolean equals(Object obj ){
	 if(this ==  obj){
	   	 return true;
	 }
	 if(obj instanceof Course){
		Course c = (Course) obj;
		if(this.name == c.name){
			return true;
		}
	 }
	 return false;
      }
    //重写hashcode（）方法时找到一个与该对象相关的int值相加后的结果乘以31
     public int hashCode(){
	  return name.hashCode()*31;
      }
```

<br/>
<b>注意:<br/>1.覆盖equals()的时候可以不覆盖hashcode();覆盖hashcode()的时候必须覆盖equals();通常情况下两个是一起覆盖的，覆盖hashcode/equals的时候要遵照相同的规则（比如：忽略大小写时要同步）；<br/>2.hashcode(),通常是指地址编号，equals()通常是指，对象所取得的值<br/>3.重写hashcode（）方法时找到一个与该对象相关的int值相加后的结果乘以31，得出的结果比较接近hashcode（）算法得到的值；</b>
<hr>
<h5>TreeSet</h5>
&nbsp;&nbsp;&nbsp;&nbsp;TreeSet可以保证数据的不可重复并且可以对数据进行排序；<br/>&nbsp;&nbsp;&nbsp;&nbsp;当我们要将一个对象类型的数据添加到TreeSet中的时候，该对象中就必须实现Comparable接口，并实现其中的compareto方法，并且在这个方法中实现学生数据的排序规则；<br/>&nbsp;&nbsp;&nbsp;&nbsp;当我们要将数据添加到TreeSet中的时候，TreeSet就会自动调用对象中的compareto方法进行比较，如果返回值为0时，就不让数据进入集合，然后根据返回的正数/负数，对数据进行正序/倒叙的排序<br/><font color="red">TreeSet就是通过以上方法保证数据的不可重复和可排序的</font>
<br/>&nbsp;&nbsp;&nbsp;&nbsp;TreeSet实现的方法有两种：<br/>a.学生对象自带的比较器就是在学生对象中覆盖compareTo方法，<br/>b.重新定义一个比较器类在TreeSet中之间new；
<br/>

```
//以下就是再类中覆盖的compareto方法
@Override
public int compareTo(Student o) {
	if(this.age >o.age){
		return 1;
	}
	
	if(this.age == o.age){
		return 0;
	}
	if(this.age <o.age){
		return -1;
	}
  if(this.name.compareTo(o.name)>0){
	  return 1;
  }
  if(this.name.compareTo(o.name)==0){
	  return 0;
  }
  if(this.name.compareTo(o.name)<0){
	  return -1;
  }
  return 0;
}  
}
```
<hr/>

<h2>List</h2>
&nbsp;&nbsp;&nbsp;&nbsp;List中存放的是有序的可重复的数据；<br/>
&nbsp;&nbsp;&nbsp;&nbsp;数组在内存中是一块连续的内存空间，数组在添加数据的时候需要频繁的移动内存；数组添加删除数据比链表添加删除数据慢，数组查询数据比链表快；
<h5>ArrayList</h5>
&nbsp;&nbsp;&nbsp;&nbsp;ArrayList就是通过数组的方式实现数据的增删查改；  


```
List<String> list = new ArrayList<String>();
    	//添加数据
    	list.add("hello1");
    	list.add("hello2");
    	list.add("hello3");
    	list.add("hello4");
    	list.add("hello5");
    	list.add("hello6");
    	list.add(1,"添加数据");
    	//修改数据
    	list.set(1, "修改数据");
    	//删除数据
    	String str = list.remove(1);
    	System.out.println("被删除的数据是："+str);
    	//查询数据
    	int index = list.indexOf("hello4");
    	if(index >=0){
    		System.out.println("hello4所在的索引位置是："+index);
    	}	
    	//遍历数组
    	Iterator<String> it = list.iterator();
    	while(it.hasNext()){
    		String str2 = it.next();
    		System.out.println(str2);
    	}
```


<hr/>

*LinkedList是通过链表的方式来实现的（链表在添加删除的时候不需要频繁移动内存）；
<hr/>




```
	List<String> list = new LinkedList<String>();        
    	//添加数据
    	list.add("hello1");
    	list.add("hello2");
    	list.add("hello3");
    	list.add("hello4");
    	list.add("hello5");
    	list.add("hello6");
    	list.add(1,"添加数据"); 	
    	//修改数据
    	list.set(1, "修改数据");
    	//删除数据
    	String str = list.remove(1);
    	System.out.println("被删除的数据是："+str);
    	//查询数据
    	int index = list.indexOf("hello4");
    	if(index >=0){
    		System.out.println("hello4所在的索引位置是："+index);
    	}
    	//遍历数组
    	Iterator<String> it = list.iterator();
    	while(it.hasNext()){
    		String str2 = it.next();
    		System.out.println(str2);
    	}
```


*Vector也是采用数组来实现的，代码和上面的都差不多；<br/>
注意：<br/>1.jdk包中的stack由于它是继承了Vector的方法，在Vector中有直接利用索引删除数据的方法indexof()，而stack也继承了这个方法，所以说不能直接用这个栈；<br/>2.List 接口除了可以通过Iterator进行迭代之外还提供了特殊的迭代器ListIterator，除了允许 Iterator 接口提供的正常操作外，该迭代器还允许元素插入和替换，以及双向访问。还提供了一个方法来获取从列表中指定位置开始的列表迭代器。
<hr/>
<font size="5px" color="blue">集合的删除：</font>在遍历集合的过程中，尽量不要通过集合的remove（），来删除数据，这样会导致集合状态和迭代器的状态不一致，如果删除后再次遍历集合会出现异常，所以一旦采用了集合的remove（）方法删除，那么就必须用return来中断循环；在遍历集合的过程中，可以使用迭代器的remove（），来删除数据；
<hr/>
ps:以上就是我对集合中set分支的总结以及一些注意事项，有空我也会将map的内容进行相关的梳理









