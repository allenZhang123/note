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
