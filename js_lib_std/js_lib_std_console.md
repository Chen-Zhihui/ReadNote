
namespace console

logging: 
assert(condition, ...data), 
clear(), 
debug|error|info|log|trace|warn(...data)
dir(item, options), dirxml(...data)

counting:
count(label),countReset(label)

group
group(...data), groupCollapsed(...data), groupEnd()

timing
time(label), timeLog(label, ...data), timeEnd(label)


Logger(logLevel, args)
Formatter(args)
Printer(logLevel, args[, options])

# reference
[Standard](https://console.spec.whatwg.org/)

# UC

## 在日志中使用表达式(console.log(`${expr}`))

```js
const regex1 = RegExp('foo*', 'g');
const str1 = 'table football, foosball';
let array1;

while ((array1 = regex1.exec(str1)) !== null) {
  console.log(`Found ${array1[0]}. Next starts at ${regex1.lastIndex}, value=${str1[regex1.lastIndex]}.`);
  // expected output: "Found foo. Next starts at 9, value=t."
  // expected output: "Found foo. Next starts at 19, value=s."
}
```