
### Big 0 notation
```
O(1)
O(logn)
O(n)
O(nlogn)
O(n^2)
O(2^n)
O(n!)
```

### Summation of n number

#### O(n)
```js
const summation=(n)=>{
	let sum=0;
	for(let i=1;i<=n;i++){
		sum+=i;
	}
	return sum;
}
console.log(summation(5));
```

#### O(1)
```js
const summation=(n)=>{
	return n*(n+1)/2;
}
console.log(summation(5));
```

### Fibonacci Series
```js
const fibonacci=(n)=>{
	let fib=[];
	fib[0]=0;
	fib[1]=1;

	for (let i=2;i<=n;i++){
		fib[i]=fib[i-1]+fib[i-2];
	}
	return fib;
}
console.log(fibonacci(5));

// Time Complexity:  O(n)
// Space Complexity: O(n)
```

Recursive

```js
const fibonacci=(n)=>{
	if (n<2){
		return n;
	}

	return fibonacci(n-1)+fibonacci(n-2);
}

console.log(fibonacci(2));
console.log(fibonacci(4));

// Time Complexity:  O(2^n)
// Space Complexity: O(1)
```

### Factorial
```js
function factorial(n){
	if (n<=1){ return 1;}
	return n*factorial(n-1);
}

console.log(factorial(5));
```

```js
const factorial=(n)=>{
	if (n==1){
		return 1;
	}
	return n*factorial(n-1);
}
console.log(factorial(3));

// Time Complexity:  O(n)
// Space Complexity: O(1)
```
### Prime Number

```js
const checkPrime=(n)=>{
	if(n<2){
		return 0;
	}
	for (let i=2;i<=Math.sqrt(n);i++){
		if (n%i==0){
			return 0;
		}
	}
	return 1;
}

console.log(checkPrime(5)); // 1
console.log(checkPrime(2)); // 1
console.log(checkPrime(4)); // 0

// Time Complexity:  O(sqrt(n))
// Space Complexity: O(1)
```

### Power of Two
```js
const checkPowerOfTwo=(n)=>{
	if(n<1){
		return false;
	}

	while(n>1){
		if(n%2!=0){
			return false;
		}
		n=n/2;
	}
	return true;
}

console.log(checkPowerOfTwo(2));
console.log(checkPowerOfTwo(4));
console.log(checkPowerOfTwo(5));
console.log(checkPowerOfTwo(6));

// Time Complexity:  O(log(n))
// Space Complexity: O(1);
```


```js
const checkPowerOfTwo=(n)=>{
	if(n<1){
		return 0;
	}
	return (n&(n-1))==0;
}

console.log(checkPowerOfTwo(2));
console.log(checkPowerOfTwo(4));
console.log(checkPowerOfTwo(5));
console.log(checkPowerOfTwo(6));

// Time Complexity:  O(1)
// Space Complexity: O(1);
```

### Search Algorithms

#### Linear Search
```js
const linearSearch=(array,target)=>{
	for (let i=0;i<array.length;i++){
		if (array[i]==target){
			return i;
		}
	}
	return -1;
}

a1 = [1,2,3,4,5,6,7];
console.log(linearSearch(a1,7));

// Time Complexity: O(n)
// Space Complexity: O(1)
```

#### Binary Search
Only for the sorted array

```js
const binarySearch=(array,target)=>{
	let left = 0;
	let right = array.length-1;

	while (left<=right){
		let middle=Math.floor((right+left)/2);
		if (array[middle]==target){
			return middle;
		}

		else if(array[middle]<target){
			left = middle+1;
		}
		else{
			right =  middle-1;
		}
	}
	return -1;
}

ar1 = [1,2,3,4,5,6,7];
console.log(binarySearch(ar1,2));

// Time Complexity:  O(logn)
// Space Complexity: O(1)
```

### Sorting

#### Bubble Sort
```js
const bubbleSort=(ary)=>{
	let swapped
	do{
		swapped=false
		for(let i=0;i<ary.length-1;i++){
			if(ary[i]>ary[i+1]){
				let temp=ary[i]
				ary[i]=ary[i+1]
				ary[i+1]=temp
				swapped=true
			}
		}
	}while(swapped)
	return ary
}

ar1=[4,3,2,1]
console.log(bubbleSort(ar1)) //[1,2,3,4]
```

