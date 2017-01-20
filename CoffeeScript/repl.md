##REPL

REPL (read-evaluate-print-loop, REPL) 是一个在许多编程语言中，特别是在各种函数式语言中都能找到的标准工具。REPL 就相当于 Ruby 的 IRB，只需输入 coffee 就会启动 CoffeeScript 的 REPL。

```
coffee> nums = [1..10]
[ 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 ]
coffee> isOdd = (n) -> n % 2 == 1
[Function]
coffee> odds = nums.filter isOdd
[ 1, 3, 5, 7, 9 ]
coffee> odds.reduce (a,b) -> a + b
25
```