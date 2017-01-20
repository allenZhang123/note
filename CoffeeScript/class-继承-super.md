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
