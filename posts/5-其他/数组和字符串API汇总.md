# 前言

相信不少前端程序猿都有相同的感受，JS 数组跟字符串的 API 太多了，好不容易记下，用的时候都忘了。

本文尝试着帮大家梳理这些API。

<br/>

# 转换

数组跟字符串是可以相互转换的，记住他们之间的桥梁，也就是两个API：

- split 字符串转数组
- join  数组转字符串

<br/>

# 数组API汇总

数组API可以分为两类，一类会更改原数组，一类不会更改原数组。

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/172.png' width='500'>
<br/>

再往下细分，我们可以看到数组API的全貌了~

- 更改原数组
    - 添加
        - push()：末尾添加
        - unshift()：开始位置添加
    - 删除
        - pop()：末尾移除
        - shift()：开始位置移除
    - 排序
        - reverse()：反转
        - sort()：排序
    - 覆盖
        - copyWithin(target,start,end) 从数组的指定位置拷贝元素到数组的另一个指定位置中
    - 连接
        - concat()
    - 转换
        - join() 将数组转成字符串
    - 填充
        - ✨fill(value, start, end) 用一个固定值填充一个数组中从起始索引到终止索引内的全部元素。不包括终止索引。
- 不更改原数组
    - 截取
        - slice(起始位置，结束位置)
        - splice(起始位置，要删除的数目，要插入的任意数量的项目)
    - 寻找
        - indexOf()
        - lastIndexOf()
        - ✨ includes() 返回布尔值
        - ✨ find() 返回第一个符合数组条件的成员
        - ✨ findIndex() 返回第一个符合数组条件的成员在数组中的位置
    - 迭代
        - every() 对数组中的每一项运行指定函数，如果该函数对每一项都返回true，则返回true
        - some() 对数组中的每一项运行指定函数，如果该函数对任意一项都返回true，则返回true
        - filter() 对数组中的每一项运行指定函数，将结果为true的项组成新数组，并返回该新数组
        - forEach() 对数组中的每一项运行指定函数
        - map() 对数组中的每一项运行指定函数，返回每次调用的结果组成的数组
    - 归并
        - reduce(callback(Accumulator, CurrentValue, CurrentIndex, SourceArray ), initValue)

最后，上个思维导图，可以长按保存~

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/173.png' width='1000'>
<br/>

# 字符串API

字符串API少得多，直接上~

- 字符串操作
    - 截取（返回子字符串，原字符串不会被修改）
        - substring(start, end)
        - slice(start, end)
        - substr(start, 截取长度)
    - 连接
        - concat()
    - 重复
        - ✨ repeat()
    - 字符串位置
        - indexOf(要搜索的子字符串，开始搜索的位置[可选])
        - lastIndexOf(要搜索的子字符串，开始搜索的位置[可选])
        - ✨includes() 返回布尔值，表示是否找到
        - ✨startWith() 返回布尔值，表示参数字符串是否在原字符串头部
        - ✨endsWith() 返回布尔值，表示参数字符串是否在原字符串尾部
    - 字符串大小写转换
        - toLowerCase()
        - toLocaleLowerCase()
        - toUpperCase()
        - toLocaleUpperCase()
    - 字符串模式匹配
        - match(正则) 返回符合正则筛选的数组
        - search(正则) 返回第一个匹配项的索引
        - replace(正则，字符串/函数) 返回替换后的字符串
        - split(分隔符，数组长度)
    - 其他
        - localeCompare 比较两个字符串
        - fromCharCode() 将字符串编码转成字符串

最后，同样上个思维导图，可以长按保存~

<br/>
<img src='https://github.com/jiangxia/FE-Knowledge/raw/master/images/174.png' width='1000'>
<br/>

# 写在最后

平时用这些API时，多联系相同类型的API，能增强记忆。

将常用的API记熟，对日常工作意义重大，这点投入是值得的！