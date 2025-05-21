Robotic Arm
========================

## References
Link: https://youtu.be/5toNqaGsGYs

## Rotary Encoder and Stepper Motor with LCD
```c
#include <LiquidCrystal.h> // includes the LiquidCrystal Library 
LiquidCrystal lcd(1, 2, 4, 5, 6, 7); // Creates an LC object. Parameters: (rs, enable, d4, d5, d6, d7) 

// defines pins numbers
 #define stepPin 8 
 #define dirPin  9
 #define outputA 10
 #define outputB 11

 int counter = 0;
 int angle = 0; 
 int aState;
 int aLastState;  
 
void setup() {
  // Sets the two pins as Outputs
  pinMode(stepPin,OUTPUT); 
  pinMode(dirPin,OUTPUT);
  pinMode (outputA,INPUT);
  pinMode (outputB,INPUT);
  
  aLastState = digitalRead(outputA);
  lcd.begin(16,2); // Initializes the interface to the LCD screen, and specifies the dimensions (width and height) of the display } 

}
void loop() {

  aState = digitalRead(outputA);
  
  if (aState != aLastState){     
     if (digitalRead(outputB) != aState) { 
       counter ++;
       angle ++;
       rotateCW();  
     }
     else {
       counter--;
       angle --;
       rotateCCW(); 
     }
     if (counter >=30 ) {
      counter =0;
     }
     
     lcd.clear();
     lcd.print("Position: ");
     lcd.print(int(angle*(-1.8)));
     lcd.print("deg"); 
     lcd.setCursor(0,0);
     
   }
  aLastState = aState;
}

void rotateCW() {
  digitalWrite(dirPin,LOW);
    digitalWrite(stepPin,HIGH);
    delayMicroseconds(2000);
    digitalWrite(stepPin,LOW);
    delayMicroseconds(2000); 
}
void rotateCCW() {
  digitalWrite(dirPin,HIGH);
    digitalWrite(stepPin,HIGH);
    delayMicroseconds(2000);
    digitalWrite(stepPin,LOW);
    delayMicroseconds(2000);   
}
```

## Encoder controlling the stepper
```c
/*
 * Arduino stepper motor control with rotary encoder.
 * This is a free software with NO WARRANTY.
 * https://simple-circuit.com/
 */

// include Arduino stepper motor library
#include <Stepper.h>

// number of steps per one revolution is 2048 ( = 4096 half steps)
#define STEPS  2048

// define stepper motor control pins
#define IN1  11
#define IN2  10
#define IN3   9
#define IN4   8

// initialize stepper library
Stepper stepper(STEPS, IN4, IN2, IN3, IN1);

int8_t  quad = 0;
uint8_t previous_data;

void setup()
{
  stepper.setSpeed(10);  // set stepper motor speed to 10 rpm

  // get rotary encoder state
  previous_data = digitalRead(A5) << 1 | digitalRead(A4);

  // pin change interrupt configuration
  PCICR  = 2;      // enable pin change interrupt for pins PCINT14..8 (Arduino A0 to A5)
  PCMSK1 = 0x30;   // enable pin change interrupt for pins PCINT12 & PCINT13 (Arduino A4 & A5)
}

ISR (PCINT1_vect)  // ISR for Arduino A4 (PCINT12) and A5 (PCINT13) pins
{
  uint8_t current_data = digitalRead(A5) << 1 | digitalRead(A4);

  if( current_data == previous_data )
    return;

  if( bitRead(current_data, 0) == bitRead(previous_data, 1) )
    quad -= 1;
  else
    quad += 1;
  previous_data = current_data;
}

int8_t encoder_update(void)
{
  int8_t val = 0;
  while(quad >= 4){
    val += 1;
    quad -= 4;
  }
  while(quad <= -4){
    val -= 1;
    quad += 4;
  }
  return val;
}

// main loop
void loop()
{
  int8_t stp = encoder_update();

  while(stp != 0)
  {
    int8_t dir = (stp > 0) ? -1 : 1;
    stepper.step( 20 * dir );
    stp += dir;
    stp += encoder_update();
  }

  digitalWrite(IN1, LOW);
  digitalWrite(IN2, LOW);
  digitalWrite(IN3, LOW);
  digitalWrite(IN4, LOW);

  delay(100);

}

// end of code.
```

## Stepper control Basic
```c
//Includes the Arduino Stepper Library
#include <Stepper.h>

// Defines the number of steps per rotation
const int stepsPerRevolution = 2038;

// Creates an instance of stepper class
// Pins entered in sequence IN1-IN3-IN2-IN4 for proper step sequence
Stepper myStepper = Stepper(stepsPerRevolution, 8, 10, 9, 11);

void setup() {
    // Nothing to do (Stepper Library sets pins as outputs)
}

void loop() {
	// Rotate CW slowly at 5 RPM
	myStepper.setSpeed(5);
	myStepper.step(stepsPerRevolution);
	delay(1000);
	
	// Rotate CCW quickly at 10 RPM
	myStepper.setSpeed(10);
	myStepper.step(-stepsPerRevolution);
	delay(1000);
}
```

# Encoder Basics
```c
// Rotary Encoder Inputs
#define CLK A5
#define DT A4

int counter = 0;
int currentStateCLK;
int lastStateCLK;
String currentDir ="";

void setup() {
        
	pinMode(CLK,INPUT);
	pinMode(DT,INPUT);

	Serial.begin(9600);

	// Read the initial state of CLK
	lastStateCLK = digitalRead(CLK);
}

void loop() {
        
	// Read the current state of CLK
	currentStateCLK = digitalRead(CLK);

	// If last and current state of CLK are different, then pulse occurred
	// React to only 1 state change to avoid double count
	if (currentStateCLK != lastStateCLK  && currentStateCLK == 1){

		// If the DT state is different than the CLK state then
		// the encoder is rotating CCW so decrement
		if (digitalRead(DT) != currentStateCLK) {
			counter --;
			currentDir ="CCW";
		} else {
			// Encoder is rotating CW so increment
			counter ++;
			currentDir ="CW";
		}

		Serial.println(counter);
	}

	// Remember last CLK state
	lastStateCLK = currentStateCLK;
}
```

# Checking 
```c
#include <Stepper.h>

const int stepsPerRevolution = 2038;
Stepper myStepper = Stepper(stepsPerRevolution, 8,10,9,11);

// Rotary Encoder Inputs
#define CLK A5
#define DT A4

int counter = 0;
int currentStateCLK;
int lastStateCLK;

void setup() {
        
	pinMode(CLK,INPUT);
	pinMode(DT,INPUT);

	Serial.begin(9600);

	// Read the initial state of CLK
	lastStateCLK = digitalRead(CLK);
}

void loop() {
        
	// Read the current state of CLK
	currentStateCLK = digitalRead(CLK);

	// If last and current state of CLK are different, then pulse occurred
	// React to only 1 state change to avoid double count
	if (currentStateCLK != lastStateCLK  && currentStateCLK == 1){

		// If the DT state is different than the CLK state then
		// the encoder is rotating CCW so decrement
		if (digitalRead(DT) != currentStateCLK) {
			counter --;
      myStepper.setSpeed(10);
      myStepper.step(stepsPerRevolution/20);

		} else {
			// Encoder is rotating CW so increment
			counter ++;
      myStepper.setSpeed(10);
      myStepper.step(-stepsPerRevolution/20);
		}

		Serial.println(counter);
	}

	// Remember last CLK state
	lastStateCLK = currentStateCLK;
}
```