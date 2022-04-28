#include <Servo.h> // Servo Library
#include <Stepper.h> // Stepper Library 

//control
bool pinChange = 1; // pin that changes sequence
int pinSET = 0; // active pin set
bool pinNEW = 0;// detect change in pin
int pinUp = 0; //up direction
int pinDown = 0; // down direction
int servo_rotation = 90; // servo rotation variable
int serv1_pos = 90; // servo 1 position
int serv2_pos = 90; // servo 2 position
int serv3_pos = 90; // servo 3 position

//switch
int switc = 4; // switch change
int switu = 3; // switch up
int switd = 2; // switch down

//motor
Stepper myStepper = Stepper(200, 7, 8);

// servo
int serv1 = 9; // servo 1 variable
int serv2 = 10; // servo 2 variable
int serv3 = 11; // servo 3 variable

Servo Servo1; // servo 1 controller
Servo Servo2; // servo 2 controller
Servo Servo3; // servo 3 controller

void setup() {

  Serial.begin(9600); //serial monitor


  //switches
  pinMode(switc, INPUT_PULLUP); // pin change
  pinMode(switu, INPUT_PULLUP); // pin up
  pinMode(switd, INPUT_PULLUP); //pin down

  // H bridge
  myStepper.setSpeed(100);

  //servos
  Servo1.attach(serv1); // congfig servo pin
  Servo2.attach(serv2);  // congfig servo pin
  Servo3.attach(serv3); // congfig servo pin

}

void loop() {


  pinChange = digitalRead(switc); // controller pin change

  pinUp = digitalRead(switu); // controller pin up
  pinDown = digitalRead(switd); // controller pin down

  if (pinSET > 3) // if pin set is greater than 3, pin set resets
  {
    pinSET = 0; // pin set = 0
  }

  if (pinChange == 0 && pinNEW == 0) // if pin change
  {
    if (pinSET == 1)
    {
      serv1_pos = servo_rotation; //save rotation servo 1
      servo_rotation = serv2_pos; // change to selected servo position
    }
    if (pinSET == 2)
    {
      serv2_pos = servo_rotation; //save rotation servo 2
      servo_rotation = serv3_pos; // change to selected servo position
    }
    if (pinSET == 3)
    {
      serv3_pos = servo_rotation; //save rotation servo 3
      servo_rotation = serv1_pos; // change to selected servo position
    }

    pinSET ++; // increment pin set
    pinNEW = 1; // pin active
    delay(1000);
    pinNEW = 0; // pin deactive

  }

  if (pinUp > 0 && servo_rotation < 180 && pinSET != 0)
  {
    servo_rotation ++; // if pin set servo, if rotation under 180 degrees and pin up pressed, increase rotation
  }

  if (pinDown > 0 && servo_rotation > 0 && pinSET != 0)
  {
    servo_rotation --; // if pin set servo, if rotation greater than 0 degrees and pin down pressed, decrease rotation
  }

  if (pinSET == 0 && pinUp > 0) // if pin set motor up rotation through H bridge
  {
    myStepper.step(200);
  }

  if (pinSET == 0 && pinUp > 0) // if pin set motor down rotation through H bridge
  {
    myStepper.step(-200);
  }


  if (pinSET == 1)  // pin set 1 is first servo
  {
    Servo1.write(servo_rotation);
  }

  if (pinSET == 2) // pin set 2 is second servo
  {
    Servo2.write(servo_rotation);
  }

  if (pinSET == 3) // pin set 3 is third servo
  {
    Servo3.write(servo_rotation);
  }


  //prints
  delay(1000);
  Serial.println("Pin Selected:");
  Serial.println(pinSET);
  Serial.println("Pin Change Trigger:");
  Serial.println(pinChange);
  Serial.println("Pin Up Trigger:");
  Serial.println(pinUp);
  Serial.println("Pin Down Trigger:");
  Serial.println(pinDown);
  Serial.println("Servo Rotation Value:");
  Serial.println(servo_rotation);
}
