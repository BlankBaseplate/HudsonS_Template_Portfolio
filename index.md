# Mini Tank Robot
Replace this text with a brief description (2-3 sentences) of your project. This description should draw the reader in and make them interested in what you've built. You can include what the biggest challenges, takeaways, and triumphs from completing the project were. As you complete your portfolio, remember your audience is less familiar than you are with all that your project entails!

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Hudson S | Westmont Highschool | Mechanical Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](HudsonS.heic)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/YkA2mTx3aO4?si=McGtIobe3QWB95xG" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

In this milestone I was able to connect the Mini Tank Robot to bluetooth. This allowed me to control the Mini Tank robot with my phone. This was due to me installing the bluetooth module onto the robot which allowed the robot to take inputs and perform output actions from my phone. The bluetooth module also helped display the distance of an object infront of the robot through the ultrasonic distance sensor and displaying it on an app on my phone. This project suprised me by me learning about new things at a relatively fast pace, as I didn't know how to connect Arduino components to bluetooth along with coding Arduino prior to the project. Before I reach my final milestone, I need to figure out what materials I want to use, along with where I want to place all of the components. My idea is to put rockets ontop of the Mini Tank Robot and have them launch and it may be challenging to find a way to fit everything and make sure everything works. 

Challenges faced
During this milestone I had trouble putting together the components. I had trouble finding out how to make the robot controllable via bluetooth, display a distance of an object infront of it, and also have the servomotor turn. I was able to figure out how to put the code together by using curly braces and putting the code into the voidloop or the voidsetup. However the actions were still being delayed due to some of the code being in seconds instead of milliseconds. I fixed this by making sure that all of the code used milliseconds instead of seconds to make all of the components respond to each other faster.

# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/0TFiV7wv_90?si=M8jecxFUCus5Npow" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

I built my Mini Tank Robot using tank treads, wheels, motors, a led lightboard, a battery pack, a Arduino Uno, and a battery pack. The Arduino Uno allowed me to code the robot using Arduino IDE (Integrated Development Environment). This code let the robot perform certain functions like moving forward, backward, left, and right. In addition to that it calculated the distance of the Mini Tank Robot from an object infront of it along with connect to bluetooth to be controlled by a mobile device. The LED lightboard displayed what function the robot was going through, for example whenever the robot was about to stop the LED lightboard displayed STOP, and when it was going forward it displayed a front arrow. The Motors helped drive the robot by moving the wheels and the treads. My plan to complete my project is to first build the full robot and test all the sensors using Arduino IDE and then connect it to bluetooth and add further modifications. 

Challenges faced
Some challenges I faced was trying to upload code to the Mini Tank Robot. I tried switching out the Arduino UNO, along with modifying my code to ensure that there weren't any errors. However, I realized that the problem was due to me having a bluetooth module connected to the Arduino. This bluetooth module prevents new code from being uploaded to the robot when its connected to the Arduino, and so I learned to remove it whenever uploading new code. Another challenge I faced was finding a way to power the robot without it being plugged into the laptop. Since we didn't have 18650 batteries that the Mini Tank Robot originally took, I had to improvise. I decided that I would connect the robot to a battery pack connected to a usb port instead of using batteries. 

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code

```c++
#include <IRremoteTank.h>
IRrecv irrecv(A0);  //set IRrecv irrecv to A0
decode_results results;
long ir_rec;  //save the IR value received

//Array, used to store the data of the pattern, can be calculated by yourself or obtained from the modulus tool
unsigned char start01[] = {0x01,0x02,0x04,0x08,0x10,0x20,0x40,0x80,0x80,0x40,0x20,0x10,0x08,0x04,0x02,0x01};
unsigned char front[] = {0x00,0x00,0x00,0x00,0x00,0x24,0x12,0x09,0x12,0x24,0x00,0x00,0x00,0x00,0x00,0x00};
unsigned char back[] = {0x00,0x00,0x00,0x00,0x00,0x24,0x48,0x90,0x48,0x24,0x00,0x00,0x00,0x00,0x00,0x00};
unsigned char left[] = {0x00,0x00,0x00,0x00,0x00,0x00,0x44,0x28,0x10,0x44,0x28,0x10,0x44,0x28,0x10,0x00};
unsigned char right[] = {0x00,0x10,0x28,0x44,0x10,0x28,0x44,0x10,0x28,0x44,0x00,0x00,0x00,0x00,0x00,0x00};
unsigned char STOP01[] = {0x2E,0x2A,0x3A,0x00,0x02,0x3E,0x02,0x00,0x3E,0x22,0x3E,0x00,0x3E,0x0A,0x0E,0x00};
unsigned char clear[] = {0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00,0x00};
#define SCL_Pin  A5  //Set clock pin to A5
#define SDA_Pin  A4  //Set data pin to A4

#define ML_Ctrl 13  //define the direction control pin of left motor
#define ML_PWM 11   //define PWM control pin of left motor
#define MR_Ctrl 12  //define the direction control pin of right motor
#define MR_PWM 3    //define PWM control pin of right motor

#define servoPin 9 //pin of servo
int pulsewidth; //save the pulse width value of servo

void setup(){
  Serial.begin(9600);
  irrecv.enableIRIn();  //Initialize the IR reception library
  
  pinMode(ML_Ctrl, OUTPUT);
  pinMode(ML_PWM, OUTPUT);
  pinMode(MR_Ctrl, OUTPUT);
  pinMode(MR_PWM, OUTPUT);
  
  pinMode(SCL_Pin,OUTPUT);
  pinMode(SDA_Pin,OUTPUT);
  matrix_display(clear); //Clear Screen
  matrix_display(start01);  //show start picture
  
  pinMode(servoPin, OUTPUT);
  procedure(90);  //Servo rotates to 90°
}

void loop(){
  if (irrecv.decode(&results)) //receive the IR remote value
  {
    ir_rec=results.value;
    String type="UNKNOWN";
    String typelist[14]={"UNKNOWN", "NEC", "SONY", "RC5", "RC6", "DISH", "SHARP", "PANASONIC", "JVC", "SANYO", "MITSUBISHI", "SAMSUNG", "LG", "WHYNTER"};
    if(results.decode_type>=1&&results.decode_type<=13){
      type=typelist[results.decode_type];
    }
    Serial.print("IR TYPE:"+type+"  ");
    Serial.println(ir_rec,HEX);
    irrecv.resume();
  }
  
  if (ir_rec == 0xFF629D) //Go forward
  {
    Car_front();
    matrix_display(front);  //Display front image
  }
  if (ir_rec == 0xFFA857)  //Robot car goes back
  {
    Car_back();
    matrix_display(front);  //Go back
  }
  if (ir_rec == 0xFF22DD)   //Robot car turns left
  {
    Car_T_left();
    matrix_display(left);  //Display left-turning image
  }
  if (ir_rec == 0xFFC23D)   //Robot car turns right
  {
    Car_T_right();
    matrix_display(right);  //Display right-turning image
  }
  if (ir_rec == 0xFF02FD)   //Robot car stops
  { 
    Car_Stop();
    matrix_display(STOP01);  //show stop image
  }
  if (ir_rec == 0xFF30CF)   //robot car rotates anticlockwise
  {
    Car_left();
    matrix_display(left);  //show anticlockwise rotation picture
  }
  if (ir_rec == 0xFF7A85)  //robot car rotates clockwise
  {
    Car_right();
    matrix_display(right);  //show clockwise rotation picture
 }
}
/******************Control Servo*******************/
void procedure(int myangle) {
  for (int i = 0; i <= 50; i = i + (1)) {
    pulsewidth = myangle * 11 + 500;
    digitalWrite(servoPin,HIGH);
    delayMicroseconds(pulsewidth);
    digitalWrite(servoPin,LOW);
    delay((20 - pulsewidth / 1000));
  }
}

/******************Dot Matrix****************/
// this function is used for dot matrix display 
void matrix_display(unsigned char matrix_value[])
{
  IIC_start();
  IIC_send(0xc0);  //Choose address
   for(int i = 0;i < 16;i++) //The picture has 16 bits
  {
     IIC_send(matrix_value[i]); //data to convey patterns
  }
  IIC_end();   //end to convey data pattern
  
  IIC_start();
  IIC_send(0x8A);  //display control, set pulse width to 4/16
  IIC_end();
}

//The condition starting to transmit data
void IIC_start()
{
  digitalWrite(SCL_Pin,HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin,HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin,LOW);
  delayMicroseconds(3);
}
//传输数据
void IIC_send(unsigned char send_data)
{
  for(char i = 0;i < 8;i++)  //Each byte has 8 bits 8bits for every character
  {
      digitalWrite(SCL_Pin,LOW);  //pull down clock pin SCL Pin to change the signals of SDA      
      delayMicroseconds(3);
      if(send_data & 0x01)  //set high and low level of SDA_Pin according to 1 or 0 of every bit
      {
        digitalWrite(SDA_Pin,HIGH);
      }
      else
      {
        digitalWrite(SDA_Pin,LOW);
      }
      delayMicroseconds(3);
      digitalWrite(SCL_Pin,HIGH); //pull up clock pin SCL_Pin to stop transmitting data
      delayMicroseconds(3);
      send_data = send_data >> 1;  // detect bit by bit, so move the data right by one
  }
}
//The sign that data transmission ends
void IIC_end()
{
  digitalWrite(SCL_Pin,LOW);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin,LOW);
  delayMicroseconds(3);
  digitalWrite(SCL_Pin,HIGH);
  delayMicroseconds(3);
  digitalWrite(SDA_Pin,HIGH);
  delayMicroseconds(3);
}
/***************the function to run motor***************/
void Car_front()
{
  digitalWrite(MR_Ctrl,LOW);
  analogWrite(MR_PWM,200);
  digitalWrite(ML_Ctrl,LOW);
  analogWrite(ML_PWM,200);
}
void Car_back()
{
  digitalWrite(MR_Ctrl,HIGH);
  analogWrite(MR_PWM,200);
  digitalWrite(ML_Ctrl,HIGH);
  analogWrite(ML_PWM,200);
}
void Car_left()
{
  digitalWrite(MR_Ctrl,LOW);
  analogWrite(MR_PWM,255);
  digitalWrite(ML_Ctrl,HIGH);
  analogWrite(ML_PWM,255);
}
void Car_right()
{
  digitalWrite(MR_Ctrl,HIGH);
  analogWrite(MR_PWM,255);
  digitalWrite(ML_Ctrl,LOW);
  analogWrite(ML_PWM,255);
}
void Car_Stop()
{
  digitalWrite(MR_Ctrl,LOW);
  analogWrite(MR_PWM,0);
  digitalWrite(ML_Ctrl,LOW);
  analogWrite(ML_PWM,0);
}
void Car_T_left()
{
  digitalWrite(MR_Ctrl,LOW);
  analogWrite(MR_PWM,255);
  digitalWrite(ML_Ctrl,LOW);
  analogWrite(ML_PWM,180);
}
void Car_T_right()
{
  digitalWrite(MR_Ctrl,LOW);
  analogWrite(MR_PWM,180);
  digitalWrite(ML_Ctrl,LOW);
  analogWrite(ML_PWM,255);
}
 //****************************************************************
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| KEYESTUDIO V4 Development Board | Allows for code to be transmitted to the robot via port | $Price | <a href="https://www.amazon.com/KEYESTUDIO-Development-Board-ATmega328P-Arduino/dp/B08H1RB61B"> Link </a> |
| L298P Shield | Allows for batteries to power the robot by inserting wires | $Price | <a href="https://www.google.com/aclk?sa=L&ai=DChsSEwj6sIeLisGVAxWwE60GHWxSJ4MYACICCAEQBBoCcHY&co=1&gclid=EAIaIQobChMI-rCHi4rBlQMVsBOtBh1sUieDEAAYASAAEgK_gvD_BwE&cid=CAAS0gHkaI9t3G9eO-qBgGXS-T6IfDKns0Pmhq55rPT3MTCsLtSr3x-cJCszuCY5eFyJ048kSZ0oM3nPY0EDbUFxGXR2_-YazfLF2XkHJkt-2gqyzMU46--e9Wy-bf2Vbk6J5BzrZ5wnE0TwDNs9uElPSozfxX0gMoe_q4eaSo-6a6slanRVIjjB9FFWo4GltL2aM-Z6gj22l2GjngP1JkKCzJ503cBpR8VrAWjYwUHlcRvZIsLIvSs8ycn3rVbpoeY5H4AcuhU_AFjMfVIVFnWAx1lQSwg&cce=1&sig=AOD64_11phkBZ3wNJClglIhWO2pMbiGdDQ&q&adurl&ved=2ahUKEwi_tIKLisGVAxUQNzQIHd5QDO4Q0Qx6BAgYEAE"> Link </a> |
| V5 Sensor Shield | Connects the HC-SR04 (ultrasonic distance sensor) and bluetooth module to the robot | $Price | <a href="https://www.walmart.com/ip/Sensor-Shield-V5-Digital-Analog-Expansion-Module-for-Arduino-UNO-R3-MEGA2560/288883962?wmlspartner=wlpa&selectedSellerId=101028229&adid=22222222227288883962_101028229_14069003552_202077872&wl0=&wl1=g&wl2=c&wl3=42423897272&wl4=pla-2449037643288&wl5=1027576&wl6=&wl7=&wl8=&wl9=pla&wl10=361337442&wl11=online&wl12=288883962_101028229&veh=sem&gad_source=4&gad_campaignid=202077872&gbraid=0AAAAADmfBIpsg6MzOve_MBYfy3C1ehjHd&gclid=EAIaIQobChMI6KyDwYrBlQMV2Q-tBh2CrRM3EAkYASABEgKxfPD_BwE"> Link </a> |
| HC-SR04 | Detects the distance of an object infront of the robot | $Price | <a href="https://www.walmart.com/ip/HC-SR04-Ultrasonic-Distance-Measuring-Transducer-Sensor-Module-for-Arduino/666164021?wmlspartner=wlpa&selectedSellerId=101028229&adid=22222222227666164021_101028229_14069003552_202077872&wl0=&wl1=g&wl2=c&wl3=42423897272&wl4=pla-2449037643288&wl5=1027576&wl6=&wl7=&wl8=&wl9=pla&wl10=361337442&wl11=online&wl12=666164021_101028229&veh=sem&gad_source=4&gad_campaignid=202077872&gbraid=0AAAAADmfBIpsg6MzOve_MBYfy3C1ehjHd&gclid=EAIaIQobChMItaCA7orBlQMV4gutBh0FYSvhEAkYAiABEgLVSfD_BwE"> Link </a> |
| HM-10 Bluetooth 4.0 Module | Allows the robot to be controlled through bluetooth | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/](https://store.arduino.cc/products/bluetooth-low-energy-4-0-module-hm-10"> Link </a> |
| Remote Control | Controls the robot by sending IR signals to the robot | $Price | <a href="https://www.keyestudio.com/products/keyestudio-ir-receiver-module-kitreceiver-moduleremote-controller3pin-f-m-dupont-line-for-arduino"> Link </a> |
| 8x16 LED Panel | Displays the action that the robot is about to perform | $Price | <a href="https://www.keyestudio.com/products/keyestudio-8x16-led-dot-matrix-board-with-ph-254-connector-4pin-cable-for-arduino"> Link </a> |
| IR Reciever Module Module | Recieves IR signals from the remote control and sends data to the robot so the remote control can control the robot | $Price | <a href="https://www.keyestudio.com/products/keyestudio-ir-receiver-module-kitreceiver-moduleremote-controller3pin-f-m-dupont-line-for-arduino"> Link </a> |
| Tank Driver Wheel | Drives the tank treads | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Caterpillar Band | Lets the robot drive on rough surfaces | $Price | <a href="https://www.amazon.com/Tracked-Caterpillar-Platform-Raspberry-Microbit/dp/B09V7CCDSV"> Link </a> |
| Metal Motor | Drives the wheels of the robot to let the robot move around | $Price | <a href="https://www.amazon.com/LVLOZ-GA25-310-Reduction-Miniature-Rotating/dp/B0BZ3MM5K2?th=1"> Link </a> |
| Screws and Nuts | Secures all of the parts of the robot | $Price | <a href="https://www.keyestudio.com/products/keyestudio-diy-mini-tank-v20-smart-robot-car-kit-for-arduino-stem"> Link </a> |
| Acrylic Pieces | Base of the robot and securing the LED board | $Price | <a href="https://www.keyestudio.com/products/keyestudio-diy-mini-tank-v20-smart-robot-car-kit-for-arduino-stem"> Link </a> |
| Battery Pack | Powers the robot | $Price | <a href="https://www.google.com/url?sa=t&source=web&rct=j&url=https%3A%2F%2Fwww.walmart.com%2Fip%2F20000-mAh-Portable-Charger-Power-Bank-Dual-USB-Battery-Pack-for-iPhone-iPad-Galaxy-Android-Pixel-and-Tablet-Black%2F3303493713&ved=0CBkQjhxqFwoTCNjmqNmNwZUDFQAAAAAdAAAAABA3&opi=89978449"> Link </a> |


# Starter Project

<iframe width="560" height="315" src="https://www.youtube.com/embed/gi7opj50VXs?si=p5391IpJNljBN9r4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

# Summary
For my starter project I chose the Retro Arcade Console. It had multiple gamemodes such as tetris, space invaders, and more. 

| **Part** | **Note** |
|:--:|:--:|
| Buzzer | Making noise/music in the retro arcade console | $Price | 
| PCB | Main circuit board of the retro arcade console, and is responsible for sending electricity through the console | 
| Buttons | The buttons allow the player to move and interact with the console | 
| Screws | Help secure the console together | 
| Acrylic shells | The casing of the console |
| Batteries | Provide power to the console | 

Most of these components besides the columns and the screws were soldered to the printed circuit board (PCB). This allowed the electric currents from the battery pack to flow through the solders and allow the Retro Arcade Console to function. 

# Challenges Faced
My main problem with this project was properly placing the solders. I kept running into the problem of having cold solders which meant that the solder wasnt melting enough as the iron kit wasn't hot enough. I fixed this by changing the tip of the ironing kit and also turning up the heat. I also made sure that I was cleaning off execess solder on the tip of the ironing kit by putting the tip in brass to clean it. Another challenege I faced was getting precise about the solder welds. This was a problem as the solder joints would be very close to each other and often times connecting to each other. I solved this by disconnecting them with the ironing kit by keeping the tip in the middle of the two connected joints. 

To watch the BSE tutorial on how to create a portfolio, click here.
