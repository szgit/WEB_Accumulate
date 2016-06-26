# 入门

参考链接<http://deerchao.net/tutorials/regex/regex.htm>


##1. 元字符

| 元字符 | 说明                         |
|--------|------------------------------|
| .      | 匹配除换行符意外的任意字符   |
| \w     | 匹配字母或数组或下划线或汉字 |
| \s     | 匹配任意的空白符             |
| \d     | 匹配数字                     |
| \b     | 匹配单词的开始或结束         |
| ^      | 匹配字符串的开始             |
| $      | 匹配字符串的介绍             |


##2.限定符

| 限定符 | 说明       |
|--------|------------|
| *      | 重复0~n次  |
| +      | 重复1~n次  |
| ?      | 重复0~1次  |
| {n}    | 重复n次    |
| {n,}   | 重复n~多次 |
| {n,m}  | 重复n~m次  |

##3. 字符类[]

匹配单个字符

##4. 分支 |

不同的匹配条件

##5. 分组()

一组匹配条件.

```javascript
//匹配IP
((2[0-4]\d|25[0-5]|[01]?\d\d?)\.){3}(2[0-4]\d|25[0-5]|[01]?\d\d?)
```

##6. 反义

| 反义     | 说明                                    |
|----------|-----------------------------------------|
| \\W      | 匹配任意不是字母,数字,下划线,汉字的字符 |
| \S       | 匹配任意不是空白符的字符                |
| \D       | 匹配任意非数字的字符                    |
| \[^aeiou] | 匹配除了aeiou以外的任意字符             |

##7. 后向引用

匹配重复单词

```javascript
\b(w+)\b\s+\1\b //\1带便分组1的引用.即(w+)
```

自定义组名`(?<Word\w+>)`. or `(?'Word'\w+)`

反向引用这个分组

```javascript
\b(?<Word>\w+)\b\s+\k<Word>\b
```

| 分类     | 语法         | 说明                                                        |
|----------|--------------|-------------------------------------------------------------|
| 捕获     | (exp)        | 匹配exp,并捕获文本到自动命名的组里                          |
| 捕获     | (?<name>exp) | 匹配exp,并捕获文本到名称为name的组里,也可以写成(?'name'exp) |
| 捕获     | (?:exp)      | 匹配exp,不捕获匹配的文本,也不给此分组分配组号               |
| 零宽断言 | (?=exp)      | 匹配exp前面的位置                                           |
| 零宽断言 | (?<=exp)     | 匹配exp后面的位置                                           |
| 零宽断言 | (?!exp)      | 匹配后面跟的不是exp的位置                                   |
| 零宽断言 | (?<!exp)     | 匹配前面不是exp的位置                                       |
| 注释     | (?#comment)  | 注释,不会有任何影响                                         |

分组0对应整个正则表达式

组号分配过程 : 

1. 扫描第一遍,给未命名组分配
2. 扫描第二遍,给命名组分配
3. 命名组号>未命名组号
4. 可以哦那个(?:exp)剥夺一个分组对组号分配的参与权.

保证`<a></a>`等对应闭合的HTML标签

```javascript
(?<=<(\w+)>).*(?=<\/\1>)
```
##8. 贪婪与懒惰

| 语法   | 说明                       |
|--------|----------------------------|
| *?     | 重复任意次,尽可能少重复    |
| +?     | 重复1次或多次,尽可能少重复 |
| ??     | 重复0~1此,尽可能少重复     |
| {n,}?  | 重复n次及其以上,但尽可能少重复 |
| {n,m}? | 重复n~m次,尽可能少重复     |