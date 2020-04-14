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

```
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

```
>>> favorite_language = 
'python '
>>> favorite_language 
'python '
>>> favorite_language.rstrip() 
'python'
>>> favorite_language
'python '
```
```
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

 - `lstrip()`删除左侧
 - `strip()`删除两侧

#### Python2中的`print`
 - 可以不加括号

### 数字
 
 > 空格不影响Python计算表达式的方式

#### 整数

#### 浮点数

 - 结果包含的小数位数可能是**不确定的**
 ```
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

## 列表

 - 索引从0开始
 - 负数索引从-1开始，-1为最后一个
 - 用[]
 - 可以调用字符串方法等
 - 逗号后加不加空格随意

### 列表编辑

#### `append()`
 - 在末尾添加元素
```
motorcycles = []
motorcycles.append('honda') 
motorcycles.append('yamaha') 
motorcycles.append('suzuki')
print(motorcycles)
## 输出
['honda', 'yamaha', 'suzuki']
```

#### `insert()`
 - 在任意位置添加元素`insert(?,?)
 - 添加到指定位置之前，后方所有元素右移一个位置
```
motorcycles = ['honda', 'yamaha', 'suzuki']
motorcycles.insert(1, 'ducati') 
print(motorcycles)
## 输出
['honda', 'ducati', 'yamaha', 'suzuki']
```

#### `del[]`
 - 删除指定**位置**的元素
 ```
 del motorcycles[0]
 ```
 - **方**括号内为位置索引

### `pop()`
 - 无参数：弹出队尾元素（从末尾删除，并立即使用）
 - 有参数：弹出指定位置的元素（从列表中删除）
 ```
 first_owned = motorcycles.pop(0) 
 print('The first motorcycle I owned was a ' + first_owned.title() + '.')
 ```

### `remove()`
 - 删除对应值的元素
 - 括号内仅能为**值**
 - 仅删除**第一个**符合的元素


## 组织列表
### `sort()`
 - 对列表进行**永久**排序
 - 默认按ASCII码升序？
 - `table.sort()`

```
cars = ['bmw', 'audi', 'toyota', 'subaru']
cars.sort() print(cars)
# 输出
['audi', 'bmw', 'subaru', 'toyota']
```
 - 括号内填入参数即可适用其他排序方法
    - 反向排序：`reverse=True`


### `sorted()`
 - 不改变列表实际顺序
 - `sorted(table,reverse=True)`

### `reverse()`
 - **反转**列表元素的排列顺序
 - **永久**改变列表的顺序

### `len()`
 - 确定列表长度
 - `len(table)`
```
>>> cars = ['bmw', 'audi', 'toyota', 'subaru'] 
>>> len(cars) 
4
```

