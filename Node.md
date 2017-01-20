[TOC]
#MAC快捷键
- 用键盘访问 Dock

按下 Control-Fn-F3 移动到 Dock。（如果您的键盘没有 Fn 键，请按下 Control-F3。）然后使用左箭头键和右箭头键在图标之间移动。按下 Return 以打开一个图标。

- cmd+option+松手 

当一个应用程序最小化（cmd+M）到dock后，你可以通过cmd+tab转换到那个应用程序，松开tab但不要松开cmd键，然后大指顺势从 cmd再压住option键(或者enter键)，然后松开。就可以把最小化的窗口调出。（不要看稍稍复杂了点，但这个绝对非常实用）

- cmd+shift+t  打开当前文件终端

- Shift-Command-C 打开开发者工具（浏览器为活动窗口）
					打开finder （finder为活动窗口）
          
- Shift-Command-G 前往窗口

- Control-Command-F 切换全屏
- 剪切 com+v 在目标位置 OPTION+CMD+V

- 显示系统隐藏文件

`defaults write com.apple.finder AppleShowAllFiles -boolean true ; killall Finder`

- 隐藏系统隐藏文件

`defaults write com.apple.finder AppleShowAllFiles -boolean false ; killall Finder`

- ctrl+tab 浏览器页面切换

- Command-Option-Esc 强制退出应用
- uname -a  查看系统信息
- ifconfig  查看本地域名

#项目上传服务器

##vue-webpack

- 在package.json script里面中添加

```
"ready": "cd dist && rm -rf wpb-activity2 && mkdir wpb-activity2 && cp -r ./index.html ./static ./wpb-activity2",
"upload": "cd dist && tar -czf wpb-activity2.tar.gz wpb-activity2 && scp wpb-activity2.tar.gz root@192.168.19.172:~/deploy"
```


- 运行npm run dev

- 运行npm run build

- 运行 npm run upload

- 运行 ssh root@192.168.19.172 链接服务器
- 运行  cd deploy
- 运行 tar xvzf wpb-activity2.tar.gz -C /opt/weixin/ytx3/weipan/public 将文件解压 
- 网址： http://test.ygapp.dx168.com/assets/wpb-activity2

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


#Vue.JS

##构造器

```
var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello',
    items:[
      { message:'Foo'},
      { message:'Bar'}
    ]
  },
  computed: {
    
  },
  methods:{
  	
  },
  mounted: {
  	// 创建vm.$el以后执行
  }
})
```
##实例生命周期

![实例声明周期](https://cn.vuejs.org/images/lifecycle.png)

##模板语法

###插值

- 文本 

使用 “Mustache” 语法（双大括号）

`<span>Message: {{ msg }}</span>`

- 纯HTML

`<div v-html="rawHtml"></div>`

- 属性

Mustache 不能在 HTML 属性中使用，应使用 v-bind 指令

`<div v-bind:id="dynamicId"></div>`

支持布尔值属性，当属性为false时，属性移除，为true时，属性添加

`<button v-bind:disabled="status">Button</button>`

**简写**

`<a :href="url"></a>`

- JS表达式

```
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```

###指令

[指令网址](https://cn.vuejs.org/v2/api/)

###Filters 过滤器

过滤器只能在 mustache 绑定和 v-bind 表达式（从 2.1.0 开始支持）中使用

```
<!--html模块-->

<!-- in mustaches -->
{{ message | capitalize }}

<!-- in v-bind -->
<div v-bind:id="rawId | formatId"></div>

<!--js模块-->
new Vue({
  data: {
  	rawId: 'example'
  }
  // 实例中所有过滤器的对象
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
})
```
过滤器可以串联：
`{{ message | filterA | filterB }}`

过滤器是 JavaScript 函数，因此可以接受参数：
`{{ message | filterA('arg1', arg2) }}`

这里，字符串 'arg1' 将传给过滤器作为第二个参数， arg2 表达式的值将被求值然后传给过滤器作为第三个参数。

##计算属性 computed

```
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>

var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // a computed getter
    reversedMessage: function () {
      // `this` points to the vm instance
      return this.message.split('').reverse().join('')
    }
  }
})
```

###计算属性 VS methods

```
<p>Reversed message: "{{ reverseMessage() }}"</p>

// in component
methods: {
  reverseMessage: function () {
    return this.message.split('').reverse().join('')
  }
}
```
计算属性是基于它的依赖缓存。计算属性只有在它的相关依赖发生改变时才会重新取值。这就意味着只要 message 没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数。

相比而言，每当重新渲染的时候，method 调用总会执行函数。

所以： 希望缓存采用computed，不缓存采用methods

###计算属性 vs Watched Property

watched监测

```
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
})
```
computed计算，实现同样功能

```
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```
###计算setter和getter

计算属性中默认只有getter，可以手动重置添加setter和getter，运行会自动调用

```
computed: {
  fullName: {
    // getter 调用fullName属性会自动调用
    get: function () {
      return this.firstName + ' ' + this.lastName
    },
    // setter  赋值自动调用
    set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
  }
}
```
###watch

监测数据变化

```
<div id="watch-example">
  <p>
    Ask a yes/no question:
    <input v-model="question">
  </p>
  <p>{{ answer }}</p>
</div>

<!--script-->
new Vue({
  el: '#watch-example',
  data: {
    question: '',
    answer: 'I cannot give you an answer until you ask a question!'
  },
  watch: {
    // 如果 question 发生改变，这个函数就会运行
    question: function (newQuestion) {
      this.answer = 'Waiting for you to stop typing...'
      this.getAnswer()
    }
  },
  methods: {
    getAnswer: {
    	// 处理answer的执行过程
    }
```
##class绑定

###对象语法

给 v-bind:class 一个对象，以动态地切换 class ，v-bind:class 指令可以与普通的 class 属性共存。

```
模板:
<div class="static"
	  <!--isActive为true添加active的class,为false不添加-->
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>

如下 data:
data: {
  isActive: true,
  hasError: false
}

渲染为:
<div class="static active"></div>
```
直接绑定计算属性或者对象：

```
<div v-bind:class="classObject"></div>

data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
```
###数组语法

```
<div v-bind:class="[activeClass, errorClass]">

data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}

渲染为:
<div class="active text-danger"></div>
```

条件切换：

三元表达式

`<div v-bind:class="[isActive ? activeClass : '', errorClass]">`

对象

`<div v-bind:class="[{ active: isActive }, errorClass]">`

###组件class

```
Vue.component('my-component', {
  template: '<p class="foo bar">Hi</p>'
})

然后在使用它的时候添加一些 class：
<my-component class="baz boo"></my-component>

HTML 最终将被渲染成为:
<p class="foo bar baz boo">Hi</p>

同样的适用于绑定 HTML class :
<my-component v-bind:class="{ active: isActive }"></my-component>

当 isActive 为 true 的时候，HTML 将被渲染成为:
<p class="foo bar active"></p>

```

##style绑定

###对象语法

类似css

```
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>

data: {
  activeColor: 'red',
  fontSize: 30
}
```
对象或者计算属性

```
<div v-bind:style="styleObject"></div>

data: {
  styleObject: {
    color: 'red',
    fontSize: '13px'
  }
}
```

###数组语法

v-bind:style 的数组语法可以将多个样式对象应用到一个元素上：

```
<div v-bind:style="[baseStyles, overridingStyles]">
```

##条件渲染

###v-if

```
<!--if else-->
<h1 v-if="ok">Yes</h1>
<h1 v-else-if="ok">Yes</h1>
<h1 v-else>No</h1>
```
```
<!--template切换多个元素-->
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```
**key元素**

控制元素唯一性，方式复用

`<input placeholder="Enter your username" key="username-input">`

###v-show

v-show 是简单的切换元素的 CSS 属性 display，有更高的初始渲染消耗

**注意：** v-show 不支持template语法

##列表渲染

###v-for

####基本用法

```
<!--单参数-->
<ul id="example-1">
  <li v-for="value in items">
    {{ value.message }}
  </li>
</ul>
<!--双参数-->
<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```

####template

template 标签来渲染多个元素块

```
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider"></li>
  </template>
</ul>
```

####对象迭代

```
<div v-for="(value, key) in object">
  {{ key }} : {{ value }}
</div>
```

####整数迭代

重复多次模板

```
<div>
  <span v-for="n in 10">{{ n }}</span>
</div>
```

####组件
todolist 完整版

```
<div id="todo-list-example">
  <input
    v-model="newTodoText"
    v-on:keyup.enter="addNewTodo"
    placeholder="Add a todo"
  >
  <!--使用is 制定模板-->
  <ul>
    <li
      is="todo-item"
      v-for="(todo, index) in todos"
      v-bind:title="todo"
      v-on:remove="todos.splice(index, 1)"
    ></li>
  </ul>
</div>
Vue.component('todo-item', {
  <!--模板通过$emit与组件传递数据-->
  template: '\
    <li>\
      {{ title }}\
      <button v-on:click="$emit(\'remove\')">X</button>\
    </li>\
  ',
  <!--接受父组件数据-->
  props: ['title']
})
new Vue({
  el: '#todo-list-example',
  data: {
    newTodoText: '',
    todos: [
      'Do the dishes',
      'Take out the trash',
      'Mow the lawn'
    ]
  },
  methods: {
    addNewTodo: function () {
      this.todos.push(this.newTodoText)
      this.newTodoText = ''
    }
  }
})
```

###key 

确定元素的唯一性，相当于`track-by="$index"`

```
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```
###数组更新检测

####变异方法：
可以触发试图更新
push()
pop()
shift()
unshift()
splice()
sort()
reverse()

####非变异方法：
可以触发视图更新
filter(), concat(), slice()

####注意事项

**不能引起视图更新！！**

当你利用索引直接设置一个项时，例如： vm.items[indexOfItem] = newValue

当你修改数组的长度时，例如： vm.items.length = newLength

解决方法：

```
避免第一种情况
// Vue.set
Vue.set(example1.items, indexOfItem, newValue)

// Array.prototype.splice`
example1.items.splice(indexOfItem, 1, newValue)

避免第二种情况，使用 splice：
example1.items.splice(newLength)
```
##事件监听

###v-on 绑定事件监听
监听原生DOM

```
向函数内传入$event鼠标事件对象
<button v-on:click="doThat('hello', $event)"></button>

<!-- 键修饰符，键别名 -->
<input @keyup.enter="onEnter">

<!-- 键修饰符，键代码 -->
<input @keyup.13="onEnter">
监听组件触发的自定义事件
<!-- 组件触发事件调用 -->
<my-component @my-event="handleThis(123, $event)"></my-component>
```

###事件修饰符
- .stop - 调用 event.stopPropagation()。

- .prevent - 调用 event.preventDefault()。

- .capture - 添加事件侦听器时使用 capture 模式。

- .self - 只当事件是从侦听器绑定的元素本身触发时才触发回调。

- .{keyCode | keyAlias} - 只当事件是从侦听器绑定的元素本身触发时才触发回调。

- .native - 监听组件根元素的原生事件。

- .once 事件只执行一次

```
<!-- 阻止单击事件冒泡 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联  -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件侦听器时使用事件捕获模式 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当事件在该元素本身（而不是子元素）触发时触发回调 -->
<div v-on:click.self="doThat">...</div>

<!-- the click event will be triggered at most once -->
<a v-on:click.once="doThis"></a>

```
###按键修饰符

- .enter
- .tab
- .delete (捕获 “删除” 和 “退格” 键)
- .esc
- .space
- .up
- .down
- .left
- .right
- .ctrl
- .alt
- .shift
- .meta

```
<!-- 同上 -->
<input v-on:keyup.enter="submit">

<!-- 缩写语法 -->
<input @keyup.enter="submit">
```

##表单控件

###表单修饰符

- .lazy

在默认情况下， v-model 在 input 事件中同步输入框的值与数据 (除了 上述 IME 部分)，但你可以添加一个修饰符 lazy ，从而转变为在 change 事件中同步：

```
<!-- 在 "change" 而不是 "input" 事件中更新 -->
<input v-model.lazy="msg" >
```
- .number

如果想自动将用户的输入值转为 Number 类型（如果原值的转换结果为 NaN 则返回原值），可以添加一个修饰符 number 给 v-model 来处理输入值：

```
<input v-model.number="age" type="number">
这通常很有用，因为在 type="number" 时 HTML 中输入的值也总是会返回字符串类型
```

- .trim

如果要自动过滤用户输入的首尾空格，可以添加 trim 修饰符到 v-model 上过滤输入：

```
<input v-model.trim="msg">
```

##组件



##vue-cli + webpack

```
$ npm install -g vue-cli
$ vue init webpack my-project
$ cd my-project
$ npm install
$ npm run dev
```

#Webpack

##模块系统

###CommonJS规范

服务器端的 Node.js 遵循 CommonJS规范，该规范的核心思想是允许模块通过 require 方法来同步加载所要依赖的其他模块，然后通过 exports 或 module.exports 来导出需要暴露的接口。

**优点**

- 服务器端模块便于重用
- NPM 中已经有将近20万个可以使用模块包
- 简单并容易使用

**缺点**

- 同步的模块加载方式不适合在浏览器环境中，同步意味着阻塞加载，浏览器资源是异步加载的
- 不能非阻塞的并行加载多个模块

**实现**

- 服务器端的 Node.js

```
require("module");
require("../file.js");

exports.doStuff = function() {};
module.exports = someValue;
```

###AMD

Asynchronous Module Definition 规范其实只有一个主要接口 define(id?, dependencies?, factory)，它要在声明模块的时候指定所有的依赖 dependencies，并且还要当做形参传到 factory 中，对于依赖的模块提前执行，**依赖前置，预加载**。

**优点**

- 适合在浏览器环境中异步加载模块
- 可以并行加载多个模块

**缺点**

- 提高了开发成本，代码的阅读和书写比较困难，模块定义方式的语义不顺畅
- 不符合通用的模块化思维方式，是一种妥协的实现

**实现**

- [RequireJS](http://requirejs.org/)
- [curl](https://github.com/cujojs/curl)

```
define("module", ["dep1", "dep2"], function(d1, d2) {
  return someExportedValue;
});
require(["module", "../file"], function(module, file) { /* ... */ });
```

###CMD

**优点：**

- 依赖就近，延迟执行
- 可以很容易在 Node.js 中运行

**缺点：**

- 依赖 SPM 打包，模块的加载逻辑偏重

**实现：**

- [Sea.js](http://seajs.org/docs/)
- [coolie](https://github.com/cooliejs/coolie.js)

```
define(function(require, exports, module) {
  // 依赖加载
  var $ = require('jquery');
  var Spinning = require('./spinning');
  exports.doSomething = ...
  module.exports = ...
})
```
###ES6模块 

ES6 模块的设计思想，是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。

**优点：**

- 容易进行静态分析
- 面向未来的 EcmaScript 标准

**缺点：**

- 原生浏览器端还没有实现该标准
- 全新的命令字，新版的 Node.js才支持

**实现：**

- [Babel](https://babeljs.io/)

```
import "jquery";

export function doStuff() {}

module "localModule" {}
```

##使用

###安装

```
$ npm install webpack -g

$ npm install webpack-dev-server -g
```

###使用

静态页面html文件

```
<!-- index.html -->
<html>
<head>
  <meta charset="utf-8">
</head>
<body>
  <!--引入bundle.js文件-->
  <script src="bundle.js"></script>
</body>
</html>
```
增加module模块

```
// module.js
module.exports = 'It works from module.js.'
```
入口js文件

```
// entry.js
document.write('It works.')
document.write(require('./module.js')) // 添加模块
```
编译

```
$ webpack entry.js bundle.js
```
打开index.html文件查看编译后样式

##loader

在引用 loader 的时候可以使用全名 json-loader，或者使用短名 json。这个命名规则和搜索优先级顺序在 webpack 的 resolveLoader.moduleTemplates api 中定义。

Default: ["\*-webpack-loader", "\*-web-loader", "\*-loader", "*"]

###css-loader

Webpack 本身只能处理 JavaScript 模块，如果要处理其他类型的文件，就需要使用 loader 进行转换。

Loader 可以理解为是模块和资源的转换器，它本身是一个函数，接受源文件作为参数，返回转换的结果。这样，我们就可以通过 require 来加载任何类型的模块或文件，比如 CoffeeScript、 JSX、 LESS 或图片。

安装 loader：

`npm install css-loader style-loader`

css文件:

```
/* style.css */
body { background: yellow; }
```

修改 entry.js：

```
require("!style!css!./style.css") // 载入 style.css
document.write('It works.')
document.write(require('./module.js'))
```
执行：

方法一： `webpack`

方法二：

```
将 entry.js 中的 require("!style!css!./style.css") 修改为 require("./style.css") ，然后执行：

$ webpack entry.js bundle.js --module-bind 'css=style!css'
```
方法三：

配置文件 webpack.config.js

```
var webpack = require('webpack')

module.exports = {
  entry: './entry.js',
  output: {
    path: __dirname,
    filename: 'bundle.js'
  },
  module: {
    loaders: [
      {test: /\.css$/, loader: 'style!css'}
    ]
  }
}
```
同时简化 entry.js 中的 style.css 加载方式：

```
require('./style.css')
```


###Babel-loader

Babel-loader 能够将jsx/es6文件转换成js文件。

安装： `npm install Babel-loader`

安装： babel-preset-es2015 and babel-preset-react 插件

webpack.config.js:

```
module.exports = {
  entry: './main.jsx',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        loader: 'babel-loader?presets[]=es2015&presets[]=react'
      },
    ]
  }
};
```
或者通过query选项

```
module: {
  loaders: [
    {
      test: /\.jsx?$/,
      exclude: /node_modules/,
      loader: 'babel',
      query: {
        presets: ['es2015', 'react']
      }
    }
  ]
}
```

###img-loader

安装： npm install img-loader url-oader --save-dev

webpack.config.js

```
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192' }
    ]
  }
};
```

imgModule.js

```
var img1 = document.createElement("img");
img1.src = require("./small.png");
document.body.appendChild(img1);

var img2 = document.createElement("img");
img2.src = require("./big.png");
document.body.appendChild(img2);
```

webpack.config.js

```
module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      { test: /\.(png|jpg)$/, loader: 'url-loader?limit=8192' }
    ]
  }
};
```
###css-module

安装：npm install css-module --save-dev

index.html

```
<html>
<body>
  <h1 class="h1">Hello World</h1>
  <h2 class="h2">Hello Webpack</h2>
  <div id="example"></div>
  <script src="./bundle.js"></script>
</body>
</html>
```

app.css

```
.h1 {
  color:red;
}

:global(.h2) {
  color: blue;
}
```

main.jsx

```
var React = require('react');
var ReactDOM = require('react-dom');
var style = require('./app.css');

ReactDOM.render(
  <div>
    <h1 className={style.h1}>Hello World</h1>
    <h2 className="h2">Hello Webpack</h2>
  </div>,
  document.getElementById('example')
);
```

webpack.config.js

```
module.exports = {
  entry: './main.jsx',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['es2015', 'react']
        }
      },
      {
        test: /\.css$/,
        loader: 'style-loader!css-loader?modules'
      }
    ]
  }
};
```
h1是局部样式，只能在style.h1添加的样式中显示，h2是全局样式，所有class都可以显示

##插件

插件的使用一般是在 webpack 的配置信息 plugins 选项中指定，修改 webpack.config.js，添加 plugins：

```
var webpack = require('webpack')
// 自带插件
var uglifyJsPlugin = webpack.optimize.UglifyJsPlugin;
// 外部安装插件
var HtmlwebpackPlugin = require('html-webpack-plugin');

module.exports = {
  entry: './entry.js',
  output: {
    path: __dirname,
    filename: 'bundle.js'
  },
  module: {
    loaders: [{test: /\.css$/,loader: 'style!css'}]
  },
  plugins: [
    new webpack.BannerPlugin('This file is created by zhaoda'),
    new uglifyJsPlugin({
      compress: {
        warnings: false
      }
    }),
    new HtmlwebpackPlugin({
      title: 'Webpack-demos',
      filename: 'index.html'
    })
  ]
}
```

再运行webpack即可

###全局插件变量

main.js

```
$('h1').text('Hello World');

```
webpack.config.js
 
```
var webpack = require('webpack');

module.exports = {
  entry: {
    app: './main.js'
  },
  output: {
    filename: 'bundle.js'
  },
  plugins: [
    new webpack.ProvidePlugin({
      $: "jquery",
      jQuery: "jquery",
      "window.jQuery": "jquery"
    })
  ]
};
```
###暴露全局变量

For example, we have a data.js.

```
var data = 'Hello World';
```

We can expose data as a global variable.

webpack.config.js

```
module.exports = {
  entry: './main.jsx',
  output: {
    filename: 'bundle.js'
  },
  module: {
    loaders:[
      {
        test: /\.js[x]?$/,
        exclude: /node_modules/,
        loader: 'babel-loader',
        query: {
          presets: ['es2015', 'react']
        }
      },
    ]
  },
  externals: {
    // require('data') is external and available
    //  on the global var data
    'data': 'data'
  }
};
```
Now, you require data as a module variable in your script. but it actually is a global variable.

main.jsx

```
var data = require('data');
var React = require('react');
var ReactDOM = require('react-dom');

ReactDOM.render(
  <h1>{data}</h1>,
  document.body
);
```
##环境变量 Environment flags 

`var TARGET = process.env.npm_lifecycle_event;` 
获取环境启动变量 如 npm run start 中的start

main.js

```
document.write('<h1>Hello World</h1>');

if (__DEV__) {
  document.write(new Date());
}
```

index.html

```
<html>
<body>
  <script src="bundle.js"></script>
</body>
</html>
```

webpack.config.js

```
var webpack = require('webpack');

var devFlagPlugin = new webpack.DefinePlugin({
  __DEV__: JSON.stringify(JSON.parse(process.env.DEBUG || 'false'))
});

module.exports = {
  entry: './main.js',
  output: {
    filename: 'bundle.js'
  },
  plugins: [devFlagPlugin]
};
```

Now pass environment variable into webpack.

```
# Linux & Mac
$ env DEBUG=true webpack-dev-server

# Windows
$ set DEBUG=true
$ webpack-dev-server
```
##代码分离

webpack自带，无需插件，Webpack actually builds main.js and a.js into different chunks(bundle.js and 1.bundle.js), and loads 1.bundle.js from bundle.js when on demand.

main.js

```
require.ensure(['./a'], function(require) {
  var content = require('./a');
  document.open();
  document.write('<h1>' + content + '</h1>');
  document.close();
});
```

a.js

```
module.exports = 'Hello World';
```

##开发环境

让编译的输出内容带有进度和颜色，启动监听模式

方式一：

```
$ webpack --progress --colors --watch
```

方式二：

```
# 安装
$ npm install webpack-dev-server -g

# 运行
$ webpack-dev-server --progress --colors
```
在浏览器访问 127.0.0.1:8080打开网页


#ES6

[ES6阮一峰](http://es6.ruanyifeng.com/)

##命令

- 查看node已经实现的es6特性

`$ node --v8-options | grep harmony`

- 查看Node对es6的支持程度

```
$ npm install -g es-checker

$ es-checker
```

##babel转码器

###配置.babelrc

```
  {
    "presets": [
      "es2015",
      "react",
      "stage-2"
    ],
    "plugins": []
  }
```
转码规则：

```
# ES2015转码规则
$ npm install --save-dev babel-preset-es2015

# react转码规则
$ npm install --save-dev babel-preset-react

# ES7不同阶段语法提案的转码规则（共有4个阶段），选装一个
$ npm install --save-dev babel-preset-stage-0
$ npm install --save-dev babel-preset-stage-1
$ npm install --save-dev babel-preset-stage-2
$ npm install --save-dev babel-preset-stage-3
```

###命令行转码babel-cli

安装：

```
$ npm install --global babel-cli
```

在命令行全局转码：

```
# 转码结果输出到标准输出
$ babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ babel example.js --out-file compiled.js
# 或者
$ babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ babel src --out-dir lib
# 或者
$ babel src -d lib

# -s 参数生成source map文件
$ babel src -d lib -s
```

在项目中转码：

```
# 安装
$ npm install --save-dev babel-cli
```
更改package.json，添加build

```
{
  // ...
  "devDependencies": {
    "babel-cli": "^6.0.0"
  },
  "scripts": {
    "build": "babel src -d lib"
  },
}
```
转码的时候，就执行下面的命令。

```
$ npm run build
```
###babel-node REPL环境

babel-cli工具自带一个babel-node命令，提供一个支持ES6的REPL环境。

它支持Node的REPL环境的所有功能，而且可以直接运行ES6代码。

```
$ babel-node
> (x => x * 2)(1)
2

# babel-node命令可以直接运行ES6脚本。将上面的代码放入脚本文件es6.js，然后直接运行。
$ babel-node es6.js
2

# babel-node也可以安装在项目中。
$ npm install --save-dev babel-cli

# 然后，改写package.json。
{
  "scripts": {
    "script-name": "babel-node script.js"
  }
}
上面代码中，使用babel-node替代node，这样script.js本身就不用做任何转码处理。
```

###babel-register

babel-register模块改写require命令，为它加上一个钩子。此后，每当使用require加载.js、.jsx、.es和.es6后缀名的文件，就会先用Babel进行转码。

```
$ npm install --save-dev babel-register

// 使用时，必须首先加载babel-register。
require("babel-register");
require("./index.js");
// 然后，就不需要手动对index.js转码了。
```

需要注意的是，babel-register只会对require命令加载的文件转码，而不会对当前文件转码。

另外，由于它是实时转码，所以只适合在开发环境使用。

###babel-core

调用Babel的API进行转码

```
#安装
npm install babel-core --save

// 使用
var babel = require('babel-core');

// 字符串转码
babel.transform('code();', options);
// => { code, map, ast }

// 文件转码（异步）
babel.transformFile('filename.js', options, function(err, result) {
  result; // => { code, map, ast }
});

// 文件转码（同步）
babel.transformFileSync('filename.js', options);
// => { code, map, ast }

// Babel AST转码
babel.transformFromAst(ast, code, options);
// => { code, map, ast }
// 配置对象options，可以参看官方文档http://babeljs.io/docs/usage/options/。

// 下面是一个例子。

var es6Code = 'let x = n => n + 1';
var es5Code = require('babel-core')
  .transform(es6Code, {
    presets: ['es2015']
  })
  .code;
// '"use strict";\n\nvar x = function x(n) {\n  return n + 1;\n};'
// 上面代码中，transform方法的第一个参数是一个字符串，表示需要被转换的ES6代码，第二个参数是转换的配置对象。
```

###babel-polyfill

Babel默认只转换新的JavaScript句法（syntax），而不转换新的API，比如Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise等全局对象，以及一些定义在全局对象上的方法（比如Object.assign）都不会转码。

举例来说，ES6在Array对象上新增了Array.from方法。Babel就不会转码这个方法。如果想让这个方法运行，必须使用babel-polyfill，为当前环境提供一个垫片。

```
#安装
$ npm install --save babel-polyfill

// 然后，在脚本头部，加入如下一行代码。
import 'babel-polyfill';
// 或者
require('babel-polyfill');
```

###浏览器环境

**方法一：**

Babel也可以用于浏览器环境。但是，从Babel 6.0开始，不再直接提供浏览器版本，而是要用构建工具构建出来。如果你没有或不想使用构建工具，可以通过安装5.x版本的babel-core模块获取。

`$ npm install babel-core@5`
运行上面的命令以后，就可以在当前目录的node_modules/babel-core/子目录里面，找到babel的浏览器版本browser.js（未精简）和browser.min.js（已精简）。

然后，将下面的代码插入网页。

```
<script src="node_modules/babel-core/browser.js"></script>
<script type="text/babel">
// Your ES6 code
</script>
```
上面代码中，browser.js是Babel提供的转换器脚本，可以在浏览器运行。用户的ES6脚本放在script标签之中，

但是要注明 **type="text/babel"**。

**方法二：**

使用babel-standalone模块提供的浏览器版本，将其插入网页。

```
<script src="https://cdnjs.cloudflare.com/ajax/libs/babel-standalone/6.4.4/babel.min.js"></script>
<script type="text/babel">
// Your ES6 code
</script>
```
注意，网页中实时将ES6代码转为ES5，对性能会有影响。生产环境需要加载已经转码完成的脚本。

**方法三：**

下面是如何将代码打包成浏览器可以使用的脚本，以Babel配合Browserify为例。首先，安装babelify模块。

```
$ npm install --save-dev babelify babel-preset-es2015
# 然后，再用命令行转换ES6脚本。

$  browserify script.js -o bundle.js \
  -t [ babelify --presets [ es2015 ] ]
# 上面代码将ES6脚本script.js，转为bundle.js，浏览器直接加载后者就可以了。

# 在package.json设置下面的代码，就不用每次命令行都输入参数了。

{
  "browserify": {
    "transform": [["babelify", { "presets": ["es2015"] }]]
  }
}
```
###Traceur转码器

Google公司的Traceur转码器，也可以将ES6代码转为ES5代码

[链接——阮一峰](http://es6.ruanyifeng.com/#docs/intro#Traceur转码器)

##const和let


