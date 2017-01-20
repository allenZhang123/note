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
