#include <Servo.h> // Servo Library
#include <Encoder.h>

Servo vertical; // Servo for vertical movement
int servo_pos = 90; // Servo position


// MOTOR INFORMATION //
// Motor setup
#define MOTA_PIN 5
#define MOTB_PIN 6

// Motor Speed
int motorSpeed = 20; //set motor speed

// Create encoder
Encoder myEnc(2,3); //define encoder pins

// Encoder change value / degree
int EncChange = 30; // Rev/deg


// PHOTORESISTORS //
int topLeftSensor = 1; // Top left sensor
int bottomLeftSensor = 2; // Bottom Left sensor
int topRightSensor = 3; // Top Right sensor
int bottomRightSensor = 4; // Bottom Right sensor

// SERVO MOTOR //
// Pin connection to servo motor
int servoPin = 9;


// DATA //
// Sensor values
int TLS; // Top Left Sensor
int BLS; // Bottom Left Sensor
int TRS; // Top Right Sensor
int BRS; // Bottom Right Sensor 

//Global avg sensor values
int avgTop; 
int avgBottom;
int avgLeft;
int avgRight;

long position = 0; // Encoder position

void setup() {
  Serial.begin(19200); //begin serial connection

  // Attach the servo motor
  vertical.attach(servoPin);

  // Setup motor pins
  pinMode(MOTA_PIN,OUTPUT);
  pinMode(MOTB_PIN,OUTPUT);

  // Set initial Servo position
  vertical.write(servo_pos);

  // Read encoder value
  position = myEnc.read();
  
  delay(1000); //one second delay
}

void loop() {

  // Read photoresistors
  TLS = analogRead(topLeftSensor); // Top left sensor
  BLS = analogRead(bottomLeftSensor); // Bottom left sensor
  TRS = analogRead(topRightSensor); // Top right sensor
  BRS = analogRead(bottomRightSensor); // Bottom Right sensor

  // Print to serial terminal
  Serial.print("TL: "); Serial.println(TLS);
  Serial.print("BL: "); Serial.println(BLS);
  Serial.print("TR: "); Serial.println(TRS);
  Serial.print("BR: "); Serial.println(BRS);

  // Calculate the avg values
  avgTop = (TLS + TRS) / 2; 
  avgBottom = (BLS + BRS) / 2; 
  avgRight = (TRS + BRS) / 2;
  avgLeft = (TLS + BLS) / 2; 

  //print averages
  Serial.print("AvgTop: "); Serial.println(avgTop);
  Serial.print("AvgBottom: "); Serial.println(avgBottom);
  Serial.print("AvgRight: "); Serial.println(avgRight);
  Serial.print("AvgLeft: "); Serial.println(avgLeft);

  // Servo position
  Serial.print("Servo Position: "); Serial.println(servo_pos);

  // SERVO //
  // Check to see if change between top and bottom avg values

  if (abs(avgTop-avgBottom)<50)
  {
   
  }
  else if (avgTop < avgBottom ) // Move up
  {
    // Increase servo position by 1 degree
    servo_pos=servo_pos-1;

    if (servo_pos < 30)
    {
      // Set the max limit for servo
      servo_pos = 30;
    }
    vertical.write(servo_pos); //move servo
    delay(40); //40 ms delay
  }
  else if (avgBottom < avgTop ) // Move down
  {
    // Decrease servo by 1 degree
    servo_pos=servo_pos+1;

    if (servo_pos > 120)
    {
      // Set the min limit for servo
      servo_pos = 120; 
    }
    vertical.write(servo_pos); //move servo
    delay(40); //40ms delay
  }

  // MOTOR //
  if(abs(avgLeft-avgRight)<70) //compares left and right avg

 {
  digitalWrite(6,LOW); //turns motor off
  digitalWrite(5,LOW); 
  }
  
  else if (avgLeft < avgRight) //Move counter clock wise
  {
  analogWrite(6,140); 
  digitalWrite(5,LOW); 

  delay(40); //40 ms delay
  }
  
  else if (avgRight < avgLeft) // Move Clockwise
  {
  digitalWrite(6,LOW); 
  analogWrite(5,140); 

  delay(40); //40 ms delay
  }

 else
 {

 digitalWrite(6,LOW); //stop motor
 digitalWrite(5,LOW); 

  }
}
