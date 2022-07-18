# 函数

​	要调用一个函数，需要知道函数的名称和参数，比如求绝对值的函数`abs`，只有一个参数。可以直接从Python的官方网站查看文档：

链接：http://docs.python.org/3/library/functions.html#abs

## 函数基础

### 定义函数

多行代码的集合

```python
def 函数名():
    print(123)
    ...
函数名() #执行该函数
```

- 函数的意义：
  - 当我们的代码程序出席可重用的代码时，可以用函数解决（增强代码的重用性）；
  - 增强代码可读性；

- 注释:

  - 在写函数注释时，一般写在函数定义下一行，方便了解该模块的功能。

  - 格式为：把内容使用三个双引号引起来

- 注意：

  函数名本就是一个变量，再次使用同样的名称去定义一个变量时则会报错：

  ```python
  def get_data():
      print(123)
      print(456)
      
  get_data()
  #再以get_data定义变量时报错
  get_data = []#错误
  ```

### 参数

放在函数名后的()中作为参数进行传递，可以传递多个参数

```python
def send_email(x1):#x1便是参数（形参）
    """发送邮件"""
    msg = "给{}发送了一份邮件.foramt(x1)"
    print(msg)
send_email(x1)#（实参）
```

- 传参：

  - 关键字传参：和顺序无关

    ```python
    def send_email(x1,x2):#x1便是参数（形参）
        """发送邮件"""
        msg = "给{}发送了一份{}.foramt(x1,x2)"
        print(msg)
    send_email("小陈","邮件")#（实参）
    send_email("小林","留言")
    ```

  - 位置传参：按照参数先后顺序

    ```python
    def send_email(x1,x2):#x1便是参数（形参）
        """发送邮件"""
        msg = "给{}发送了一份{}.foramt(x1,x2)"
        print(msg)
    send_email(x1="小陈",x2="邮件")#（实参）
    send_email(x2="小林",x1"留言")
    ```

  - 混搭：关键字传参一定要排在位置传参后面

    ```python
    def send_email(x1,x2):#x1便是参数（形参）
        """发送邮件"""
        msg = "给{}发送了一份{}.foramt(x1)"
        print(msg)
    send_email("小陈",x2="邮件")#可以的
    send_email(x1="小林","留言")#这是不可以的
    ```

- 默认参数：默认值不能放在前面

  ```python
  def send_email(x1,x2="邮件"):#x1便是参数（形参），此处x2便是默认参数
      """发送邮件"""
      msg = "给{}发送了一份{}.foramt(x1)"
      print(msg)
  send_email("小陈")#这里x2不传参的话，默认就是"邮件"
  send_email("小陈","留言")#这里x2传参的话，参数就是"留言"
  ```

- 动态参数（*）：执行函数时，接收任意个以位置传递的参数

  - 此处的*表示的参数，不论下面send_email传递多少个元素，他都会打包成元素传递给函数作为参数
  
  ```python
  def send_email(*x1):#x1便是参数（形参）
      """发送邮件"""
      print(x1)
  send_email(123)
  send_email([123,345])#将列表打包成元素传递给函数作为参数,输出时，整体输出
  send_email({11,22,33})
  #(123)
  #([123,345])
  #({11,22,33})
  ```
  
- 执行函数，传参加*

  ```python
  def send_email(*x1):#x1便是参数（形参）
      """发送邮件"""
      print(x1)
  send_email(*123)
  send_email(*[123,345,(11,22)])#将列表打包成元素传递给函数作为参数,输出时会将列表里面的元素拆开输出。
  send_email(*{11,22,33}) 
  #(123,)
  #(123, 345,(11,22))
  #(33, 11, 22)
  
  ```

- **接收多个参数：关键子传参，将传入的参数当作字典

  ```python
  def send_email(**x1):
      print(x1)
  send_email(v1="lin",v2="周")
  #{'v1': 'lin', 'v2': '周'}
  ```

- 混合用*和**

  ```python
  def func(*x1,**x2):
      print(x1)
      print(x2)
  func(1,2,3,v1=0)
  #
  #(1, 2, 3)
  #{'v1': 0}
  ```

  - 潜规则：一般情况下为

  ```python
  def func(*arges,**kwarges):
      pass
  func()
  ```

### 返回值

```python
#定义函数，计算字符串中陈出现的次数
def get_count():
    test = "乘风破浪会有时"
    count = 0
    for item in test:
        if item == "乘":
            count += 1
    return count
#执行函数
#res=函数的返回值
res = get_count()
print(res)
#1
```

关于函数的返回值：

- 如果函数中没有出现return，那么默认值为return None;

- 函数一旦遇到return则立即终止程序；

- 关于return后面的值，什么都不加返回return None,return后面可以加任何的元素;

- return是专属于函数才能用的，不能单独出现在循环或者判断语句中，但是混搭可以使用：

  ```python
  def run():
      name = "lin"
      for i in range(10):
        return #跳出循环了，下面的age不会再执行
      age = 18
  res = run()
  #
  #None
  ```

- 关于print 和resturn

  ```python
  def run():
      name = "lin"
      print(name)
      for i in range(10):
          print(i)
          return
      print("6666")
  res = run()
  print(res)
  #lin
  #0
  #None
  ```

## 函数进阶

- 函数名是变量

  ```python
  def func():
      return 123
  v1 = func()#v1是变量，这里v1等于函数func()
  
  v2 = v1()#
  ```

  ```python
  num = 123
  age = 18
  def func():
      return 123
  data_list = [ num,sge,func() ]#func函数已经执行了有返回值，放在列表data_list中
  ```

- 函数参数可以传任意类型

  ```python
  def do():
      return "哈哈"
  def func(v1,v2):
      data = v2()
      print(data)
  res = func(123,do)
  print(res)
  #哈哈	None
  ```

  ```python
  def func(arg):
      return arg + 1
  def do(a1,a2):
      print(a2)
      res = a1(999)
      print(res)
      return  res
  data = do(func,123)
  print(data)
  #123	1000	1000
  #先执行do传递两个参数为func和123,然后打印a2，然后func = a1返回arg+1，最后返回res，然后打印data
  ```

- 练习2：

  ```python
  def do(arg,num):
      return arg + num
  def func(a1,a2,base):  #a1=do a2=do base=20
      v1 =a1(base,10) #v1=do(20,10) 30
      v2=a2(base,100)#v2=do(20,100) 120
      return v1+v2
  res = func(do,do,20)#150
  print(res)
  ```

### 作用域（全局和局部变量）

- 在python中是以函数作为作用域的,一个函数就是一个作用域；

- 全局作用域，默认情况下就只有一个作用域；

- 执行函数时，会为函数创建作用域，去寻找值，优先在自己的作用域里面找，如果没有再到上级作用域找；

  示例1:

  ```python
  num = 1000
  def func():
      name = "lsk"
      print(name)
      print(num)
  func()
  ```

  在局部作用域使用gloabal，强制引用全局变量；

  规范 ：

  - 全局变量都是大写；
  - 局部变量都是小写；

  示例2;

  ```python
  data_list = []
  def func():
      global data_list#强制data_list就是全局的那个data_list变量
      data_list.append(123)
  print(data_list)
  func()
  print(data_list)
  ```

  示例3：

  ```python
  DATA_LIST = [11,22]
  def func():
      global DATA_LIST 
      DATA_LIST  =  []
      name = 'lsk'
  func()
  ```

### 参数传递易错点(内存地址)

```python
#不可变类型
def func(v1):
    print(v1)
name = "lsk"
func(name)
#lsk
```

```python
def func(data):
    data.append(999)
data = [11,22,,33]
func(data)
print(data)
#[11, 22, 33, 999]
```

- python执行并传参时默认：引用、内存地址

  

- 函数递归：

  Python 也接受函数递归，这意味着定义的函数能够调用自身，这样做的好处是可以循环访问数据以达成结果

  ```python
  def recursion(k):
      if (k>0):
          result = k+recursion(k-1)
          print(result)
      else:
          result = 0
      return result
  print("\n\nRecursion Example Results")
  recursion(10)        
  ```

  ### Lambda

  lambda 函数是一种小的匿名函数。

  lambda 函数可接受任意数量的参数，但只能有一个表达式。

  ```python
  x = lambda a : a + 10
  print(x(5))
  ```

  ```python
  x = lambda a, b : a * b
  print(x(5, 6))
  ```

  

## 函数高级

### 迭代器

- 概念

  - 迭代器是访问集合元素的一种方式；
  - 可以被next()函数调用并返回一个值的对象就是迭代器；
  - 迭代器不但可以用于for，还可以用于next()；
  - 迭代器是一个可以记住遍历的位置的对象。
  - 迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。
  - 迭代器有两个基本的方法：**iter()** 和 **next()**

  ```python
  li = [1,2,3,4,5]
  g = iter(li)
  print(g,type(g))
  print(next(g))
  #1
  ```

  ```python
  import sys  # 引入 sys 模块
  list = [1, 2, 3, 4]
  it = iter(list)  # 创建迭代器对象
  while True:
      try:
          print(next(it))
      except StopIteration:
          sys.exit()
  ```

### 生成器

- 概念：如果在函数中出现yield关键字，那么这个函数就是生成器函数。

- 生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器

- 在调用生成器运行的过程中，每次遇到 yield 时函数会暂停并保存当前所有的运行信息，返回 yield 的值, 并在下一次执行 next() 方法时从当前位置继续运行

- 注意：
  -  函数时 序执行，遇到return语句最后一行代码就返回；
  - 如果想让一个函数变为生成器函数，只需要将函数中的return改为yield；
  - 执行生成器函数不会执行函数代码，得到一个生成器；
  - 在每次调用next()的时候，会执行生成器函数，遇到yield语句就返回；

```python
def func():
    print(123)
    yield 1
    print(456)
    yield 2
    print(789)
    yield 3
data = func()
for item in data:
    print(item)
#123	1	456	2	789
	
```

### 函数和模块：

#### 闭包

- 创建一个闭包需要满足以下几点:
  - 必须有一个内嵌函数
  - 内嵌函数必须引用外部函数中的变量
  - 外部函数的返回值必须是内嵌函数

- python中以函数为作用域；

- 可以在函数中嵌套另外一个函数，作用域同样现在内部函数内部找，然后再向外部函数找,如下；

  ```python
  name = "lsk"
  def outer():
      def inner():
          print(name)
      inner()
  outer()
  #lsk
  ```

  ```python
  name = "lsk"
  def outer():
      def inner():
          print(name)
      	return inner()#会执行inner函数，如果不加括号，那返回的就是inner函数的函数名，输出结果为None
  v = outer()
  #lsk
  ```

##### 线程池

​	线程池在系统启动时即创建大量空闲的线程，程序只要将一个函数提交给线程池，线程池就会启动一个空闲的线程来执行它。当该函数执行结束后，该线程并不会死亡，而是再次返回到线程池中变成空闲状态，等待执行下一个函数

- 线程池的使用

​	线程池的基类是 concurrent.futures 模块中的 Executor，Executor 提供了两个子类，即 ThreadPoolExecutor 和 ProcessPoolExecutor，其中 ThreadPoolExecutor 用于创建线程池，而 ProcessPoolExecutor 用于创建进程池

```python
# 定义一个准备作为线程任务的函数
def action(max_num):
    my_sum = 0
    for i in range(max_num):
        logger.info(threading.current_thread().name + '  ' + str(i))
        my_sum += i
    return my_sum
# 向线程池提交一个task, 50会作为action()函数的参数
future1 = pool.submit(action, 50)
```



#### 装饰器

- 什么情况下使用装饰器？

  在不改变原函数的基础上，想要在函数之前、之后定制某些功能。

- 闭包和装饰器的区别：

​		闭包传递的是变量，而装饰器传递的是函数，除此之外没有任何区别，或者说装饰器是闭包的一种，它只是传递函数的闭包。

```python
def x1(arg):
    #arg=原来的func函数
    def inner():
       return arg()
    return inner

@x1#不带括号，先执行x1函数，并获取他的返回值，再重新赋值给func函数
#func = x1(func)
def func():
   return 123
v1 = func()
print(v1)
#123
```

```python
def outer(func):
    def inner(*args,**kwarge)
    	return func(*args,**kwargs)
    return inner
```

```python
#带参数的装饰器，实现n次循环
def tt(count):
    def outer(func):
        def inner(*args,**kwargs):
            result = 0
            for i in range(count):
                data = func(*args,**kwargs)
                result += data
            return result
        return inner
    return outer
@tt(5)
def do(v1,v2):
    return v1 + v2
data = do(11,22)
print(data)
#165
```

### 数据结构

### 模块

- 模块和包

- 模块

  模块就是一个.py文件

- 包

  包含多个.py文件

- sys.path

  - 在执行python代码时，如果要导入某个模块，默认python寻找模块的路径：（前面找到之后，后面就不会继续找了）
  - pycharm会自动条件添加一个项目目录
  - 想控制pycharm去定义的路径下寻找模块。

  ```python
  import sys
  sys.path.append("寻找的绝对路径")
  ```

  ```python
  import sys
  for path in sys.path:
      print(path)
  
  D:\python\pythonProject\venv\Scripts\python.exe 
  #当前运行脚本所在的目录
  ```

#### 导入模块

- import

```python
-导入py文件的级别
-使用模块中的成员（函数）时，需要把全部路径都写上
```

- from xxx.xxx import  函数

```python
from sys impoet f1
#从sys模块调用f1函数，也可以导入多个,如果导入函数名重复可以使用as设置一个别名
-级别可以到成员
	from utils import f1
    from utils import f1,f2
    from utils import *	#导入所有
    from utils import f2 as u2	#设置别名f2=u2 
-使用时不需要写全路径
	from lsk.tset import db
    db.get_tales()
```

#### 内置模块：

##### json

​	json是一种轻量级的数据交换格式，易于人阅读和编写

​	Python 有一个名为 `json` 的内置包，可用于处理 JSON 数据

- 规则：
  - json中的字符串都是双引号；
  - json输出 之后是类似于集合的

```python
v1 = '{"name":"lsk","age":18，"hoby":[11,22,33]}'#这就是一个json格式
v1 = "{'name':'lsk','age':18}" #这个就不是 json格式
v1 = '{"name":"lsk","age":18,"hoby":(11,22,33)}'#这个也不是 json格式
```

- json.dumps

  将python数据类型转换成json格式的字符串（序列化）

```python
import json
# Python 对象（字典）：
x = {
  "name": "老大",
  "age": 63,
  "city": "Seatle"
}
# 转换为 JSON：
y = json.dumps(x,ensure_ascii=False)
# 结果是 JSON 字符串：
print(y)
```

**注：**如果python数据中有中文，ensure_ascii=False是为了转化之后能正常按照中文 显示

（这种是 属于特殊情况下）

- json.dumps进行转化时但不是对所有数据都序列化，支持列表如下：

| Python           | JSON   |
| :--------------- | :----- |
| dict             | object |
| list, tuple      | array  |
| str, unicode     | string |
| int, long, float | number |
| True             | true   |
| False            | false  |
| None             | null   |

- json.loads

  将json格式的字符串转换成python数据类型（反序列化）

```python
import json
# 一些 JSON:
x =  '{ "name":"Bill", "age":63, "city":"Seatle"}'
# 解析 x:
y = json.loads(x)
# 结果是 Python 字典：
print(y["age"])
```

##### time和datetime:

- 时间戳

```python
import time
v1 = time.time()
print(v1)
```

- datatime类型：对象

```python
import  datatime
v1 = time.datatime.new()
print(v1,type(v1))
```

```python
#时间相加减
from  datetime import datetime, timedelta
v1 = datetime.now()
v2 = v1 - timedelta(hours=3,seconds=500)
print(v2)
#2022-07-13 11:27:30.999333
```

- 字符串类型：

```python
import  datatime
v2 = time.datatime.new()
string_time = v2.strftime("%Y-%m-%d %H:%M:%S")
print(string_time,type(string_time))
```

##### **OS**

- 获取当前脚本的绝对路径：

```python
abs_path = os.path.abspath(_file_)
```

- 获取文件的上级目录

```python
bash_path = os.path.dirname(os.path.dirname("路径"))
```

- 拼接路径：

```python
import os
data = os.path.join("lsk","zhou")
print(data)
```

- 判断路径是否存在：


```python
os.path.exists()
```

- 罗列相对路径下所有的文件和文件夹


```python
os.listdir()
```

- 文件夹还是文件：


```python
os.path.isdir()
```

- 创建目录：

```python
import os 
file_path = os.path.join('db','oo','xo')
if not os.path.exists(file_path):
    os.makedirs(file_path)
```

##### md5加密

- hashlib，密码不能是明文

```python
import  hashlib
data_string = "林"
obj = hashlib.md5()
obj.update(data_string.encode('utf-8')) #转换成utf-8字节
result = obj.hexdigest()#得密文
print(result)
```

md5加密不可逆，但是可以被撞库。避免这种风险就需要加盐。

```python
obj = hashlib.md5("jlashah".encode('utf-8'))
```

##### 寻找目录下所有的文件和文件夹

```python
# 修改工作目录
import os
os.chdir(r'C:\Users\Hider\Desktop')
# 定义函数
def list_all_files(rootdir):
    import os
    _files = []
	# 列出文件夹下所有的目录与文件
    list = os.listdir(rootdir)
    for i in range(0, len(list)):
		# 构造路径
        path = os.path.join(rootdir, list[i])
		# 判断路径是否为文件目录或者文件
		# 如果是目录则继续递归
        if os.path.isdir(path):
            _files.extend(list_all_files(path))
        if os.path.isfile(path):
            _files.append(path)
    return _files
# 执行
dir = r'C:\Users\Hider\Desktop\python' # 目录地址
list_all_files(dir)
```

- 重命名文件夹或文件：

```python
import os 
os.rename("1.txt","2.txt")
#或者
import shuilt
shutil.move("1.txt","2.txt")
```

- 删除文件：

```python
os.remove("xxx")
```

- 删除文件夹

```python
shutil.rmtree("lll")
```

- 解压文件

```python
shutil.unpack_archive(filename='2022.zip',extract_dir='路径'，format='zip')
```

##### subprocess模块

用来生成子进程，并可以通过管道连接他们的输入/输出/错误，以及获得他们的返回值

-  subprocess.getstatusoutput()

  接受字符串形式的命令，返回 一个元组形式的结果，第一个元素是命令执行状态，第二个为执行结果

```python
subprocess.getstatusoutput('pwd')
```

-  subprocess.getoutput()

  接受字符串形式的命令，放回执行结果

```python
subprocess.getoutput('pwd')
```

##### sys

- sys.path

  导入文件默认寻找的路径

- sys.argv

  执行脚本时获取的参数

```python
import sys
print(sys.argv)
```

##### re模块

从文本中获取我们所需要的数据。

```python
import re
data = re.findall()
```



