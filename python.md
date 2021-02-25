# 基础

## 变量和简单数据类型

### 字符串

#### 转义
 - 转义字符`\`
 - `\n`换行 `\t`制表符
 - 用`r''`表示`''`内部的字符串默认不转义

#### 换行
 - `\n`
 - 使用**三引号**`'''`的情况下可敲回车（行首显示`...`）

#### 布尔值
 - `True` `False`
 - 注意大小写
 - 可以使用`and` `or` `not`运算

#### 空值
 - `none`
 - Python中没有`null`

#### `title()`方法

 - 只最大化每个词的首字母，中间的大写会变成小写

```python
name = ('ada loVelace')
print(name.title())

## 返回结果
Ada Lovelace
```

#### `upper()` `lower()`

 - 全部大写/全部小写

#### `rstrip()`

 - 默认：删除字符串**结尾**的空白
 - `rstrip()`删除结尾字符是**暂时性**的
 - 填入参数：删除结尾的指定字符`rstrip('?')`

```python
>>> favorite_language = 
'python '
>>> favorite_language 
'python '
>>> favorite_language.rstrip() 
'python'
>>> favorite_language
'python '
```
```python
language = ' python 111111'
print(language)
print(language.rstrip('1'))
print(language)
### return
python 111111
python
python 111111
```

#### `lstrip()` `strip()`

 - `lstrip()`删除左侧空白或指定字符
 - `strip()`删除两侧空白或指定字符

#### Python2中的`print`
 - 可以不加括号

### 数字

 > 空格不影响Python计算表达式的方式

#### 整数

#### 浮点数

 - 结果包含的小数位数可能是**不确定的**
 ```python
>>> 0.2 + 0.1 
0.30000000000000004 
>>> 3 * 0.1 
0.30000000000000004
 ```
#### 除法
 - `/`结果**始终为浮点数**
 - `//`结果**始终为整数**
 - `%`余数运算 `10%3`  输出`1`

#### `str()`

 - 在字符串中使用整数时，需要显式地指出你希望Python将这个整数用作字符串
 - 将非字符串的值转换为字符串

#### Python 2中的整数

 - Python 2中，整数除法的结果只包含整数部分，*小数*部分会被**直接删除**
 - 在Python 2中，若要避免这种情况，务必确保至少有一个操作数为浮点数，这样结果也将为浮点数
 - Python 3无需如此

#### 注释
 - 单个`#`即可

## 列表list

 - 索引从0开始
 - 负数索引从-1开始，-1为最后一个
 - 用[]
 - 可以调用字符串方法等
 - 逗号后加不加空格随意
 - 将结果生成为list时需要使用

### list方法

#### `append()`
 - 只能在末尾添加元素
```python
motorcycles = []
motorcycles.append('honda') 
motorcycles.append('yamaha') 
motorcycles.append('suzuki')
print(motorcycles)
## 输出
['honda', 'yamaha', 'suzuki']
```

#### `insert()`
 - 在任意位置添加元素`insert(?,?)`
 - 添加到指定索引之**前**，后方所有元素右移一个位置
- `input()`返回的数据类型是**`str`**




```python
motorcycles = ['honda', 'yamaha', 'suzuki']
motorcycles.insert(1, 'ducati') 
print(motorcycles)
## 输出
['honda', 'ducati', 'yamaha', 'suzuki']
```

#### `del[]`
 - 删除指定**位置**的元素
 ```python
 del motorcycles[0]
 ```
 - **方**括号内为位置索引

### `pop()`
 - 无参数：弹出队尾元素（从末尾删除，并立即使用）
 - 有参数：弹出指定位置的元素（从列表中删除）
 ```Python
 first_owned = motorcycles.pop(0) 
 print('The first motorcycle I owned was a ' + first_owned.title() + '.')
 ```

### `remove()`
 - 删除对应值的元素
 - 括号内仅能为**值**
 - 仅删除**第一个**符合的元素



### `sort()`
 - 对列表进行**永久**排序
 - 默认按ASCII码升序？
 - `table.sort()`

```python
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort() print(cars)
# 输出
['audi', 'bmw', 'subaru', 'toyota']
```
 - 括号内填入参数即可适用其他排序方法
    - 逆向排序：`reverse=True`


### `sorted()`
 - **临时**排序，不改变列表实际顺序
 - `sorted(table,reverse=True)`

### `reverse()`
 - **反转**列表元素的排列顺序
 - **永久**改变列表的顺序
 - 和`sort(reserve=True)`的区别：`reserve()`只翻转列表，不会按照字母排序

### `len()`
 - 确定列表长度
 - `len(table)`
```python
>>> cars = ['bmw', 'audi', 'toyota', 'subaru'] 
>>> len(cars) 
4
```

## tuple元组

- 一旦初始化就不能修改
- 没有append()，insert()这样的方法；其他获取元素的方法和list相同
- `t=()` `t = (1,2,3)`  `t = (1,)`

- tuple无法改变，但是tuple的项目自身可以变化



## 条件判断

### `if`

- 和其他语言的区别：需要加冒号
- 注意缩进

```python
age = 20
if age >= 18:
    print('your age is', age)
    print('adult')
else:
    print('your age is', age)
    print('teenager')
```

### `elif`

- 类似于其他语言的`else if`，和`switch case `也有相似之处
- 注意缩进和冒号
- 通常最后还有`else`

```python
age = 20
if age >= 6:
    print('teenager')
elif age >= 18:
    print('adult')
else:
    print('kid')
```



## 循环

### `for`

- `for i in table`遍历list或tuple中的每个元素

- Python的for循环只有`for in `

  > 注意缩进

  ```python
  sum = 0
  for i in [1,2,3,4,5]:
      sum += i
  print(sum)
  ```

- `range()`函数：生成**整数**序列，使用`list()`函数可转换为list

  - `range(start,stop,step)` ：从`start`开始到`stop`**前**一个结束（不包括stop）

  - `range(10)`：**0**,1,2,3，...，**9**

  - `range(1,11)`：**1**,2,3，...，**10**

  - `range(0,-10,-1)`：**0**,-1,-2，...，**-9**

    ```python
    sum = 0
    for x in range(101):
        sum = sum + x
    print(sum)
    # 5050
    ```



### `while`

```python
sum = 0
x = 0
while x < 101:
    sum += x
    x += 1
print(sum)
# 5050
```



### `break`

- 提前退出循环

```python
n = 1
while n <= 100:
    if n > 10: # 当n = 11时，条件满足，执行break语句
        break # break语句会结束当前循环
    print(n)
    n = n + 1
print('END')
# 1
# 2
# ...
# 10
# END
```



### `continue`

- 跳过当前循环，直接进行下一次

```python
n = 0
while n < 10:
    n = n + 1
    if n % 2 == 0: # 如果n是偶数，执行continue语句
        continue # continue语句会直接继续下一轮循环，后续的print()语句不会执行
    print(n)

```

## `dict`和`set`

### `dict`

- 键-值（key-value）存储
- key必须是**不可变**对象，key对应的value可以改变
  - 在Python中，字符串、整数等都是不可变的
- 具有极快的查找速度，占用内存相比list多
- 格式 `d = {'a':1,'b':2}`

```python
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d['Michael']
95
```

- 放入值，后放入的会覆盖先放入的：`>>> d['Adam'] = 67`
- 判断key是否存在可以使用`in`和`get()`：
```python
>>> 'Michael' in d `
>>> False
# dict提供的get()方法，如果key不存在，可以返回None(终端不显示结果），或自己指定的value
>>> d.get('Thomas')
>>> d.get('Thomas', -1)
-1
```

- 删除`dict`的数据：`pop(key)`，同时会返回`pop`出来的值

```python
>>> d.pop('Bob')
75
>>> d
{'Michael': 95, 'Tracy': 85}
```

### `set`

- 只有key，没有value

- 由于key的特性，`set`中没有重复的元素

- 不能放入可变对象

```python
>>> s.add(l)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: unhashable type: 'list'
```

- 若输入重复元素，将会被自动去重

- 格式`s = set([1,2,3,4])`或`s={1,2,4,3}`

```python
>>> s = set([1, 1, 2, 2, 3, 3])
>>> s
{1, 2, 3}
```

- 向set中添加元素：`s.add(key)`，移除元素：`s.remove(key)`


# 函数

## 定义函数

```python
def function(x):
    if x  0:
        return x;
    else:
        return -x
```

- `def`
- 在Python命令行时，需要注意缩进
- 打包作为py文件运行时，需要添加头

## 导入函数

从`script.py`导入`function()`函数：`from script import function`

## `pass`

- 可以编写空函数占位

- 用在其他语句中，让代码能够继续运行下去

```python
if age >= 18:
    pass
```

## `raise`

- 引发异常
- 引发异常后，`raise`后面的语句将无法执行
- 使用`try...except`等语句可以进行异常调试





## 函数参数

### 位置参数
- 按照传入值的顺序赋予给参数（变量）

- `def function(x,y)`

### 默认参数
- 不填写参数时默认传入的值

-  `def function(x,y=1,z='2')`
- 必选参数在前，默认参数在后，否则Python的解释器会报错
   - 有多个参数时，把变化多的参数放前面，变化少的参数放后面。变化小的参数就可以作为默认参数
   - 不按顺序提供部分默认参数时，需要把参数名写上

### 可变参数
- 参数接收到的转为**tuple**，可以传入任意个参数，包括**0**个

- 已有list或者tuple的情况下，可以直接变换后传入

  ```python
  def function(*x)
  >> function()
  >> function(1,2)
  
  >>> nums = [1, 2, 3]
  >>> calc(*nums)
  ```

### 关键字参数
- 必须传入要求的参数

- 类似可变参数，传入后转为**dict**

- `def function(x,y=1,**z)`

- 将dict直接传入的情况

  ```python
  >>> extra = {'city': 'Beijing', 'job': 'Engineer'}
  >>> person('Jack', 24, **extra)
  name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
  ```

  

### 命名关键字参数
- 必须传入要求的参数**名**

- 只接收特定关键字参数

- 需要一个特殊分隔符`*`，`*`**后面**的参数被视为命名关键字参数

- 可变参数后面的参数都为命名关键字参数，无需添加`*` 

- 可以拥有默认值，有默认值的情况下，该项无需提供参数名

  ```python
  def person(name, age, *, city='Beijing', job):
  >>> person('Jack', 24, job='Engineer')
  Jack 24 Beijing Engineer
  ```

## 递归函数

- python递归调用次数上限：1000

- 普通递归调用：

  ```python
  1 def recursion(n):
  2     if n==1:
  3         return n
  4     else:
  5         return n+recursion(n-1)
  
  # recursion(5)
  # 5+recursion(4)
  # 5+(4+recursion(3))
  # 5+(4+(3+recursion(2)))
  # 5+(4+(3+(2+recursion(1))))
  # 5+(4+(3+(2+1)))
  # 15
  ```

- 尾递归实现：

  ```python
  1 def tail_recursion(n,total=0):
  2     if n==0:
  3         return total
  4     else:
  5         return tail_recursion(n-1,  total+n)  
  
  # recursion(5)
  # 5+recursion(4)
  # 5+(4+recursion(3))
  # 5+(4+(3+recursion(2)))
  # 5+(4+(3+(2+recursion(1))))
  # 5+(4+(3+(2+1)))
  # 15
  ```

- 两种情况下，两个函数递归调用次数均不能超过1000，执行参数n=999即报错



# 高级特性

## 切片

L = [1,A,B,2,1,3,4]

- L[0:2]：`[1,A]`，从索引0开始取数值，到索引2前（即1）停止。也可写作`L[:2]`
- L[-3:-1]：`[1,3]`

- L[-3:]：`[1,3,4]`最后三个数字。似乎只有这种写法能包括最后一个元素

- L[2::2]：`[B,1,4]`从索引2开始，每两个取一个

- L[:]：原list

- 注意：切片顺序始终为**正向**

- **tuple和字符串**也适用切片操作

  - ```python
    >>> (0, 1, 2, 3, 4, 5)[:3]
    (0, 1, 2)
    ```

  - ```python
    >>> 'ABCDEFG'[:3]
    'ABC'
    >>> 'ABCDEFG'[::2]
    'ACEG'
    ```

## 迭代

- Python通过`for in `完成迭代操作
- 