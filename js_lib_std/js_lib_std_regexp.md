
# intro

```js
/pattern/flags
new RegExp(pattern [, flags])
RegExp(pattern [, flags])
```

```js
/ab+c/i;
new RegExp('ab+c', 'i');
new RegExp(/ab+c/, 'i');
```

不同于字符串，正则表达式用//做为分割符

字面量：
/pattern/flags

## flags
flags = gimuys
g, global
i, case insenstive
m, multi-line
u, unicode
y, sticky, 从正则表达式的 lastIndex 属性表示的索引处搜索
s, dotAll, include \n

## RegExp.config

RegExp.prototype.{global|ignoreCase|lastIndex|multiline|source|sticky}

当正则表达式为常量时，应使用字面量形式，提供编译形式的正则表达式


# 特殊字符
. any
\d number, [0~9]
\D not a number [^0-9]
\w [A-Za-z0-9_]
\W [^A-Za-z0-9]
\s, space, tab, etc
\S, not a space
\t tab
\r return
\n next line
\v vertical tab
[\b], backspace
\0 NULL
\cX ctrol+X
\xhh hh
\uhhhh unicode
\
[xyz]
[^xyz]
^ begin
$ end
\b word boundary
\B no word boundary

# 分组

(x)  
被匹配的子字符串可以在结果数组的元素 [1], ..., [n] 中找到，
或在被定义的 RegExp 对象的属性 $1, ..., $9 中找到

(?:x) 
匹配 x 不会捕获匹配项。这被称为非捕获括号（non-capturing parentheses）。
匹配项不能够从结果数组的元素 [1], ..., [n] 
或已被定义的 RegExp 对象的属性 $1, ..., $9 再次访问到

\n 反向引用（back reference）
/apple(,)\sorange\1/ 匹配 "apple, orange, cherry, peach." 中的 "apple,orange,"


# 量词(*, +, ?, {n,m})
x*, 0 or more
x+, 1 or more
x*? x*最小匹配
x+? x+最小匹配
x?  0 or 1
x|y x or y
x{n} =n
x{n,} >=n
x{n,m} 

# 断言
x(?=y)  仅匹配被y跟随的x
x(?!y)  仅匹配不被y跟随的x
(?<=y)x x只有在y后面才匹配
(?<!y)x x只有不在y后面才匹配

# RegExp

## property

### lastindex，只有在g模式上才有意义

## method

### re.exec(str)

### re.test(str)

# UC

## 只判断字符串是否与正则表达式吻合
``` js
let match = /^hello/.test(str);
```

## 是否进行全局查找(flag=g)

g选项使得正则表达式具有状态

```js
var regex = /foo/g;

console.log(`test result=${regex.lastIndex}`)
// regex.lastIndex is at 0
regex.test('foo'); // true

console.log(`test result=${regex.lastIndex}`)
// regex.lastIndex is now at 3
regex.test('foo'); // false
```