### BIF 内建方法
```python
a=list([iterable])  # 将一个可迭代对象转换成列表,转换后是新的对象 
b=tuple([iterable]) # 将一个可迭代对象转换成元组
c=str(obj)  #将对象转换成字符串 
d=len(sub) # 返回sub参数的长度 #max(),min() sum(iterable[,start])  # 返回序列 iterable 的所有元素的总和 ，start参数默认是 0 sorted(iterable,key=None,reverse=False) # 使用方法与列表的内建方法sort()一致，但返回排序后的新列表,而不影响原列表 #列表的内建方法是原地翻转，而reversed()是返回一个翻转后的迭代器对象。你没看错，它不是返回一个列表，而是返回一个迭代器对象。 reversed(sequence) list1=[1,18,13,0,-98] reversed(list1) <list_reverseiterator object at 0x00000288185904F0> for each in reversed(list1): ...     print(each,end=',') ...     -98,0,13,18,1, # 生成由二元组构成的一个迭代对象，每个二元组由可迭代参数的索引号以及对应的元素组成。 enumerate(iterable) str1='Fishc' for each in enumerate(str1): ...     print(each) ...     (0, 'F') (1, 'i') (2, 's') (3, 'h') (4, 'c') ## zip（）方法用于返回由各个可迭代参数共同组成的元组 list1=[1,3,5,7,9] str1='Fishc' for each in zip(list1,str1): ...     print(each) ...     (1, 'F') (3, 'i') (5, 's') (7, 'h') (9, 'c') 

```
------------------------------------------------------------------------------ tuple1=(2,4,6,8,10) for each in zip(list1,str1,tuple1): ...     print(each) ...     (1, 'F', 2) (3, 'i', 4) (5, 's', 6) (7, 'h', 8) (9, 'c', 10)