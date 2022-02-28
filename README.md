<p align="center">
  <b> Tic Tac Toe Delta Robot Arm</b><br>
  <a>Logan & Cole</a>
</p>

---
## Table of Contents
* [Introduction & Description](#Introduction)
* [Materials](#Materials)
* [Links & Documents](#Links)
* [CAD Renders](#Cad-Renders)
* [Problems we ran into](#Problems-we-ran-into)
* [Code](#Code)

---
### Introduction
#### Hey there, this is the repository for a 2-player Delta Robot Arm driven Tic-Tac-Toe game by Logan and Cole. 

##### The 1st player presses one of the buttons on the 9 button panel, press a button twice to accept a move, and the Delta Robot Arm will move the playing pieces were they need to go. After that, the 2nd player will select were they want to go. 

###### ***Our schedule for this entire process was to do as much work we could in class and go to BKT, a free period, when we were able to.***
---

https://user-images.githubusercontent.com/71342159/155556728-a68f3392-b6fa-4784-8c2e-a824cd14f5ab.mp4

---
### Materials
- Acrylic
- 9 panel mounted buttons
- 1 Arduino Metro board
- 1 breadboard
- 3 servos
- 9 resistors ( 10k )
- A ton of wires
- A computer to connect the metro to via USB
- Laser cutter & 3D Printer 

<img src="https://github.com/Logan-Martin/Tic-Tac-Toe-Delta-Robot-Arm/blob/main/Photos/TicTacToeDeltaArmWiring.png"> 


---
### Links
[Planning Document](https://docs.google.com/document/d/18HwzTXXG70VNSVvcM3PhlL8kFNCUQtPwDOm3BRKYQW8/edit?usp=sharing)

[Cad - OnShape Document](https://cvilleschools.onshape.com/documents/b6c0dc8ca74cd78e4cfe3490/w/83d6d21bc676c767c3550309/e/f627081b1e1d9558a92df4c4?renderMode=0&uiState=6214f43c3508af00f0f56b9e)

---

### Cad Renders

<img src="https://github.com/Logan-Martin/Tic-Tac-Toe-Delta-Robot-Arm/blob/main/Photos/Arm_Photo.PNG">
One of the three arms used to make the full delta arm assembly in CAD

<img align="right" src="https://github.com/Logan-Martin/Tic-Tac-Toe-Delta-Robot-Arm/blob/main/Photos/Full_Arm_Assembly.PNG"> 
the full delta arm assembly desgined in CAD
<img src="https://github.com/Logan-Martin/Tic-Tac-Toe-Delta-Robot-Arm/blob/main/Photos/DeltaArmTicTacToeButtonBox.jpg"> 

---

### Problems we ran into

1. We didn't really know how a delta arm worked. YouTube and Google were helpful, but the math behind it all was too confusing. Thus we tried looking for someones code on a delta arm for Arduino. This leads to our second issue.
2. How do we even code this thing? We eventually got to [this](https://github.com/deltarobotone/one_system_library), a library for a Arduino Delta arm. However this was not a 100% solution. The code that was in the background making everything possible was far too complex for us change.
3. How are we going to pick up and place tic tac toe pieces? We chose to use magnets. This means that we need a way to magnitize and un-magnitize an area on the delta arm so we can pick things up. We need to 3D print the pieces and stop the process about half way through so we can fit a manget inside. This seems easy to do, but 3D printing takes time and that is not exactly something we a have a ton of.
4. Are we going to have the tic tac toe board be cleared when the game is over? How will the robot arm knows who wins and when they win? Why did we even make this robot? Existentialism aside, these problems can only we be solved if we have enough time. Ideally I would love the board to clear itself, but that again will take time.

---

### Code

<details><summary>Click for Code.</summary>
<p>

```
#include <Servo.h>

// these are the buttons for moving the robot arm. Totally didn't re-write the names 3+ times because I forgot how to spell button.
int button1 = 10;
int button2 = 2;
int button3 = 3;
int button4 = 4;
int button5 = 5;
int button6 = 6;
int button7 = 7;
int button8 = 8;
int button9 = 9;

int PowerButton = 1; // may or not use
int LCDScreen = 2; // may or not use

Servo servo1;
Servo servo2;
Servo servo3;

int posForFirstServo = 0; // variable to store the servo position
int posForSecondServo = 0;
int posForThirdServo = 0;

bool hasButton1AlreadyBeenPressed = false; // this is to make a button press be well a button press
bool hasButton2AlreadyBeenPressed = false;
bool hasButton3AlreadyBeenPressed = false;
bool hasButton4AlreadyBeenPressed = false;
bool hasButton5AlreadyBeenPressed = false;
bool hasButton6AlreadyBeenPressed = false;
bool hasButton7AlreadyBeenPressed = false;
bool hasButton8AlreadyBeenPressed = false;
bool hasButton9AlreadyBeenPressed = false;

bool hasButton1BeenPressedOnce = false; // after pressing a button twice, the position of the delta arm will move
bool hasButton2BeenPressedOnce = false;
bool hasButton3BeenPressedOnce = false;
bool hasButton4BeenPressedOnce = false;
bool hasButton5BeenPressedOnce = false;
bool hasButton6BeenPressedOnce = false;
bool hasButton7BeenPressedOnce = false;
bool hasButton8BeenPressedOnce = false;
bool hasButton9BeenPressedOnce = false;



void setup() {
  Serial.begin(9600);
  
  // this makes it so I can get inputs from things like a button
  pinMode(button1, INPUT);
  pinMode(button2, INPUT);
  pinMode(button3, INPUT);
  pinMode(button4, INPUT);
  pinMode(button5, INPUT);
  pinMode(button6, INPUT);
  pinMode(button7, INPUT);
  pinMode(button8, INPUT);
  pinMode(button9, INPUT);

  servo1.attach(11);
  servo2.attach(12);
  servo3.attach(13);

}

void moveRobotArm() {
  Serial.print("Testing:");
}

void loop() {
  // This is to read the pin values
  int buttonStateForButton1 = digitalRead(button1);
  int buttonStateForButton2 = digitalRead(button2);
  int buttonStateForButton3 = digitalRead(button3);
  int buttonStateForButton4 = digitalRead(button4);
  int buttonStateForButton5 = digitalRead(button5);
  int buttonStateForButton6 = digitalRead(button6);
  int buttonStateForButton7 = digitalRead(button7);
  int buttonStateForButton8 = digitalRead(button8);
  int buttonStateForButton9 = digitalRead(button9);
  delay(10);
  // check for when button is pressed
  if (buttonStateForButton1 == HIGH and hasButton1AlreadyBeenPressed == false) {
    if (hasButton1BeenPressedOnce == false) {
      hasButton1AlreadyBeenPressed = true;

      hasButton1BeenPressedOnce = true;
      hasButton2BeenPressedOnce = false;
      hasButton3BeenPressedOnce = false;
      hasButton4BeenPressedOnce = false;
      hasButton5BeenPressedOnce = false;
      hasButton6BeenPressedOnce = false;
      hasButton7BeenPressedOnce = false;
      hasButton8BeenPressedOnce = false;
      hasButton9BeenPressedOnce = false;

      Serial.print("Button 1 Pressed!");
    }
    else if (hasButton1BeenPressedOnce == true) {
      hasButton1AlreadyBeenPressed = true;
      hasButton1BeenPressedOnce = false;
      Serial.print("Button 1 was press twice!");
      
      servo1.write(0);
      servo2.write(0);
      servo3.write(0);
      
    while (posForFirstServo < 180) {
      delay(10);
      if (posForFirstServo == 90)
        {
          Serial.print("NICE!");
          posForFirstServo = posForFirstServo + 1;
          servo1.write(posForFirstServo);
          break;
        }
        else
        {
          posForFirstServo = posForFirstServo + 1;
          servo1.write(posForFirstServo);
        }
      }
    }
  }
  else if (buttonStateForButton1 == LOW and hasButton1AlreadyBeenPressed == true) {
    hasButton1AlreadyBeenPressed = false;
    // Serial.print("Able to press any button again!");
  }


  if (buttonStateForButton2 == HIGH and hasButton2AlreadyBeenPressed == false) {
    if (hasButton2BeenPressedOnce == false) {

      hasButton2AlreadyBeenPressed = true;
      hasButton1BeenPressedOnce = false;
      hasButton2BeenPressedOnce = true;
      hasButton3BeenPressedOnce = false;
      hasButton4BeenPressedOnce = false;
      hasButton5BeenPressedOnce = false;
      hasButton6BeenPressedOnce = false;
      hasButton7BeenPressedOnce = false;
      hasButton8BeenPressedOnce = false;
      hasButton9BeenPressedOnce = false;

      Serial.print("Button 2 Pressed!");
    }
    else if (hasButton2BeenPressedOnce == true) {
      hasButton2AlreadyBeenPressed = true;
      hasButton2BeenPressedOnce = false;
      Serial.print("Button 2 was press twice!");
      servo1.write(10);
      servo2.write(10);
      servo3.write(10);
      
      posForFirstServo = 0;
    }
  }
  else if (buttonStateForButton2 == LOW and hasButton2AlreadyBeenPressed == true) {
    hasButton2AlreadyBeenPressed = false;
  }

  if (buttonStateForButton3 == HIGH and hasButton3AlreadyBeenPressed == false) {
    if (hasButton3BeenPressedOnce == false) {
      hasButton3AlreadyBeenPressed = true;

      hasButton1BeenPressedOnce = false;
      hasButton2BeenPressedOnce = false;
      hasButton3BeenPressedOnce = true;
      hasButton4BeenPressedOnce = false;
      hasButton5BeenPressedOnce = false;
      hasButton6BeenPressedOnce = false;
      hasButton7BeenPressedOnce = false;
      hasButton8BeenPressedOnce = false;
      hasButton9BeenPressedOnce = false;

      Serial.print("Button 3 Pressed!");
    }
    else if (hasButton3BeenPressedOnce == true) {
      hasButton3AlreadyBeenPressed = true;
      hasButton3BeenPressedOnce = false;
      Serial.print("Button 3 was press twice!");
      servo1.write(20);
      servo2.write(20);
      servo3.write(20);
    }
  }
  else if (buttonStateForButton3 == LOW and hasButton3AlreadyBeenPressed == true) {
    hasButton3AlreadyBeenPressed = false;
  }


  if (buttonStateForButton4 == HIGH and hasButton4AlreadyBeenPressed == false) {
    if (hasButton4BeenPressedOnce == false) {
      hasButton4AlreadyBeenPressed = true;

      hasButton1BeenPressedOnce = false;
      hasButton2BeenPressedOnce = false;
      hasButton3BeenPressedOnce = false;
      hasButton4BeenPressedOnce = true;
      hasButton5BeenPressedOnce = false;
      hasButton6BeenPressedOnce = false;
      hasButton7BeenPressedOnce = false;
      hasButton8BeenPressedOnce = false;
      hasButton9BeenPressedOnce = false;

      Serial.print("Button 4 Pressed!");
    }
    else if (hasButton4BeenPressedOnce == true) {
      hasButton4AlreadyBeenPressed = true;
      hasButton4BeenPressedOnce = false;
      Serial.print("Button 4 was press twice!");
      servo1.write(30);
      servo2.write(30);
      servo3.write(30);
    }
  }
  else if (buttonStateForButton4 == LOW and hasButton4AlreadyBeenPressed == true) {
    hasButton4AlreadyBeenPressed = false;
  }


  if (buttonStateForButton5 == HIGH and hasButton5AlreadyBeenPressed == false) {
    if (hasButton5BeenPressedOnce == false) {
      hasButton5AlreadyBeenPressed = true;

      hasButton1BeenPressedOnce = false;
      hasButton2BeenPressedOnce = false;
      hasButton3BeenPressedOnce = false;
      hasButton4BeenPressedOnce = false;
      hasButton5BeenPressedOnce = true;
      hasButton6BeenPressedOnce = false;
      hasButton7BeenPressedOnce = false;
      hasButton8BeenPressedOnce = false;
      hasButton9BeenPressedOnce = false;

      Serial.print("Button 5 Pressed!");
    }
    else if (hasButton5BeenPressedOnce == true) {
      hasButton5AlreadyBeenPressed = true;
      hasButton5BeenPressedOnce = false;
      Serial.print("Button 5 was press twice!");
      servo1.write(40);
      servo2.write(40);
      servo3.write(40);
    }
  }
  else if (buttonStateForButton5 == LOW and hasButton5AlreadyBeenPressed == true) {
    hasButton5AlreadyBeenPressed = false;
  }


  if (buttonStateForButton6 == HIGH and hasButton6AlreadyBeenPressed == false) {
    if (hasButton6BeenPressedOnce == false) {
      hasButton6AlreadyBeenPressed = true;

      hasButton1BeenPressedOnce = false;
      hasButton2BeenPressedOnce = false;
      hasButton3BeenPressedOnce = false;
      hasButton4BeenPressedOnce = false;
      hasButton5BeenPressedOnce = false;
      hasButton6BeenPressedOnce = true;
      hasButton7BeenPressedOnce = false;
      hasButton8BeenPressedOnce = false;
      hasButton9BeenPressedOnce = false;

      Serial.print("Button 6 Pressed!");
    }
    else if (hasButton6BeenPressedOnce == true) {
      hasButton6AlreadyBeenPressed = true;
      hasButton6BeenPressedOnce = false;
      Serial.print("Button 6 was press twice!");
      servo1.write(50);
      servo2.write(50);
      servo3.write(50);
    }
  }
  else if (buttonStateForButton6 == LOW and hasButton6AlreadyBeenPressed == true) {
    hasButton6AlreadyBeenPressed = false;
  }


  if (buttonStateForButton7 == HIGH and hasButton7AlreadyBeenPressed == false) {
    if (hasButton7BeenPressedOnce == false) {
      hasButton7AlreadyBeenPressed = true;

      hasButton1BeenPressedOnce = false;
      hasButton2BeenPressedOnce = false;
      hasButton3BeenPressedOnce = false;
      hasButton4BeenPressedOnce = false;
      hasButton5BeenPressedOnce = false;
      hasButton6BeenPressedOnce = false;
      hasButton7BeenPressedOnce = true;
      hasButton8BeenPressedOnce = false;
      hasButton9BeenPressedOnce = false;

      Serial.print("Button 7 Pressed!");
    }
    else if (hasButton7BeenPressedOnce == true) {
      hasButton7AlreadyBeenPressed = true;
      hasButton7BeenPressedOnce = false;
      Serial.print("Button 7 was press twice!");
      servo1.write(60);
      servo2.write(60);
      servo3.write(60);
    }
  }
  else if (buttonStateForButton7 == LOW and hasButton7AlreadyBeenPressed == true) {
    hasButton7AlreadyBeenPressed = false;
  }


  if (buttonStateForButton8 == HIGH and hasButton8AlreadyBeenPressed == false) {
    if (hasButton8BeenPressedOnce == false) {
      hasButton8AlreadyBeenPressed = true;

      hasButton1BeenPressedOnce = false;
      hasButton2BeenPressedOnce = false;
      hasButton3BeenPressedOnce = false;
      hasButton4BeenPressedOnce = false;
      hasButton5BeenPressedOnce = false;
      hasButton6BeenPressedOnce = false;
      hasButton7BeenPressedOnce = false;
      hasButton8BeenPressedOnce = true;
      hasButton9BeenPressedOnce = false;

      Serial.print("Button 8 Pressed!");
    }
    else if (hasButton8BeenPressedOnce == true) {
      hasButton8AlreadyBeenPressed = true;
      hasButton8BeenPressedOnce = false;
      Serial.print("Button 8 was press twice!");
      servo1.write(70);
      servo2.write(70);
      servo3.write(70);
    }
  }
  else if (buttonStateForButton8 == LOW and hasButton8AlreadyBeenPressed == true) {
    hasButton8AlreadyBeenPressed = false;
  }


  if (buttonStateForButton9 == HIGH and hasButton9AlreadyBeenPressed == false) {
    if (hasButton9BeenPressedOnce == false) {
      hasButton9AlreadyBeenPressed = true;

      hasButton1BeenPressedOnce = false;
      hasButton2BeenPressedOnce = false;
      hasButton3BeenPressedOnce = false;
      hasButton4BeenPressedOnce = false;
      hasButton5BeenPressedOnce = false;
      hasButton6BeenPressedOnce = false;
      hasButton7BeenPressedOnce = false;
      hasButton8BeenPressedOnce = false;
      hasButton9BeenPressedOnce = true;

      Serial.print("Button 9 Pressed!");
    }
    else if (hasButton9BeenPressedOnce == true) {
      hasButton9AlreadyBeenPressed = true;
      hasButton9BeenPressedOnce = false;
      Serial.print("Button 9 was press twice!");
      servo1.write(90);
      servo2.write(90);
      servo3.write(90);
    }
  }
  else if (buttonStateForButton9 == LOW and hasButton9AlreadyBeenPressed == true) {
    hasButton9AlreadyBeenPressed = false;
  }

}
```
  
</p>
</details>



