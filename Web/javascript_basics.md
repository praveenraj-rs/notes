# javascript_basics

```js
console.log("Hello, World!")

let a = 'String Type'
let b = 5
let c = 5.00
let d = true
let e = false
let f = undefined
let g =  null

const a = 'String Type'
const b = 5
const c = 5.00
const d = true
const e = false
const f = undefined
const g =  null

a = 1
console.log(++a) // 2

b = 1
console.log(a++) // 1
console.log(a) // 2

a+=b // a = a+b
a*=b
a/=b
a%=b

// Object
a = {firstName:'praveen',lastName:'raj'}
// Array
b = ['praveen','raj']

console.log('1'+'2') // 12
console.log('1'+2) // 12
console.log('1'-'2') // -1
console.log('1'-2) // -1
console.log('1'*2) // 2
console.log(parseInt('1')+parseInt('2')) // 3
console.log(parseFloat('3.14')) // 3.14
console.log(String(3.124)) // '3.124'
consoe.log((1).toString()) // '1'
console.log(Booloean(5)) // true


const a = true?1:2 // a = 1

// Conditional Statement
a>b
a<b
a<=b
a>=b
a==b
a!=b
a===b
a!==b
!a

a&&b
a||b
!a

// bitwise
a&b //and
a|b //or
a^b //xor
~a //not

if(a==b){console.log('a is equal to b')}
else if(a<b){console.log('a is lessthan b')}
else{ consoel.log('a is greater than b')}

switch(color){
	case 'red':
		console.log('Color is Red')
		break
	case 'green':
		console.log('Color is Green')
		break
	default:
		console.log('Not a valid color')
		break
}

// For Loop
for (let i=1;i<=5;i++){
	console.log(i)
}

// While Loop
let i=1
while(i<=5){
	console.log(i)
	i++
}

// Do While Loop
let i=1
do{
	console.log(i)
	i++
}while(i<=5)

// For of Loop
const a = ['first','secound','third']
for(const i of a){
	console.log(i)
}

// Function
function sum(a,b){
	return a+b
}

// Arrow Function 
const sum=(a,b)=>{
	return a+b
}

Math.sqrt(4) // 2

// String Manipulation

let str = 'praveenrajrs'
str.length //12
str.charAt(0) //p
str.charCodeAt(0) //112
str.at(0) //p
str.at(-1) //s
str[0] //p

str1 = str.slice(0,7) //praveen
str1 = str.slice(7) //rajrs
str1 = str.slice(-2) //rs
str1 = str.slice(-12,-1) //praveenrajr
str1 = str.slice(0,-2) //praveenraj

str2 = str.substring(0,7) //praveen
str2 = str.substring(7) //rajrs
str2 = str.substring(-2) //praveenrajrs

str3 = str.substr(0,7) //praveen
str3 = str.substr(7) //rajrs
str3 = str.substr(-2) //rs

str.toUpperCase() //PRAVEENRAJRS
str.toLowerCase() //praveenrajrs

str = ' praveenrajrs '
str.trimStart() //'praveenrajrs '
str.trimEnd() //' praveenrajrs'
str.trim() //'praveenrajrs'

text="r"
str1 = text.padStart(5,"e") //eeeer
str1 = text.padEnd(5,"e") //reeee

text='raj'
text.repeat(2) //rajraj

text='world world'
newText = text.replace('world','hello') // hello world
newText = text.replace(/WORLD/i,'hello') // hello world
newText = text.replace(/world/g,'hello') // hello hello
newText = text.replaceAll('world','hello') // hello hello

newTextArray = text.split(" ")//["world","world"]

```


### Nested function's scope
```js
// Nested Function
function outer(a){
	const b = 2
	function inner(b){
		console.log(a,b)
	}
	inner(b)
}
const a = 1
outer(a)
```
### Closures
```js
// Closure
// That combination of the function and its scope chain is what is called a closure in JavaScript.
function outer(){
	let count = 0
	function inner(){
		count++
		console.log(count)
	}
	return inner
}
const fn = outer()
fn()
fn()
// 1 2
```
### Currying
```js
// Currying Function
const sum=(a,b)=>{
	return a+b
}

const curried=(fn)=>{
	return function(a){
		console.log(a)
		return function(b){
			console.log(b)
			return fn(a,b)
		}
	}
}

const curFun=curried(sum)
//console.log(curFun(1)(2))

const add = curFun(2)
const add1 = add(3) 
const add2 = add(2)
console.log(add1)
console.log(add2)
```
### This keyword
- Implicit binding
- Explicit binding
- New binding
- Default binding

#### Implicit Binding
```js
const ob1 = {
name:"praveenrajrs",
tellName:function(){console.log(`My name is ${this.name}`)}
}
ob1.tellName()
```

#### Explicit Binding
```js
const ob1 = {
	 name:"praveenrajrs"
}
function tellName(){
	console.log(`My name is ${this.name}`)
}

tellName.call(ob1)
```

#### New binding
```js
function person(name){
	this.name = name
}

const p1 = new person('praveen')
const p2 = new person('raj')

console.log(p1.name,p2.name)
```

#### Default binding
```js
function person(){
	console.log(`My name is ${this.name}`)
}

person()

globalThis.name = 'raj'
function pr(){
	console.log(`pr name is ${this.name}`)
}
pr()

// My name is undefined
// pr name is raj
```

### Prototype
```js
function person(fName,lName){
	this.firstName = fName
	this.lastName = lName
}

const person1 = new person('praveen','raj')
const person2 = new person('raj','praveen')

person.prototype.getFullName=function(){
	return this.firstName+" "+this.lastName
}

console.log(person1.getFullName())
console.log(person2.getFullName())
```

### Prototype inheritance
```js
function person(fName,lName){
	this.firstName = fName
	this.lastName = lName
}

const person1 = new person('praveen','raj')
const person2 = new person('raj','praveen')

person.prototype.getFullName=function(){
	return this.firstName+" "+this.lastName
}

console.log(person1.getFullName())
console.log(person2.getFullName())


function superHero(ffName,llName){
	person.call(this,ffName,llName)
	this.isSuperHero = true
}

superHero.prototype = Object.create(person.prototype)
superHero.prototype.constructor = superHero

const ironman = new superHero('robert','downey')
console.log(ironman.firstName)
console.log(ironman.getFullName())
```
### Class
```js
class person{
	constructor(fName,lName){
		this.firstName = fName
		this.lastName = lName
	}
	getFullName(){
		return this.firstName+" "+this.lastName
	}
}

const p1 =new person('praveen','raj')
console.log(p1.getFullName())
```

Inherited Class
```js
class person{
	constructor(fName,lName){
		this.firstName = fName
		this.lastName = lName
	}
	getFullName(){
		return this.firstName+" "+this.lastName
	}
}

const p1 =new person('praveen','raj')
console.log(p1.getFullName())

class superHero extends person{
	constructor(ffName,llName){
		super(ffName,llName)
		this.superHero = true
	}
	fight(){
		return 'Fighting for Justice'
	}
}

const ironman = new superHero('robert','downey')
console.log(ironman.fight())
console.log(ironman.getFullName())
```
### Generators 
```js
const ar1 = ['hello','world']
for (const word of ar1){
	console.log(word)
}

function* generatorFunction(){
	yield 'Hello'
	yield 'World'
}

const generatorObject =  generatorFunction()
for(const word of generatorObject){
	console.log(word)
}
```


## Asynchronous

```js
// setTimeout(functionRef, delay, param1, param2)
setTimeout(func,1000,arg1,arg2) // 1000=1sec
ftime = setTimeOut(func,1000,arg1,arg2)
clearTimeout(ftime)
```

##### async and await

##### Sequential Execution 
```js
function resolveHello() {
  return new Promise((resolve) => {
    setTimeout(function () {
      resolve("Hello");
    }, 2000);
  });
}

function resolveWorld() {
  return new Promise((resolve) => {
    setTimeout(function () {
      resolve("World");
    }, 1000);
  });
}

async function sequentialStart() {
  const hello = await resolveHello();
  console.log(hello); // Logs after 2 seconds
  const world = await resolveWorld();
  console.log(world); // Logs after 2 + 1 = 3 seconds
}
sequentialStart();

```

##### Concurrent Execution 
```js
function resolveHello() {
  return new Promise((resolve) => {
    setTimeout(function () {
      resolve("Hello");
    }, 2000);
  });
}

function resolveWorld() {
  return new Promise((resolve) => {
    setTimeout(function () {
      resolve("World");
    }, 1000);
  });
}

async function concurrentStart() {
  const hello = resolveHello();
  const world = resolveWorld();
  console.log(await hello); // Logs after 2 seconds
  console.log(await world); // Logs after 2 seconds
}
concurrentStart();

```

##### Parallel Execution
```js
function resolveHello() {
  return new Promise((resolve) => {
    setTimeout(function () {
      resolve("Hello");
    }, 2000);
  });
}

function resolveWorld() {
  return new Promise((resolve) => {
    setTimeout(function () {
      resolve("World");
    }, 1000);
  });
}

function parallel() {
  Promise.all([
    (async () => console.log(await resolveHello()))(), // Logs after 2 seconds
    (async () => console.log(await resolveWorld()))(), // Logs after 1 second
  ]);
}
parallel();

```
## DOM Elements

HTML elements like `<div>`, `<p>`, `<h1>`, etc., are represented as objects in the DOM. 
These objects have properties and methods that you can manipulate using JavaScript.

## Accessing DOM Elements

- Use `document.getElementById('id')` to get a reference to an element by its ID.
- Use `document.getElementsByClassName('class')` or `document.getElementsByTagName('tag')` to select elements by class or tag name.
- Use `document.querySelector('selector')` or `document.querySelectorAll('selector')` for more flexible element selection.

## Manipulating DOM Elements

- Change the content of an element using `element.innerHTML` or `element.textContent`.
- Modify element attributes with `element.getAttribute('attribute')` and `element.setAttribute('attribute', 'value')`.
- Change CSS styles with `element.style.property`.

## Creating and Appending Elements

- Create new elements with `document.createElement('tag')`.
- Append elements to the DOM using `parentElement.appendChild(newElement)`.

## Event Handling

- Use `element.addEventListener('event', callback)` to handle events like clicks, key presses, etc.
- The `event` object contains information about the event, such as the target element.

## DOM Traversal

- Move through the DOM tree using properties like `parentNode`, `childNodes`, `nextSibling`, and `previousSibling`.
- Use `element.querySelector('selector')` to find descendants of an element.

## DOM Manipulation Best Practices

- Minimize direct manipulation; consider creating functions for repeated tasks.
- Use `classList` to manipulate classes and keep CSS separate from JavaScript.
- Optimize by minimizing re-flows and repaints.

## Asynchronous JavaScript and the DOM

- Understand how asynchronous tasks affect the DOM.
- Use `setTimeout` and `setInterval` for asynchronous operations.
- Handle AJAX requests and Promises for efficient data retrieval.

# JSON Basics

## `JSON.parse()`

- Use `JSON.parse()` to convert a JSON string into a JavaScript object.
- Example: `let jsonObj = JSON.parse(jsonString);`

## `JSON.stringify()`

- Use `JSON.stringify()` to convert a JavaScript object into a JSON string.
- Example: `let jsonString = JSON.stringify(jsonObject);`

## Local Storage with JSON

- Store structured data in local storage using JSON.
- Use `JSON.stringify()` to save data and `JSON.parse()` to retrieve it.
