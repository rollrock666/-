by tsm
----------
# 变量、运算符与数据类型
1. 注释

    单行注释：#
    
    多行注释：''' '''

2. 运算符

    算术运算符 
    ```
    print(1 + 1)  # 2
    print(2 - 1)  # 1
    print(3 * 4)  # 12
    print(3 / 4)  # 0.75
    print(3 // 4)  # 0
    print(3 % 4)  # 3
    print(2 ** 3)  # 8
    ```
    比较运算符
    ```
    print(1 + 1)  # 2
    print(2 - 1)  # 1
    print(3 * 4)  # 12
    print(3 / 4)  # 0.75
    print(3 // 4)  # 0
    print(3 % 4)  # 3
    print(2 ** 3)  # 8
    ```
    逻辑运算符
    ```
    print((3 > 2) and (3 < 5))  # True
    print((1 > 3) or (9 < 2))  # False
    print(not (2 > 1))  # False
    ```
    位运算符
    ```
    print(bin(4))  # 0b100
    print(bin(5))  # 0b101
    print(bin(~4), ~4)  # -0b101 -5
    print(bin(4 & 5), 4 & 5)  # 0b100 4
    print(bin(4 | 5), 4 | 5)  # 0b101 5
    print(bin(4 ^ 5), 4 ^ 5)  # 0b1 1
    print(bin(4 << 2), 4 << 2)  # 0b10000 16
    print(bin(4 >> 2), 4 >> 2)  # 0b1 1
    ```
    三元运算符
    ```
    x, y = 4, 5
    small = x if x < y else y
    print(small)  # 4
    ```
    其他运算符
    ```
    letters = ['A', 'B', 'C']
    if 'A' in letters:
    print('A' + ' exists')
    if 'h' not in letters:
    print('h' + ' not exists')
    # A exists
    # h not exists
    ```
3. 变量和赋值

- 在使用变量之前，需要对其先赋值。
- 变量名可以包括字母、数字、下划线、但变量名不能以数字开头。
- Python 变量名是大小写敏感的，foo != Foo。

4. 数据类型与转换
- 整型（int）
- 浮点型（float）
- 布尔型（bool）

5. print() 函数
```
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

- 将对象以字符串表示的方式格式化输出到流文件对象file里。其中所有非关键字参数都按str()方式进行转换为字符串输出；
- 关键字参数sep是实现分隔符，比如多个参数输出时想要输出中间的分隔字符；
- 关键字参数end是输出结束时的字符，默认是换行符\n；
- 关键字参数file是定义流输出的文件，可以是标准的系统输出sys.stdout，也可以重定义为别的文件；
- 关键字参数flush是立即把内容输出到流文件，不作缓存。

# 位运算
1. 原码、反码和补码
- 正数原码=反码=补码
- 负数反码=原码0和1反置，补码=反码+1
2. 按位运算

- 按位非操作 ~ 

    ~ 1 = 0
    
    ~ 0 = 1

    ~ 把num的补码中的 0 和 1 全部取反（0 变为 1，1 变为 0）有符号整数的符号位在 ~ 运算中同样会取反。

    00 00 01 01 -> 5
   
    ~11 11 10 10 -> -6

    11 11 10 11 -> -5
    
    ~00 00 01 00 -> 4
- 按位与操作 &

    1 & 1 = 1
   
    1 & 0 = 0
   
    0 & 1 = 0
   
    0 & 0 = 0
- 按位或操作 |

    1 | 1 = 1
    
    1 | 0 = 1
    
    0 | 1 = 1
    
    0 | 0 = 0
- 按位异或操作 ^

    1 ^ 1 = 0
    
    1 ^ 0 = 1
    
    0 ^ 1 = 1
    
    0 ^ 0 = 0

- 按位左移操作 <<

    num << i 将num的二进制表示向左移动i位所得的值。

    00 00 10 11 -> 11

    11 << 3

    01 01 10 00 -> 88 

- 按位右移操作 >>

    num >> i 将num的二进制表示向右移动i位所得的值。

    00 00 10 11 -> 11

    11 >> 2

    00 00 00 10 -> 2 

3. 利用位运算实现快速计算
- 通过 <<，>> 快速计算2的倍数问题。

    n << 1 -> 计算 n*2
    
    n >> 1 -> 计算 n/2，负奇数的运算不可用
    
    n << m -> 计算 n*(2^m)，即乘以 2 的 m 次方
    
    n >> m -> 计算 n/(2^m)，即除以 2 的 m 次方
    
    1 << n -> 2^n 
- 通过 ^ 快速交换两个整数。 通过 ^ 快速交换两个整数。

    a ^= b
    
    b ^= a
    
    a ^= b
- 通过 a & (-a) 快速获取a的最后为 1 位置的整数。

    00 00 01 01 -> 5
    &
    11 11 10 11 -> -5

    00 00 00 01 -> 1

    00 00 11 10 -> 14
    &
    11 11 00 10 -> -14

    00 00 00 10 -> 2

4. 利用位运算实现整数集合
    
    一个数的二进制表示可以看作是一个集合（0 表示不在集合中，1 表示在集合中）。

    比如集合 {1, 3, 4, 8}，可以表示成 01 00 01 10 10 而对应的位运算也就可以看作是对集合进行的操作。

    元素与集合的操作：

    a | (1<<i)  -> 把 i 插入到集合中
    
    a & ~(1<<i) -> 把 i 从集合中删除
    
    a & (1<<i)  -> 判断 i 是否属于该集合（零不属于，非零属于）

    集合之间的操作：

    a 补   -> ~a
    
    a 交 b -> a & b
    
    a 并 b -> a | b
    
    a 差 b -> a & (~b)

    注意：整数在内存中是以补码的形式存在的，输出自然也是按照补码输出。
# 条件语句
1. if
    ```
   if expression:
    expr_true_suite
    ```
2. if-else
    ```
    if expression:
    expr_true_suite
    else:
    expr_false_suite
    ```
3. if-elif-else
    ```
    if expression1:
    expr1_true_suite
    elif 
    expression2:
    expr2_true_suite
    elif
    expressionN:
    exprN_true_suite
    else:
    expr_false_suite
    ```
4. assert
   
    assert这个关键词我们称之为“断言”，当这个关键词后边的条件为 False 时，程序自动崩溃并抛出AssertionError的异常。
    ```
    my_list = ['lsgogroup']
    my_list.pop(0)
    assert len(my_list) > 0

    # AssertionError
    ```
# 循环语句
1. while
   ```
    while 布尔表达式:
    代码块
   ```
2. while-else
   
   当while循环正常执行完的情况下，执行else输出，如果while循环中执行了跳出循环的语句，比如 break，将不执行else代码块的内容。 
   ```
    while 布尔表达式:
    代码块
    else:
    代码块
   ```
3. for
   ```
    for i in 'ILoveLSGO':
    print(i, end=' ')  # 不换行输出
   ```
4. for-else
   ```
    for 迭代变量 in 可迭代对象:
    代码块
    else:
    代码块
   ```
5. range
   ```
    range([start,] stop[, step=1])
   ```
6. enumerate
   ```
    enumerate(sequence, [start=0])
   ```
7. break
  
   跳出当前循环
8. continue
   
   跳过当前循环
9.  pass

    留空
10. 推导式
- 列表推导式

    [ expr for value in collection [if condition] ]
- 元组推导式
  
  ( expr for value in collection [if condition] )
- 字典推导式

    { key_expr: value_expr for value in collection [if condition] }
- 集合推导式

    { expr for value in collection [if condition] }

# 异常处理
1. Python 标准异常总结

    BaseException：所有异常的 基类Exception：常规异常的 基类
    
    StandardError：所有的内建标准异常的基类
    
    ArithmeticError：所有数值计算异常的基类
    
    FloatingPointError：浮点计算异常
    
    OverflowError：数值运算超出最大限制
    
    ZeroDivisionError：除数为零
    
    AssertionError：断言语句（assert）失败
    
    AttributeError：尝试访问未知的对象属性
    
    EOFError：没有内建输入，到达EOF标记
    
    EnvironmentError：操作系统异常的基类
    
    
    IOError：输入/输出操作失败
    
    OSError：操作系统产生的异常（例如打开一个不
    存在的文件）
    
    WindowsError：系统调用失败
    
    ImportError：导入模块失败的时候
    
    KeyboardInterrupt：用户中断执行
    
    LookupError：无效数据查询的基类
    
    IndexError：索引超出序列的范围
    
    KeyError：字典中查找一个不存在的关键字
    
    MemoryError：内存溢出（可通过删除对象释放内存）
    
    NameError：尝试访问一个不存在的变量
    
    UnboundLocalError：访问未初始化的本地变量
    
    ReferenceError：弱引用试图访问已经垃圾回收了的对象
    
    RuntimeError：一般的运行时异常
    
    NotImplementedError：尚未实现的方法
    
    SyntaxError：语法错误导致的异常
    
    IndentationError：缩进错误导致的异常
    
    TabError：Tab和空格混用
    
    SystemError：一般的解释器系统异常
    
    TypeError：不同类型间的无效操作
    
    ValueError：传入无效的参数
    
    UnicodeError：Unicode相关的异常
    
    UnicodeDecodeError：Unicode解码时的异常
    
    UnicodeEncodeError：Unicode编码错误导致的异常
    
    UnicodeTranslateError：Unicode转换错误导致的异常

2. Python标准警告总结

    Warning：警告的基类
    
    DeprecationWarning：关于被弃用的特征的警告
    
    FutureWarning：关于构造将来语义会有改变的警告
    
    UserWarning：用户代码生成的警告
    
    PendingDeprecationWarning：关于特性将会被
    废弃的警告
    
    RuntimeWarning：可疑的运行时行为(runtime 
    behavior)的警告
    
    SyntaxWarning：可疑语法的警告
    
    ImportWarning：用于在导入模块过程中触发的警告
    
    UnicodeWarning：与Unicode相关的警告
    
    BytesWarning：与字节或字节码相关的警告
    
    ResourceWarning：与资源使用相关的警告

3. try - except 语句
    ```
    try:
        检测范围
    except Exception[as reason]:
        出现异常后的处理代码
    ```

4. try - except - finally 语句

    try: 检测范围 except Exception[as reason]: 出现异常后的处理代码 finally: 无论如何都会被执行的代码

    不管try子句里面有没有发生异常，finally子句都会执行。

    【例子】如果一个异常在try子句里被抛出，而又没有任何的except把它截住，那么这个异常会在finally子句执行后被抛出。


5. try - except - else 语句

    如果在try子句执行时没有发生异常，Python将执行else语句后的语句。
    ```
    try:
        检测范围
    except:
        出现异常后的处理代码
    else:
        如果没有异常执行这块代码
    ```
    使用except而不带任何异常类型，这不是一个很好的方式，我们不能通过该程序识别出具体的异常信息，因为它捕获所有的异常。

    try: 检测范围 except(Exception1[, Exception2[,...ExceptionN]]]): 发生以上多个异常中的一个，执行这块代码 else: 如果没有异常执行这块代码

6. raise
   
   使用raise语句抛出一个指定的异常。
   ```
   try:
    raise NameError('HiThere')
    except NameError:
    print('An exception flew by!')
   ```
