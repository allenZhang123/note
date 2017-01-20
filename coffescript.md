#CoffeeScript学习
##常用命令	
- -c, --compile	编译一个 .coffee 脚本到一个同名的 .js 文件.
- -m, --map	随 JavaScript 文件一起生成 source maps. 并且在 JavaScript 里加上 sourceMappingURL 指令.
- -i, --interactive	启动一个交互式的 CoffeeScript 会话用来尝试一些代码片段. 等同于执行 coffee 而不加参数.
- o, --output [DIR]	将所有编译后的 JavaScript 文件写到指定文件夹. 与 --compile 或 --watch 搭配使用.
- -j, --join [FILE]	编译之前, 按参数传入顺序连接所有脚本到一起, 编译后写到指定的文件. 对于编译大型项目有用.
- -w, --watch	监视文件改变, 任何文件更新时重新执行命令.
- -p, --print	JavaScript 直接打印到 stdout 而不是写到一个文件.
- -s, --stdio	将 CoffeeScript 传递到 STDIN 后从 STDOUT 获取 JavaScript. 对其他语言写的进程有好处. 比如:
cat src/cake.coffee | coffee -sc
- -l, --literate	将代码作为 Literate CoffeeScript 解析. 只会在从 stdio 直接传入代码或者处理某些没有后缀的文件名需要写明这点.
- -e, --eval	直接从命令行编译和打印一小段 CoffeeScript. 比如:
coffee -e "console.log num for num in [10..1]"
- -b, --bare	编译到 JavaScript 时去掉顶层函数的包裹.
- -t, --tokens	不对 CoffeeScript 进行解析, 仅仅进行 lex, 打印出 token stream: [IDENTIFIER square] [ASSIGN =] [PARAM_START (] ...
- -n, --nodes	不对 CoffeeScript 进行编译, 仅仅 lex 和解析, 打印 parse tree:
Expressions
  Assign
    Value "square"
    Code "x"
      Op *
        Value "x"
        Value "x"
- --nodejs	node 命令有一些实用的参数, 比如
--debug, --debug-brk, --max-stack-size, 和 --expose-gc. 用这个参数直接把参数转发到 Node.js. 重复使用 --nodejs 来传递多个参数.

##编译器
demo.coffee

```
for i in [0..5]
	console.log "hello #(i)"
```

运行

```
$ coffee demo.coffee
Hello 0
Hello 1
Hello 2
Hello 3
Hello 4
Hello 5
```
编译 

`$ coffee -c demo.coffee`

- 编译一个 .coffee 文件的树形目录 src 到一个同级  .js 文件树形目录 lib:
`coffee -c -o lib/ src/`

- 监视一个文件的改变, 每次文件被保证时重新编译:

`coffee --w -o lib/ demo.coffee`

- 监视和重复编译整个项目:
coffee -o lib/ -cw src/

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

##运行coffee文件

###直接运行文件

**demo.coffee**

`console.log "hello coffeesccript"`

**命令行**

```
coffee demo.coffee
hello coffeesccript
```

###node中运行

**index.js**

```
require('coffee-script');
var hello = require('./demo.coffee');
```
**命令行**

`node index.js`

###浏览器运行

##coffee-script语法

###操作符和aliase

####列表

| CoffeeScript	| JavaScript| 
| -----------|:----------:| 
| is	|  === | 
| isnt	| !==| 
|  not	|  	!	|  
| and	| &&| 
| or	| 双竖线 | 
| true, yes, on	| true| 
| false, no, off	| false| 
| @, this	| this| 
| of| 	in| 
| in	| no JS equivalent| 
| a ** b	| Math.pow(a, b)| 
| a // b	| Math.floor(a / b)| 
| a %% b	| (a % b + b) % b| 

#### ? 存在性操作符
.coffee

```
solipsism = true if mind? and not world?

speed = 0
speed ?= 15

footprints = yeti ? "bear"
```
.js

```
var footprints, solipsism, speed;

if ((typeof mind !== "undefined" && mind !== null) && (typeof world === "undefined" || world === null)) {
  solipsism = true;
}

speed = 0;

if (speed == null) {
  speed = 15;
}

footprints = typeof yeti !== "undefined" && yeti !== null ? yeti : "bear";
```
#### ?. 吸收null和undefined

.coffee

```
zip = lottery.drawWinner?().address?.zipcode
```
.js

```

var zip, _ref;

zip = typeof lottery.drawWinner === "function" ? (_ref = lottery.drawWinner().address) != null ? _ref.zipcode : void 0 : void 0;
```

###对象和数组

```
#带逗号
arr1 = ["do", "re", "mi", "f"]
#不带标点
arr2 = [
	"do"
	"re"
	"mi"
	"fa"
]
obj1 = { 1:"hehe", 2:"haha" }
obj2 =
	first:
		firstOne:"one"
		firstTwo:"two"
	second:
		age:'13'
		name:'leo'
```
####数组切片

```
#数组切片和利用range进行拼接
#通过两个点号的写法 (3..6), 
#range 会包含最后一个数据 (3, 4, 5, 6); 
#通过三个点号的写法 (3...6), range 不会包含最后一个数据 (3, 4, 5).
#切片的索引位置存在不错的默认值. 前面的索引位置省略的话, 默认会是 0, 
#后面的索引位置被省略的话, 默认值是数组的大小.


number = [1, 2, 3, 4, 5, 6, 7, 8, 9]
start = number[0..2]
middle = number[3...-2]
end = number[-2..]
copy = number[..]
```

```
number = [1, 2, 3, 4, 5, 6, 7, 8, 9];

start = number.slice(0, 3);

middle = number.slice(3, -2);

end = number.slice(-2);

copy = number.slice(0);
```

####切片与循环

```
#返回数组 自执行函数包裹
globals = for name of window
	"属性名称 #{name}"

#不加括号 只返回一个值，不会有自执行函数
globalsTwo = name for name of window
#加括号 返回数组 自执行函数包裹
globalsTwo = (name for name of window)
#与切片结合
globalsTwo = (name for name of window)[0..3]
```

###函数

```
console.log "hello coffeesccript"
#单箭头函数
fn = (a,b) -> a + b

#为形参设置默认值
fill = (container, liquid = "coffee") ->
	"Fill the #{container} with  #{liquid}"
```

####函数绑定

```
# 函数绑定  function binding 
# fat arrow 双箭头函数
# 单箭头函数this与普通函数相同
# 双箭头函数this指向定义函数时this的对象
Account = (customer, cart) ->
	@customer = customer
	@cart = cart

	$('.shopping_cart').bind 'click', (event) =>
		@customer.purchase @cart
```

###变量

变量不需要写var 
全局变量

`globalVar = exports ? thi`

###变参 splats

```
gold = silver = rest = 'unknown'

awardsMedals = (one, two, others...) ->
	gold = one
	silver = two
	rest = others

contenders = [
	"Michael Phelps"
	"Liu Xiang"
	"Yao Ming"
	"Allyson Felix"
	"Shawn Johnson"
	"Roman Sebrle"
	"Guo Jingjing"
	"Tyson Gay"
	"Asafa Powell"
	"Usain Bolt"
]
#不定参 
awardsMedals contenders...

console.log "Gold #{gold}"
console.log "Silver #{silver}"
console.log "The Field #{rest}"
```

###if else unless

```
if happy and knowsIt
	clapsHands()
	chaCha()
else
	showIt()
```
####条件赋值

```
mod = greatlyImproved if singing

data = if friday then sue else jill
```

###Switch/When/Else

```
switch day
	when 'mon' then go work 
	when 'tue' then go relax
	when 'fri','sat'
		if day is bingoDay
			go bingo
	else go work 
```
####条件赋值

```
score = 76
grade = switch
	when score < 60 then 'D'
	when score < 70 then 'C'
	when score < 80 then 'B'
	else 'A'

```

###循环和推导式

#### for in 迭代数组

```
eat food for food in [ 'toast', 'cheese', 'wine']

courses = ['greens', 'caviar', 'truffles', 'roast', 'cake']
#dish, i in courses  dish：值  i：键
menu i + 1, dish for dish, i in courses

foods = ['broccoli', 'spinach', 'chocolate']
# if 条件语句用when
eat food for food in foods when food isnt 'chocolate'

#不带括号给countdown赋值10次
countdown = num for num in [10..1] when num isnt 3

#带括号自执行函数返回数组 countdown是数组
countdown = (num for num in [10..1] when num isnt 3)

#迭代范围
evens = (x for x in [0..10] by 2)
```

#### for of 迭代对象

```
#迭代对象 of用于去对象中的属性
yearOld = {
	max:10
	ida:9
	tim:11
}
# child：键  age：值
ages= for child, age of yearOld
	"#{child} is #{age}"

#遍历对象自定义属性，避免集成属性
property = for own key, value of object
	"#{child} is #{age}"
```

####while循环

```
#while循环 循环条件或者赋值返回数组 
#until : while not   loop : while true
if this.studyEconomics
	buy() while supply > demand
	sell() until supply > demand

num = 6
lyrics = while num -= 1
	"#{num} little monkeys, jumping on the bed.
    One fell out and bumped his head."
```

#### do关键字

```
#循环do关键字 将定义的函数执行
for num in [10..0]
	countTime num

for filename in list
	do (filename) -> 
		fs.readFile filename,(err,contents) -> 
			compile filename,contents.toString()
```

###class 继承 super

```
class Animal 
	constructor:(@name) ->

	meve:(meters) ->
		console.log @name+ "moved #{meters}m"

class Snake extends Animal
	move: ->
		console.log "Slithering"
		#参数
		super 5
		
sam = new Snake "Sammy"

sam.move()
```
###解构赋值

```
theBait = 1000
theSwitch = 0

[ theBait, theSwitch ] = [ theSwitch, theBait ] 
```
####处理函数多返回值

```
weatherReport = (location) ->
	[location,72,'sunny']
# 按照数组索引进行匹配
[city, temp , forecast]= weatherReport "CA"
```
####取出深度嵌套属性

```
futurists =
    sculptor: "Umberto Boccioni"
    painter:  "Vladimir Burliuk"
    poet:
    	name:   "F.T. Marinetti"
    	address: [
      	"Via Roma 42R"
      	"Bellagio, Italy 22021"
    	]

{poet:{name,address:[street,city]}} = futurists
```
####与splats搭配

```
tag = "<impossible>"
[open,contents...,close]=tag.split("")

[first,...,last]=tag.split("")
```
####构造函数的形参对象赋值到实例属性

```
class Person
	constructor:(options) -> 
		# 按照键值进行匹配
		{@name,@age,@height} = options
tim = new Person age:4
```
###插入JS代码

直接写在反引号中

```
hi = `function(){
	return 'a';
	}`
```
###Try/Catch/Finally

```
try 
	a()
catch error
	print error
finally
	b()
```
###链式对比

```
a= 2
b = 1 < a <3 
```		

###块级字符串

```
html = """
	<script>
		cup of coffeescript
	</script>
	"""
```
###块级注释

```
###
是腹黑
发发火
分开都是
###
```
