## Hello, world!
```c
#include <stdio.h>
void main(){
	printf("Hello, World");
}
```

## Data Types
```c
// Data Types
int x = 10;
float y = 1.10;
double z = 1.11;
char a = 'a';
char* s = "Hello, World!";
char st[] = "Hello, World!";

const int x = 10;
```

## Print Statement
```c
// Print Statement
printf("Hello, World!");
printf("%d",x);
printf("%f",y);
printf("%lf",z);
prinft("%c",a);
printf("%s",s);

printf("%lu",sizeof(x));
printf("%.1f",y);
```

## Type Conversion
```c
// Type Conversion
int a = 9.99 // a=9
float b = 9 // a=9.00
float c = 5/2 // a=2
float d = (float)5/2 // a=2.50
```

## Const Variable
```c
// Constant
const int YEAR = 2003; // UPPERCASE for const best practice
int year = 2003;
```

## Logical Operator
```c
// Logical Operator
// and &&
// or ||
// not !
```

## Boolean
```c
#include 'stdio.h'
#include 'stdbool.h'

int main(){
	bool checkout=true;
	printf("%d",checkout);
	return 0;
}
```

## Conditional Statement
```c
// Conditional Statements
#include <stdio.h>
#include <stdbool.h>
int main(){
	bool pass=true;
	bool pass1=true;
	if (pass){
		printf("Pass");
	}
	else if(pass1){
		printf("Pass1");
	}
	else{
		prinf("Fail");
	}

	int time = 20;  
	(time < 18) ? printf("Good day.") : printf("Good evening.");
	return 0;
}
```

## Switch Case
```c
// Swtich Case
int day = 4;

switch (day) {
  case 1:
    printf("Monday");
    break;
  case 2:
    printf("Tuesday");
    break;
  case 3:
    printf("Wednesday");
    break;
  case 4:
    printf("Thursday");
    break;
  case 5:
    printf("Friday");
    break;
  case 6:
    printf("Saturday");
    break;
  case 7:
    printf("Sunday");
    break;
}
```

## While Loop
```c
// While Loop
#include <stdio.h>
int main(){
	int n=10;
	while (n>=0){
		printf("%d",n);
		n--;
	}

// Do/While Loop
	int i = 0;
	do {
	  printf("%d\n", i);
	  i++;
	}
	while (i < 5);
	return 0;
}
```

## For Loop
```c
#include <stdio.h>
int main(){
	for (int i=0;i<=5;i++){
		printf("%d",i);
	}
	return 0;
}
```

## Array
```c
#include <stdio.h>
int main(){
	int ary[]={1,2,3,4,5};
	printf("%d",ary[0]);
	return 0;
}
```

## String
```c
#include <stdio.h>
int main(){
	char greet1[] = "Hello World!";
	char greet2[] = {'H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd', '!', '\0'};
	// \0 is null terminating char for this method (need to be added)

	printf("%s\n",greet1);
	printf("%s\n",greet2);

	printf("%lu\n",sizeof(greet1)); // 12+1=13 (include '\0')
	printf("%lu\n",sizeof(greet2)); // 13

	char specialStr[]="\"Hello, world!\"";
	printf("%s",specialStr);
	return 0;
}
```

## String Fucntions

```c
#include <stdio.h>
#include <string.h>

int main(){
	char vowels[10]="aeiou";
	printf("%lu\n",strlen(vowels)); // 5
	printf("%lu\n",sizeof(vowels)); // 10

	char str1[20] = "Hello ";
	char str2[] = "World!";

	// Concatenate str2 to str1 (result is stored in str1)
	strcat(str1, str2);

	// Print str1
	printf("%s\n", str1);
	printf("%lu\n",strlen(str1));
	printf("%lu\n",sizeof(str1));
	printf("%lu\n",sizeof(str2));


	char sstr1[20] = "Hello World!";
	char sstr2[20];

	// Copy sstr1 to str2
	strcpy(sstr2, sstr1);

	// Print str2
	printf("%s", sstr2);


	char strr1[] = "Hello";
	char strr2[] = "Hello";
	char strr3[] = "Hi";

	// Compare strr1 and strr2, and print the result
	printf("%d\n", strcmp(strr1, strr2));  // Returns 0 (the strings are equal)

	// Compare str1 and str3, and print the result
	printf("%d\n", strcmp(strr1, strr3));  // Returns -4 (the strings are not equal)
	return 0;
}
```

## Taking Input

```c
#include <stdio.h>
#include <string.h>

int main() {
    int intVal;
    float floatVal;
    double doubleVal;
    long longVal;
    char charVal;
    char wordStr[50];
    char lineStr[100];

    // Integer input
    printf("Enter an integer: ");
    scanf("%d", &intVal);

    // Float input
    printf("Enter a float: ");
    scanf("%f", &floatVal);

    // Double input
    printf("Enter a double: ");
    scanf("%lf", &doubleVal);

    // Long input
    printf("Enter a long: ");
    scanf("%ld", &longVal);

    // Char input
    printf("Enter a character: ");
    scanf(" %c", &charVal);  // space before %c to skip leftover newline

    // String input (single word) using scanf
    printf("Enter a single word string: ");
    scanf("%s", wordStr);

    // Clear newline before using fgets
    getchar();

    // String input (line with spaces) using fgets
    printf("Enter a full line string (with spaces): ");
    fgets(lineStr, sizeof(lineStr), stdin);

    // Remove newline character from fgets if present
    lineStr[strcspn(lineStr, "\n")] = '\0';

    // Output all values
    printf("\nYou entered:\n");
    printf("Integer: %d\n", intVal);
    printf("Float: %.2f\n", floatVal);
    printf("Double: %.2lf\n", doubleVal);
    printf("Long: %ld\n", longVal);
    printf("Character: %c\n", charVal);
    printf("Single word string: %s\n", wordStr);
    printf("Line string: %s\n", lineStr);

    return 0;
}
```

## Memory Address
```c
int myAge = 43;
printf("%p", &myAge); // Outputs 0x7ffe5367e044
```

## Pointer
```c
int myAge = 43;     // An int variable
int* ptr = &myAge;  // A pointer variable, with the name ptr, that stores the address of myAge

// Output the value of myAge (43)
printf("%d\n", myAge);

// Output the memory address of myAge (0x7ffe5367e044)
printf("%p\n", &myAge);

// Output the memory address of myAge with the pointer (0x7ffe5367e044)
printf("%p\n", ptr);
```

## Array with Ptr
```c
int myNumbers[4] = {25, 50, 75, 100};

// Change the value of the first element to 13
*myNumbers = 13;

// Change the value of the second element to 17
*(myNumbers +1) = 17;

// Get the value of the first element
printf("%d\n", *myNumbers);

// Get the value of the second element
printf("%d\n", *(myNumbers + 1));
```

## Function
```c
#include <stdio.h>

void calculateSum() {
  int x = 5;
  int y = 10;
  int sum = x + y;
  printf("The sum of x + y is: %d", sum);
}

int main() {
  calculateSum();  // call the function
  return 0;
}
void calculateSum() {
  int x = 5;
  int y = 10;
  int sum = x + y;
  printf("The sum of x + y is: %d", sum);
}

// Outputs The sum of x + y is: 15
```

```c
#include <stdio.h>

void myFunction(char name[]) {
  printf("Hello %s\n", name);
}

int main() {
  myFunction("Liam");
  myFunction("Jenny");
  myFunction("Anja");
  return 0;
}

// Hello Liam
// Hello Jenny
// Hello Anja
```

## Scope

```c
#include <stdio.h>
// Global variable
int x = 5;

void myFunction() {
  printf("%d\n", ++x); // Increment the value of x by 1 and print it
}

int main() {
  myFunction();

  printf("%d\n", x); // Print the global variable x
  return 0;
}

// The value of x is now 6 (no longer 5)
```

## Function Declaration
```c
#include <stdio.h>
// Function declaration
void myFunction();

// The main method
int main() {
  myFunction();  // call the function
  return 0;
}

// Function definition
void myFunction() {
  printf("I just got executed!");
}
```

```c
// Declare two functions, myFunction and myOtherFunction
#include <stdio.h>
void myFunction();
void myOtherFunction();

int main() {
  myFunction(); // call myFunction (from main)
  return 0;
}

// Define myFunction
void myFunction() {
  printf("Some text in myFunction\n");
  myOtherFunction(); // call myOtherFunction (from myFunction)
}

// Define myOtherFunction
void myOtherFunction() {
  printf("Hey! Some text in myOtherFunction\n");
}
```


## Math.h
```c
#include <stdio.h>
#include <math.h>

int main(){
    printf("%.2f\n",pow(2,4));
    printf("%.2f\n",sqrt(4));
    printf("%f",ceil(2.1));
    printf("%f",floor(2.9));
    return 0;
}
```

## File - r,w,a
```c
#include <stdio.h>

int main(){
    FILE* fptr;

    fptr=fopen("log.txt","w");
    fprintf(fptr,"Hello, World!");
    fclose(fptr);

    fptr=fopen("log.txt","a");
    fprintf(fptr,"\nI am C");
    fclose(fptr);

    char file_content[100];
    fptr=fopen("log.txt","r");
    while(fgets(file_content,100,fptr)){
        printf("%s",file_content);
    }
    fclose(fptr);
    return 0;
}
```

## Struct
```c
#include <stdio.h>
#include <string.h>

struct myStructure {
  int myNum;
  char myLetter;
  char myString[30];
};

int main() {
  // Create a structure variable and assign values to it
  struct myStructure s1 = {13, 'B', "Some text"};

  // Modify values
  s1.myNum = 30;
  s1.myLetter = 'C';
  strcpy(s1.myString, "Something else");

  // Print values
  printf("%d %c %s\n", s1.myNum, s1.myLetter, s1.myString);
  
  struct myStructure s2;
  s2=s1;
  strcpy(s2.myString,"s2 text");
  printf("%d %c %s\n", s2.myNum, s2.myLetter, s2.myString);
  printf("%d %c %s\n", s1.myNum, s1.myLetter, s1.myString);
  

  return 0;
}
```

## enum
```c
#include <stdio.h>
enum Level {
  LOW = 1,
  MEDIUM,
  HIGH
};

int main() {
  enum Level myVar = MEDIUM;

  switch (myVar) {
    case 1:
      printf("Low Level");
      break;
    case 2:
      printf("Medium level");
      break;
    case 3:
      printf("High level");
      break;
  }
  return 0;
}
```