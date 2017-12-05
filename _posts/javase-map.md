---
title: 集合(2)
date: 2017-10-17 18:46:03
tags: [javase, map, collection, hashmap, Treemap]
categories: javase
---
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;除了List和Set之外，还有一种集合叫做map，它是一种通过键值一一映射的一种集合，并提供了3种collection视图，允许键集，值集，键-值映射关系查看集合；<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在这里我画了一张关于map集合的关系图

<!--more-->

<br/>![map集合关系图](http://ox8t0ws1t.bkt.clouddn.com/image/collection/map%E5%85%B3%E7%B3%BB%E5%9B%BE.png)<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在HashMap中插入的数据也是无序且不可重复的，它保证数据不可重复的原理和HashSet的原理相同点击[查看](http://wangshiyibazhang.club/2017/10/11/javase-collection/)实现不可重复的原理；<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;同样在TreeMap中的key(键)是不可重复且可以排序的，它具体的实现和TreeSet的实现原理相同。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<b>注意:</b>在以上的不可重复都是指的key(键)值得不可重复，value(键值)可以重复，当向集合中添加的key值重复时，集合会将旧的value替换为新的。<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HashMap和HashTable都要求作为key的类必须要覆盖hashcode/equals方法；
HashMap和HashTable的区别：
   HashMap：速度快（非线程安全），可以使用null作为key和value
   HashTable：速度慢（线程安全），不可以使用null作为key和value
<hr/>
Map中插入数据

```
 //HashMap，TreeMap和HashTable，除了创建类不同之外其他方法代码完全相同；   
	 Map<String ,String> map = new HashMap<String,String>();
		
	 map.put("aa", "hello1");
	 map.put("cc", "hello3");
	 map.put("ee", "hello5");
	 map.put("aa", "newhello1");//当key重复的时候新的value会替换原来的value	
```

<br/>

Map中遍历数据的几种方式:

```
//方法1：将集合中的value全部取出来放在集合中
	 Collection<String> coll = map.values();
	 for (String string : coll) {
	    System.out.println("value="+string);	
	}
 System.out.println("==================================");
//方法2：通过集合中的key得到相应的value
	  Set<String> set = map.keySet();
	  for (String key : set) {
		  String value = map.get(key);
		 System.out.println(key+"->"+value); 
		 
	}
	  System.out.println("==================================");
//方法3:通过entry遍历
	  Set<Map.Entry<String,String>> set1 = map.entrySet();
	  Iterator<Map.Entry<String, String>> it = set1.iterator();
	  while(it.hasNext()){
	   Map.Entry<String, String> entry = it.next();
	    String key = entry.getKey();
	    String value = entry.getValue();
	    System.out.println(key+"->"+value);
	  }
```
<b>ps：HashSet的底层是通过HashMap实现的,
TreeSet底层是通过TreeMap实现的，可以通过Debug查看</b>















