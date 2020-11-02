`document ready`

```js
$(document).ready(function(){
	//do something
})
```



`jquery ready`

```js
$(function(){
	//do something
})
```



`$.ajax()`

```js
$.ajax({
	url:"/save";
	data:{name:"jack",age:18};
	type:"POST";
	dataType:"json";
	success:function(msg){
		//do something
	}
})
```



`$.post()`

> 形式：$.post(url,data,func,dataType)

```js
$.post(
	"/save",
	{name:"mike",age:"20"},
	function(data){
		//do something
	},
	"json"
)
```



`$.get()`

> 形式：$.post(url,data,func,dataType)

```js
$.get(
	"/get",
	{"id",1},
	function(data){
		//do something
	},
	"json"
)
```



`$.getJSON()`

> 形式：$.getJSON(url,data,func)

```js
$.getJSON(
	"/getjosn",
	"{id:1}",
	function(data){
		//do something
	}
)
```