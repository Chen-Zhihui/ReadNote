
# create

字符串对象, valueOf()
基本字符串：字面量？

```js
var s_prim = "foo";
var s_obj = new String(s_prim);

console.log(typeof s_prim); // "string"
console.log(typeof s_obj);  // "object"
console.log(typeof s_obj.valueOf()) // string
```


与eval()函数结合是应使用基本字符串，而不是字符串对象
```js
let s1 = "2 + 2";               // creates a string primitive
let s2 = new String("2 + 2");   // creates a String object
console.log(eval(s1));      // returns the number 4
console.log(eval(s2));      // returns the string "2 + 2"
```

## UC 

## long string

``` js
let longString = "This is a very long string which needs " +
                 "to wrap across multiple lines because " +
                 "otherwise my code is unreadable.";

let longString = "This is a very long string which needs \
to wrap across multiple lines because \
otherwise my code is unreadable.";
```

## 获取单个字符

```js
str[2]
str.charAt(2)
```

## compare/ignore case/