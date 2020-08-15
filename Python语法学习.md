
## Python的内建方法
```python
a=list([iterable])  # 将一个可迭代对象转换成列表,转换后是新的对象 
b=tuple([iterable]) # 将一个可迭代对象转换成元组 
c=str(obj)  #将对象转换成字符串 d=len(sub) # 返回sub参数的长度


sum(iterable[,start])  # 返回序列 iterable 的所有元素的总和 ，start参数默认是 0

sorted(iterable,key=None,reverse=False) # 使用方法与列表的内建方法sort()一致，但返回排序后的新列表,而不影响原列表

reversed(sequence) #列表的内建方法是原地翻转，而reversed()是返回一个翻转后的迭代器对象。你没看错，它不是返回一个列表，而是返回一个迭代器对象。
list1=[1,18,13,0,-98] 
reversed(list1) 
<list_reverseiterator object at 0x00000288185904F0> 
for each in reversed(list1): 
...     print(each,end=',') 
...     -98,0,13,18,1,

enumerate(iterable) # 生成由二元组构成的一个迭代对象，每个二元组由可迭代参数的索引号以及对应的元素组成。
str1='Fishc'
for each in enumerate(str1): 
...     print(each) 
...     (0, 'F') (1, 'i') (2, 's') (3, 'h') (4, 'c')

zip（）# zip（）方法用于返回由各个可迭代参数共同组成的元组
list1=[1,3,5,7,9] 
str1='Fishc' 
for each in zip(list1,str1): 
...     print(each) 
...     (1, 'F') (3, 'i') (5, 's') (7, 'h') (9, 'c')
```
## 函数的参数和返回值
```python
# 如果返回多个值，默认是以元组形式打包 
def duo_ge_zhi(): 
... return 1,2,3,'what' 

duo_ge_zhi() 
...(1, 2, 3, 'what')

# 关键字参数：在传入参数时明确指定形参的变量名，就可以不分位置。
def eat(body,thing):
    print('%s 把 %s 吃了'%(body,thing))

eat('小王','蛋糕')
小王 把 蛋糕 吃了
eat(thing='面包',body='小李')
小李 把 面包 吃了

# 默认参数：为参数指定默认的值
def helloWorld(name='徐二',word='HelloWord'):
    print('%s说%s'%(name,word))

helloWorld()
徐二说HelloWord

#在定义函数的时候，位置参数必须在默认参数的前面

# 可变参数：函数也不知道调用者实际上会传入多少个参数。 ` 是将参数打包成元组，** 是打包成字典。
def test(*p)
    print('有%d个参数'%len(p))
    print('第二个参数是：',p[1])

# 如果定义的函数中带有可变参数，那么可将其他参数设置为默认参数。否则在调用时，Python都会把参数算在可变参数中，引发报错。
print(*objects,sep='',end='\n',file=sys.stdout,flush=False)
```

## 函数的变量作用域
```python
# 函数内部只能访问局部变量，而不能改写全局变量。除非给变量加上global关键字。
count=5
def myFun():
    global count
    count=10
    print(count)

myFun()
10

# 函数里面可以内嵌函数
def fun1():
    print('fun1正在被调用')
    def fun2():
        print('fun2正在被调用')
    fun2()

fun1()
fun1正在被调用
fun2正在被调用

# 名字一样、作用域不同的变量引用，Python引入了LEGB原则进行规范。
# Local:函数内的名字空间
# Enclosing function locals：嵌套函数中外部函数的名字空间
# Global：函数定义所在模块的名字空间
# Builtin：Python内置模块的名字空间

# 闭包：内部函数保存外部函数的变量引用
# 什么是闭包？一个持有外部环境变量的函数就是闭包,即“封闭外部状态”。一个函数怎么才叫“能封闭外部状态”呢？当外部状态的scope失效的时候，还还有一份留在内部状态里面。有3个关键点来理解：
# 1.函数:funY  2.自由变量:y 3.环境:x
def funX(x):
    def funY(y):
        return x*y # funY里引用了外部函数funX的变量x
    return funY

temp=funX(8)
temp(5)
40

# 在内部函数中，只能对外部函数的局部变量进行访问，但不能修改。在函数中，只能对全局变量进行访问，但不能进行修改。

#内部函数访问外部函数的变量，但不能修改
def funX():
    x=5
    def funY():
        x=x+1 # 当要修改的时候，Python认为在内部函数的x是内部函数的局部变量，外部函数的x就被屏蔽了，所以找不到x变量的值就报错。
        return x
    return funY()

temp=funX()
temp()

error:local varibale 'x' referenced before assignment

# 可以使用nonlocal关键字告诉Python这不是局部变量
def funX():
    x=5
    def funY():
        nolocal x
        x=x+1
        return x
    return funY

temp=funX()
temp()

6
```

## 函数的装饰器
```
@buffer
@performance
@log
def eat(name):
    print('%s 开始吃了'%name)

# 调用eat()的时候，相当于调用buffer(performance(log(eat)))
# @a funb()类似于在a函数的环境下执行b函数的功能。有点接近闭包的概念。
```
## lambda 表达式
```python
# lambda x:2*x+1 左侧为参数，右侧为返回值，lambda表达式返回的是一个函数对象

g=lambda x,y:x+y
g(3,4)

7
```

## filter()内置函数
```python
# filter(function or None,iterable)
当第一个参数为None时，筛选出第二个参数里面为True的项目
当第一个参数为函数时，用第二个参数里面每一个项目执行函数，筛选出返回结果为True的项目。

def odd(x):
    return x%2

temp=filter(odd,range(10))
list(temp)
[1,3,5,7,9]

# lambda写法

list(filter(lambda x:x%2,range(10)))
[1,3,5,7,9]

```

## map()内置函数
```python
# map()会从所有可迭代对象中依次取一个元素组成一个元组，然后将元组传递给func。注意：如果可迭代对象的长度不一致，则以较短的迭代结束为止。
tuple(map(lambda x,y:x+y,[1,3,5,7,9],[1,2,3]))

(2, 5, 8)
```

## 递归
```python
# 求阶乘
def f(n):
    if n==1:
        return 1
    else:
        return n*f(n-1)
    
result=f(5)
```
![图片2](pics/2.png)

## 字典的最佳创建方法
```Python
# 使用内建函数dict()来创建字典。严格来说这是一个创建dict类的实例，可以使用dict类实例的内置方法。
dict=dict(F=70,i=105,s=115,c=(67,8,34))
print(dict2)

{'F': 70, 'i': 105, 's': 115, 'h': 104, 'c': (67,8,34)}
```

## 字典的最佳创建方法
```Python
# 访问字典的方法有keys()、values()和items()。
# keys()用于返回字典中的键
# values()用于返回字典中所有的值
# items()当然就是返回字典中所有的键值对（也就是项）。 

get(21) # get（）方法去访问字典项，当键不存在的时候，get()方法返回 None 
get(22,'木有') # 当22的键不存在时，返回'木有' 

31 in dict1 
False   # 代表键31不存在于 dict1 中 

clear() # 清空字典 
copy()#拷贝字典
```
## 集合
```python
# 集合最重要的特征是去重且无序

set1={1,2,3,4,5,5,6,7,9,1}
print(set1) {1, 2, 3, 4, 5, 6, 7, 9} 
```

## 文件操作
```python
# open() 函数打开文件返回文件对象 。经常与with语句出现。
open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None) 

f=open(r'C:\Users\xuchu\Desktop\helloworld.txt',encoding='utf-8',mode='a') 

f.write('\n底部还是上部') 

f.close()
```

## 异常类型
```python
# 断言异常
assert 3>4 

Traceback (most recent call last):   File "<input>", line 1, in <module> AssertionError

# AttributeError 尝试访问未知的对象属性

my_list.fuck Traceback (most recent call last):   
File "<input>", line 1, in <module> AttributeError: 'list' object has no attribute 'f'
```
| 类型        | 说明   |
| --------   | -----|
|indexError|超出索引序列的范围|
|KeyError|字典中查找一个不存在的关键字|
|NameError|尝试访问一个不存在的变量|
|OSError|操作系统产生的异常|
|SyntaxError|语法错误|
|TypeError|不同类型间的无效操作，比如 1+ '1'|
|ZeroDivisionError|除数为0|


## 异常处理
```python
try:
    检测范围
except Exception [as reason]:
    出现异常后的处理代码

# 针对不同异常设置多个except
try:
    f=open('我是一个文档.md')
    print(f.read())
    f.close()
except OSError as reason:
    print('文件出错啦，原因是'+str(reason))
except TypeError as reason:
    print('类型出错啦,原因是'+str(reason))

# finally：即使出错，也会执行完finally下的语句
try:      
    f=open('我为什么是一个文档.txt')      
    print(f.read())
except:      
    print('出错啦')
finally:      
    f.close()

# raise 抛出一个异常
try:
    raise TypeError('文件找不到')
except TypeError as reason:
    print(str(reason))
finally:
    print('抛出异常测试')

```
## else的用法

```python
# else：当不发上上面那件事的时候，干点什么。
while count>1:
    xxx
else:
    YYY


## with的用法
try:
    with open('data.txt','w') as f:
    for each_line in f:
        print(each_line)
except OSError as reason:
    print('出错啦'+str(reason))

## 多重继承
```python
class C(Base1,Base2):   pass
```

## 在构造方法中变相实现多重继承
```python
class Turtle:     
    def __init__(self,x):         
        self.num=x 

class Fish:     
    def __init__(self,x):         
        self.num=x 
    
class Pool:     
    def __init__(self,x,y):         
        self.turtle=Turtle(x)         
        self.fish=Fish(y) 
        
    def print_num(self):         
        print('水池里面总共有多少乌龟 %d 只，小鱼 %d 条'%(self.turtle.num,self.fish.num))
```

## 实例对象的属性会覆盖类对象的属性

```python
class A:
    num=10

a1=A()
a2=A()
a3=A()

def get_num(a1,a2,a3):
    print('a1的num为%d\na2的num为%d\na3的num为%d'%(a1.num,a2.num,a3.num))

a1.num=100
get_num(a1,a2,a3)

A.num=10000
get_num(a1,a2,a3)

a2.num=888
get_num(a1,a2,a3)

A.num=999
get_num(a1,a2,a3)
------------------------------------------------------------------
a1的num为100
a2的num为10
a3的num为10

a1的num为100
a2的num为10000
a3的num为10000

a1的num为100
a2的num为888
a3的num为10000

a1的num为100
a2的num为888
a3的num为999
```

## 类的一些BIF内建方法
| 方法        | 说明   |
| --------   | -----|
|issubclass（class,classinfo)|如果第一个参数（class）是第二个参数（classinfo）的一个子类，则返回True，否则返回False。|
|isinstance(object, classinfo)|第一个参数（object）是对象，第二个参数（name）是属性名（属性的字符串名字）。
hasattr(c1,'x')|
|getattr(object, name[, default])|返回对象指定的属性值，如果指定的属性不存在，则返回default（可选参数）的值；若没有设置default参数，则抛出ArttributeError异常。|
|setattr(object, name, value)|设置对象中指定属性的值，如果指定的属性不存在，则会新建属性并赋值。|
|delattr(object, name)|delattr()用于删除对象中指定的属性，如果属性不存在，则抛出AttributeError异常。|
|property(fget=None, fset=None, fdel=None, doc=None)|property()是一个比较“奇葩”的BIF，它的作用是通过属性来设置属性。property()返回一个可以设置属性的属性。相当于把属性再包装。x=property(getSize,setSize,delSize) |

## 魔法方法
__init__(self[,...])的返回值只能是None。魔法方法是用来定义类里面的一些隐性操作，比如初始化，比如获取或者设置某个属性时所发出的操作。


## 描述符
```python
class Celsius:
    def __init__(self,value=26.0):
        self.value=float(value)

    def __get__(self, instance, owner):
        return self.value

    def __set__(self, instance, value):
        self.value=float(value)

class Fahrenheit:
    def __get__(self, instance, owner):
        return instance.cel*1.8+32
    def __set__(self, instance, value):
        instance.cel=(float(value-32)/1.8)

class Temperature:
    cel=Celsius()
    fah=Fahrenheit()

temp=Temperature()
temp.cel=32
print(temp.cel)
print(temp.fah)


32.0
89.6
```

## 生成器表达式
```python
[i*i for i in range(10)]
... 
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

[i for i in range(100) if i%2==0 and i%3!=0]
[2, 4, 8, 10, 14, 16, 20, 22, 26, 28, 32, 34, 38, 40, 44, 46, 50, 52, 56, 58, 62, 64, 68, 70, 74, 76, 80, 82, 86, 88, 92, 94, 98]

{i:i%2==0 for i in range(10)}
{0: True, 1: False, 2: True, 3: False, 4: True, 5: False, 6: True, 7: False, 8: True, 9: False} #字典

{i for i in[1,1,2,3,333,3,3,45,6,7,7,7]}
{1, 2, 3, 6, 7, 45, 333} # 集合
```

## Python虚拟环境
```bash
# 检查是否安装了虚拟环境
virtualenv --version

# 安装虚拟环境  如果机器上安装了多个版本python
sudo pip install virtualenv # 安装python2的虚拟环境
sudo pip3 install virtualenv #安装python3的虚拟环境
virtualenv  --no-site-packages 创建路径名  #如果不想使用系统的包,加上–no-site-packeages参数

# 找不到virtualenv命令时配置环境变量
vim ~/.bashrc
#添加进.bashrc文件中
export PATH="~/.local/bin/:$PATH" # /.local/bin/这里放着virtualenv的程序位置
#运行下面命令让.bashrc文件生效
source ~/.bashrc

#激活虚拟环境
cd venv #进入虚拟环境文件夹
source ./bin/activate #运行activate脚本
> .\Scripts\activate.bat # 这是Windows的

#退出虚拟环境 linux
deactivate
#退出虚拟环境 Windows
.\Scripts\deactivate.bat
```



