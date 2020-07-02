
#1. Introduction


1. Install Node on your computer, then run the commands node --version and npm --version to see which versions you have. 
``` bash
#Ubuntu/Linux 18.04
> sudo apt update 
> sudo apt install nodejs 
> node --version 
> sudo apt install npm 
> npm --version 
```
#2. Basic Features

### TYPEOF 
What kind of thing is typeof? Is it an expression? A function? Something else?
(You might notice that typeof typeof is syntactically invalid. In such circum­stances, an Internet search engine is your friend, as is the Mozilla Developer Net­work JavaScript reference.

**TYPEOF is a built-in operator. Typeof operator returns a sring indicating the type of the unevaluated oprand.**

### FILL IN THE BLANKS
1. What does Array.push do? 

    **Array.push appends an element to the end of the array 'Array'**

2. How does a while loop work? 

	**A while loop executes repeatedly based on a given boolean condition.**

3. What does += do? 

	**+= is a compound assignment operator. It increments the variable on the left by the value on the right and assigns it to the value on the left.**

``` javascript 
x += 2
# Is equivalent to 
x =  x + 2
```
4. What does Array.reverse do, and what does it return? 

	**Array.reverse calls the function reverse() to change the sequenece of the array 'Array' and returns the reverse sequence.**

``` javascript 
let current = 0
let table = [] 
while(current < 5){
    const entry `square of ${current} is ${curret current}`
    table.push(entry)
    current += 1 
}
table.reverse()
for(let line of table){
    console.log(line) 
}
```

### WHAT IS TRUTH? 

Write a function called isTruthy that returns true for everything that JavaScript 
considers truthy, and false for everything it considers falsy except empty arrays: 
isTruthy should return false for those. 

``` javascript 
const isTruthy = (values) => {
	let array = []; 
	for(let element of values){
		if(element ){
			if(Array.isArray(element) && !element.length){
				array.push(false);
			}
			else{
				array.push(true); 
			}
		}
		else{
			array.push(false); 		
		}	
	}
	return(array);
}
let values = ['0','false',[],{},function(){},false, 0, '', "", null, undefined, NaN];
console.log(isTruthy(values));

```
### THE SHAPE OF THINGS TO COME
 
We wrote the example function, limits, above to return [undefined,undefined]
if a variable with no length is fed into it. What is the advantage of doing this as
opposed to returning undefined only?

**The function lmits returns both the lowest and highest values in the array, not just one. [undefined, undefined] means both lowest and highest values are undefined.**


### COMBINING DIFFERENT TYPES 

What does <b>NaN</b> represent? What output would you expect from the code below?
Try running it and see whether the results match your expectations. What are the
implications of this behavior when working with real-world data?

**NaN stands for Not a Number. The elements in the array 'first' are summed and stored in the variable total. The sum of the second array will be a NaN. The real world implications is that a dataset that includes a NaN element will compute as NaN**
``` javascript 
const first = [3, 7, 8, 9 , 1]
console.log(`aggregating ${first}`)
let total = 0
for(let d of first){
	total +=d
}
console.log(total)

const second = [0, 3, -1, NaN, 8]
console.log(`aggregating ${second}`)
total = 0
for (let d of second){
	total += d
}
console.log(total)
```
### WHAT DOES THIS DO? 
Explain what is happening in the assignment statement that creates the constant
creature.

**The constant creature is an object with genus and species as the keys and 'Callithrix' and 'Jacchus' as values**
``` javascript 
const genus = 'Callithrix'
const species = 'Jacchus'
const creature = {genus, species}
console.log(creature)

```
### DESTRUCTURING ASSIGNMENT 
When this short program runs:
``` javascript 
const creature = {
	genus: 'Callithrix', 
	species: 'Jacchus'
}
const {genus, species} = creature
console.log(`genus is ${genus}`)
console.log(`species is ${species}`)
```
it produces 

genus is Callithrix <br>
species is Jacchus 

but when this program runs: 

``` javascript 
const creature = {
	first: 'Callithrix', 
	second: 'Jacchus'
}
console.log(`genus is ${genus}`)
console.log(`species is ${species}`)
```
it produces: 

genus is undefined <br>
species is undefined 

1. What is the difference between these two programs?<br>**The name of the keys in the first program are different from the second. The second program does not find a key-value pair because the keys for the object creature are 'first' and 'second'**

2. How does destructuring assignment work in general? <br>**The line {genus, species} = creature assigns values to the given keys. Destructuring assignment unpacks values form arrays, or properites from objects, into distinct variables.**
3. How can we use this technique to rewrite the require statement in
src/basics/import.js so that clip can be called directly as clip(...)
rather than as utilities.clip(...)? <br>**Us destructuring assignment to unpack utilities function onto clip**
``` javascript
const utilities = require('./utilities')
const {clip} =  utilities; 

const data = [-1, 5, 3, 0, 10]
console.log(`clip(${data}) -> ${clip(data)}`)
console.log(`clip(${data}, 5) -> ${clip(data, 5)}`)

```
### RETURN TO ME, FOR MY HEART WANTS YOU ONLY
What output would you see in the console if you ran this code?
``` javascript 
const verbose_sum = (first, second) => {
    console.log(`Going to add ${first} to ${second}`)
    let total = first + second
    return(total)
    console.log(`Finishing summing`)
}
var result = verbose_sum(3, 6)
console.log(result)
```
**3. Going to add 3 to 6 <br>9**

# 3. Callbacks

## SIDE EFFECTS WITH FOREACH 
JavaScript arrays have a method called forEach, which calls a callback function once for each element of the array. Unlike map, forEach does not save the values returned by these calls or return an array of results. The full syntax is: 

``` javascript 
someArray.forEach((value, location, container) => {
	// 'value' is the value in 'someArray'
	// 'location' is the index of the value 
	// 'container' is the containing array (in this case, 'someArray')
})
```
If you only need the value, you can provide a callback that only takes one parameter; if you only need the value and its location, you can provide a callback that takes two. Use this to write a funtion doubleInPlace that doubles all the values in an array in place: 

``` javascript 
const vals = [1, 2, 3]
doubleInPlace(vals)
console.log(`vals after change: ${vals}`)

```

``` javascript 

var doubleInPlace = (values) => {
	values.forEach( (element, index, container) => {
      container[index] = element*2;
    });
}

```

# ANNOTATING DATA 

Given an array of objects representing observations of wild animas: 
``` javascript 
data = [
	{'date': '1977-7-16', 'sex':'M', 'species': 'NL'},
	{'date': '1977-7-16', 'sex':'M', 'species': 'NL'},
	{'date': '1977-7-16', 'sex':'F', 'species': 'DM'},
	{'date': '1977-7-16', 'sex':'M', 'species': 'DM'},
	{'date': '1977-7-16', 'sex':'M', 'species': 'DM'}, 
	{'date': '1977-7-16', 'sex':'M', 'species': 'PF'},
	{'date': '1977-7-16', 'sex':'F', 'species': 'PE'},
	{'date': '1977-7-16', 'sex':'M', 'species': 'DM'}
]
```
write a function that returns a new array of object like this: 

``` javascript 
newData = [
	{'seq': 3, 'year': '1977', 'sex': 'F', 'species': 'DM'},
	{'seq': 7, 'year': '1977', 'sex': 'F', 'species': 'PE'}
]
```
<i>without</i> using any loops. The changes are: 

- The date field is replaced with just the year 
- Only observations of female animals are retained 
- The retained records are given sequence numbers to relate them back to the orginal data. (These sequence numbers are 1-based rather 0-based.)

You will probably want to use Array.reduce to generate the sequence numbers. 

''' javascript 
const result = data.filter((x) => { if(x.sex == 'F') return(x)}) 
```