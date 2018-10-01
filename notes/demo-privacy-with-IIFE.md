# Demo: Privacy utilizing an IIFE

- Below we will look at 2 (failed) attempts to create *private* functions or methods. In part #3 of this demo we will use the *revealing module pattern* to export a public interface from an IIFE, while successfully hiding functions and variables that we want to be hidden.

**counter-start.html**

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="utf-8" />
	<title>Counter!</title>
	<style>
		*{font-family:sans-serif;font-size:1.2em}
		button{margin-right:.7em;padding:.3em;}
	</style>
</head>
<body>
<p id="total">???</p>
<button id="subtract">-</button><button id="add">+</button><button id="clear">CLEAR</button>
<script>

// #1 - Everything is public
	let counter = 0;
	let lastOperation = "clear"; // we would like this to be "private"
	
	// no negative numbers allowed
	// we would like this to be "private"
	function validateCounter(number){
		return number < 0 ? 0 : number; 
	}
	
	function buttonClicked(e){
		lastOperation = e.target.id;
		switch(lastOperation){
			case "subtract":
				counter --;
				break;
			case "add":
				counter ++;
				break;
			case "clear":
				counter = 0;
				break;
		}
		counter = validateCounter(counter);
		document.querySelector("#total").innerHTML = counter;
	}

	//button event listeners
	document.querySelector("#subtract").onclick = buttonClicked;
	document.querySelector("#add").onclick = buttonClicked;
	document.querySelector("#clear").onclick = buttonClicked;
	
	// initialize #total element
	document.querySelector("#total").innerHTML = counter;
	

// #2 - Everything is still public, even with a class
// 	class Counter{
// 		constructor(){
// 			this.counterValue = 0;
// 			this.lastOperation = "clear";
// 		}
// 		add(){
// 			this.counterValue++;
// 		}
// 		subtract(){
// 			this.counterValue --;
// 			this.validateCounter(this.counterValue);
// 		}
// 		clear(){
// 			this.counterValue = 0;
// 		}
// 		// no negative numbers allowed
// 		validateCounter(number){
// 			this.counterValue =  number < 0 ? 0 : this.counterValue; 
// 		}
// 	}
// 	
// 	// button event listeners
// 	document.querySelector("#subtract").onclick = buttonClicked;
// 	document.querySelector("#add").onclick = buttonClicked;
// 	document.querySelector("#clear").onclick = buttonClicked;
// 	
// 	
// 	// initialize Counter instance
// 	let counter = new Counter();
// 	
// 	// initialize #total element
// 	document.querySelector("#total").innerHTML = counter.counterValue;
// 	
// 	function buttonClicked(e){
// 		counter.lastOperation = e.target.id;
// 		switch(counter.lastOperation){
// 			case "subtract":
// 				counter.subtract();
// 				break;
// 			case "add":
// 				counter.add();
// 				break;
// 			case "clear":
// 				counter.clear();
// 				break;
// 		}
// 		document.querySelector("#total").innerHTML = counter.counterValue;
// 	}


// #3 - Information hiding via an IIFE

// let's write this together!
</script>
</body>
</html>
```
