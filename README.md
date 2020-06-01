# arduino.ps3controlled_bot
About how to control a Remote Controlled car using bluetooth PS3 controller

#include <PS3BT.h>
#include <usbhub.h>
#include <Servo.h>
// Satisfy the IDE, which needs to see the include statment in the ino too.

//#include <SPI.h>

USB Usb;
//USBHub Hub1(&Usb); // Some dongles have a hub inside

BTD Btd(&Usb); // You have to create the Bluetooth Dongle instance like so
/* You can create the instance of the class in two ways */
PS3BT PS3(&Btd); // This will just create the instance
//PS3BT PS3(&Btd, 0x00, 0x15, 0x83, 0x3D, 0x0A, 0x57); // This will also store the bluetooth address - this can be obtained from the dongle when running the sketch
Servo myservo;

int a = 3;
int a1 = 2;
int a2 = 4;
int b = 5;
int b1 = 7;
int b2 = 8;
//int c = 6;
int c1 = A0;
int c2 = A1;
//int d = 11;
int d1 = A2;
int d2 = A3;
//int servopin = 9;
int e1 = A4;
int e2 = A5;
int s1 = 0;
int s2 = 1;
void setup() {
  Serial.begin(115200);
#if !defined(__MIPSEL__)
  while (!Serial); // Wait for serial port to connect - used on Leonardo, Teensy and other boards with built-in USB CDC serial connection
#endif
  if (Usb.Init() == -1) {
    Serial.print(F("\r\nOSC did not start"));
    while (1); //halt
  }
  Serial.print(F("\r\nPS3 Bluetooth Library Started"));
  pinMode(a, OUTPUT);
  pinMode(a1, OUTPUT);
  pinMode(a2, OUTPUT);
  pinMode(b, OUTPUT);
  pinMode(b1, OUTPUT);
  pinMode(b2, OUTPUT);
  //pinMode(c, OUTPUT);
  pinMode(c1, OUTPUT);
  pinMode(c2, OUTPUT);
 // pinMode(d, OUTPUT);
  pinMode(d1, OUTPUT);
  pinMode(d2, OUTPUT);
  myservo.attach(6);
  pinMode(e1, OUTPUT);
  pinMode(e2, OUTPUT);
                                                                                                                                                                                                                      pinMode(s1, OUTPUT);
  pinMode(s2, OUTPUT);
}
void loop() 
{
  Usb.Task();
  
  int ly = PS3.getAnalogHat(LeftHatY); 
  int lx = PS3.getAnalogHat(LeftHatX);
  //int ry = PS3.getAnalogHat(RightHatY);
  int rx = PS3.getAnalogHat(RightHatX);
  
  int l2 = PS3.getAnalogButton(L2);
  int r2 = PS3.getAnalogButton(R2);
  
  
  if (PS3.PS3Connected || PS3.PS3NavigationConnected) {
     if(ly <= 120 && lx == 127 && rx == 127)
      {
          digitalWrite(a1, HIGH);                                     
          digitalWrite(a2, LOW);
          analogWrite(a, 255);
          digitalWrite(b2, HIGH);                                     
          digitalWrite(b1, LOW);
          analogWrite(b, 255); 
          digitalWrite(c2, LOW);                                     
          digitalWrite(c1, LOW);
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tFORWARD "));
            
      }
      if(ly >= 135 && lx == 127 && rx == 127)
      {
          digitalWrite(a2, HIGH);                                     
          digitalWrite(a1, LOW);
          analogWrite(a, 255);
          digitalWrite(b1, HIGH);                                     
          digitalWrite(b2, LOW);
          analogWrite(b, 255); 
          digitalWrite(c2, LOW);                                     
          digitalWrite(c1, LOW);
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tBACKWARD "));
            
      }
   if(ly == 127 && lx == 127 && rx == 127)
      {
          digitalWrite(a1, LOW);                                     
          digitalWrite(a2, LOW);
          analogWrite(a, 0);
          digitalWrite(b2, LOW);                                     
          digitalWrite(b1, LOW);
          analogWrite(b, 0); 
          digitalWrite(c2, LOW);                                     
          digitalWrite(c1, LOW);
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tREST "));
            
      }
    
       if(lx <= 120 && ly == 127 && rx == 127)
      {
          digitalWrite(a2, HIGH);                                     
          digitalWrite(a1, LOW);
          analogWrite(a, 127);
          digitalWrite(b2, HIGH);                                     
          digitalWrite(b1, LOW);
          analogWrite(b, 127); 
          digitalWrite(c1, HIGH);                                     
          digitalWrite(c2, LOW);
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tleft"));
            
      }
      if(lx >= 135 && ly == 127 && rx == 127)                            
      {
          digitalWrite(a1, HIGH);                                     
          digitalWrite(a2, LOW);
          analogWrite(a, 127);
          digitalWrite(b1, HIGH);                                     
          digitalWrite(b2, LOW);
          analogWrite(b, 127); 
          digitalWrite(c2, HIGH);                                     
          digitalWrite(c1, LOW);
          
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tright"));
            
      }
      if (lx == 0 && ly == 0 && rx == 127)                                                                                                                     
      {                                                       
          digitalWrite(a2, LOW);                                     
          digitalWrite(a1, LOW);
          analogWrite(a, 0);
          digitalWrite(b2, HIGH);                                     
          digitalWrite(b1, LOW);
          analogWrite(b, 255); 
          digitalWrite(c1, HIGH);                                     
          digitalWrite(c2, LOW);
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tForward left cross"));
      }
     if(lx == 255 && ly == 0 && rx == 127)
     {
          digitalWrite(a1, HIGH);                                     
          digitalWrite(a2, LOW);
          analogWrite(a, 255);
          digitalWrite(b1, LOW);                                     
          digitalWrite(b2, LOW);
          analogWrite(b, 0); 
          digitalWrite(c2, HIGH);                                     
          digitalWrite(c1, LOW);
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tForward right cross"));
     }
    if(lx == 255 && ly == 255 && rx == 127)
   {
          digitalWrite(a1, LOW);                                     
          digitalWrite(a2, LOW);
          analogWrite(a, 0);
          digitalWrite(b1, HIGH);                                     
          digitalWrite(b2, LOW);
          analogWrite(b, 255); 
          digitalWrite(c2, HIGH);                                     
          digitalWrite(c1, LOW);
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tBackward right cross"));
   }
    if(lx == 0 && ly == 255 && rx == 127)
    {
         
          digitalWrite(a2, HIGH);                                     
          digitalWrite(a1, LOW);
          analogWrite(a, 255);
          digitalWrite(b1, LOW);                                     
          digitalWrite(b2, LOW);
          analogWrite(b, 0); 
          digitalWrite(c1, HIGH);                                     
          digitalWrite(c2, LOW);
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tBackward left cross"));
    }
    if(rx <= 120 && ly == 127 && lx == 127)
    {
          digitalWrite(a2, HIGH);                                     
          digitalWrite(a1, LOW);
          analogWrite(a, 255);
          digitalWrite(b2, HIGH);                                     
          digitalWrite(b1, LOW);
          analogWrite(b, 255); 
          digitalWrite(c2, HIGH);                                     
          digitalWrite(c1, LOW);
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tANTICLOCKWISE LEFT"));
    }
     if(rx >= 135 && ly == 127 && lx == 127)
    {
          digitalWrite(a1, HIGH);                                     
          digitalWrite(a2, LOW);
          analogWrite(a, 255);
          digitalWrite(b1, HIGH);                                     
          digitalWrite(b2, LOW);
          analogWrite(b, 255); 
          digitalWrite(c1, HIGH);                                     
          digitalWrite(c2, LOW);
         // analogWrite(c, (127.5-r)*2); 
          //digitalWrite(d2, HIGH);                                     
          //digitalWrite(d1, LOW);
          //analogWrite(d, (127.5-r)*2);                          
          //Serial.println((127.5-r)*2); 
          Serial.print(F("\r\n\tCLOCKWISE right"));
    }
 if(ly <= 120 && lx >= 0)
{
  if(rx <= 120) 
  { 
  // For Motor A (left front)
  digitalWrite(a1, LOW);
  digitalWrite(a2, LOW);
  analogWrite(a, 0);
  // For Motor B (right front)
  digitalWrite(b1, LOW);
  digitalWrite(b2, HIGH);
  analogWrite(b, 255);
  // For Motor C (left back)
  digitalWrite(c1, LOW);
  digitalWrite(c2,HIGH);
 // analogWrite(c, 0);
  // For Motor D (right back)
  //digitalWrite(d1, LOW);
 // digitalWrite(d2, HIGH);
  //analogWrite(d, (127.5-r)*2);  
  Serial.print(F("\r\n\tpivotal Left"));
  }
}

  if(ly <= 120 && lx >= 0)
 {
  if(rx >= 135)
  {
  // For Motor A (left front)
  digitalWrite(a1, HIGH);
  digitalWrite(a2,LOW);
  analogWrite(a, 0);
  // For Motor B (right front)
  digitalWrite(b1, LOW);
  digitalWrite(b2, LOW);
  analogWrite(b, 0);
  // For Motor C (left back)
  digitalWrite(c1, HIGH);
  digitalWrite(c2, LOW);
  //analogWrite(c, (r-127.5)*2);
  // For Motor D (right back)
  //digitalWrite(d1, LOW);
  //digitalWrite(d2, LOW); 
 // analogWrite(d, (r-127.5)*2);
  Serial.print(F("\r\n\tpivotal right")); 
  }
}
   if(ly >=135 && lx >= 0)
{
  if(rx <= 120) 
  { 
  // For Motor A (left front)
  digitalWrite(a1, LOW);
  digitalWrite(a2, LOW);
  analogWrite(a, 0);
  // For Motor B (right front)
  digitalWrite(b2, LOW);
  digitalWrite(b1, HIGH);
  analogWrite(b, 255);
  // For Motor C (left back)
  digitalWrite(c2, LOW);
  digitalWrite(c1,HIGH);
 // analogWrite(c, 0);
  // For Motor D (right back)
  //digitalWrite(d1, LOW);
 // digitalWrite(d2, HIGH);
  //analogWrite(d, (127.5-r)*2);  
  Serial.print(F("\r\n\tclockwise backward"));
  }
}

  if(ly >=135 && lx >= 0)
 {
  if(rx >= 135)
  {
  // For Motor A (left front)
  digitalWrite(a2, HIGH);
  digitalWrite(a1,LOW);
  analogWrite(a, 0);
  // For Motor B (right front)
  digitalWrite(b1, LOW);
  digitalWrite(b2, LOW);
  analogWrite(b, 0);
  // For Motor C (left back)
  digitalWrite(c2, HIGH);
  digitalWrite(c1, LOW);
  //analogWrite(c, (r-127.5)*2);
  // For Motor D (right back)
  //digitalWrite(d1, LOW);
  //digitalWrite(d2, LOW); 
 // analogWrite(d, (r-127.5)*2);
  Serial.print(F("\r\n\tanticlockwise backward")); 
  }
}

/*if(l >= 135 && l2 == 0 && r2 == 0)
{
  if(r <= 117)
  {
  // For Motor A (left front)
  digitalWrite(a1, LOW);
  digitalWrite(a2,LOW);
  analogWrite(a, 0);
  // For Motor B (right front)
  digitalWrite(b1, HIGH);
  digitalWrite(b2, LOW);
  analogWrite(b, (127.5-r)*2);
  // For Motor C (left back)
  digitalWrite(c1, LOW);
  digitalWrite(c2, LOW);
  analogWrite(c, 0);
  // For Motor D (right back)
  digitalWrite(d1, HIGH);
  digitalWrite(d2, LOW);
  analogWrite(d, (127.5-r)*2);  
  Serial.print(F("\r\n\tBackward clockwise"));
  }
}

if(l >= 135 && l2 == 0 && r2 == 0)
{
  if(r >= 135)
  {
  // For Motor A (left front)
  digitalWrite(a1, LOW);
  digitalWrite(a2,HIGH);
  analogWrite(a, (r-127.5)*2);
  // For Motor B (right front)
  digitalWrite(b1, LOW);
  digitalWrite(b2, LOW);
  analogWrite(b, (r-127.5)*2);
  // For Motor C (left back)
  digitalWrite(c1, LOW);
  digitalWrite(c2, HIGH);
  analogWrite(c, (r-127.5)*2);
  // For Motor D (right back)
  digitalWrite(d1, LOW);
  digitalWrite(d2, LOW);
  analogWrite(d, (r-127.5)*2);
  Serial.print(F("\r\n\tBackward Anticlockwise"));  
  }
} */
    

    if (PS3.getButtonClick(PS)) {
      Serial.print(F("\r\nPS"));
      PS3.disconnect();
    }
    else {
      if (PS3.getButtonClick(TRIANGLE)) {
        // digitalWrite(s1, LOW);                                     
         //digitalWrite(s2, HIGH);
         myservo.write(0);
          digitalWrite(e1, HIGH);                                     
           digitalWrite(e2, LOW);
           delay(1100);
           digitalWrite(e1, LOW);                                     
           digitalWrite(e2, LOW);
           digitalWrite(d2, HIGH);                                     
           digitalWrite(d1, LOW);
          Serial.print(F("\r\n\tball in "));
        
         // digitalWrite(e1, LOW);                                     
         // digitalWrite(e2, LOW);
        
      }
      if (PS3.getButtonClick(CIRCLE)) {
        Serial.print(F("\r\n\tshoot"));
        digitalWrite(d1, HIGH);                                     
        digitalWrite(d2, LOW);
        //digitalWrite(s1, LOW);                                     
        //digitalWrite(s2, LOW);
        myservo.write(90);
        delay(1000);
        digitalWrite(d1, LOW);                                     
        digitalWrite(d2, LOW);
        
        }
      if (PS3.getButtonClick(CROSS))
      {
        digitalWrite(d1, LOW);                                     
        digitalWrite(d2, LOW);
        Serial.print(F("\r\n\tdribbler stopped"));
      }
      if (PS3.getButtonClick(SQUARE))
        Serial.print(F("\r\nSquare"));

      /*if (PS3.getButtonClick(UP)) {
        Serial.print(F("\r\nUp"));
        if (PS3.PS3Connected) {
          PS3.setLedOff();
          PS3.setLedOn(LED4);
        }
      }
      if (PS3.getButtonClick(RIGHT)) {
        Serial.print(F("\r\nRight"));
        if (PS3.PS3Connected) {
          PS3.setLedOff();
          PS3.setLedOn(LED1);
        }
      }
      if (PS3.getButtonClick(DOWN)) {
        Serial.print(F("\r\nDown"));
        if (PS3.PS3Connected) {
          PS3.setLedOff();
          PS3.setLedOn(LED2);
        }
      }
      if (PS3.getButtonClick(LEFT)) {
        Serial.print(F("\r\nLeft"));
        if (PS3.PS3Connected) {
          PS3.setLedOff();
          PS3.setLedOn(LED3);
        }
      }

      if (PS3.getButtonClick(L1))
        Serial.print(F("\r\nL1"));
      if (PS3.getButtonClick(L3))
        Serial.print(F("\r\nL3"));
      if (PS3.getButtonClick(R1))
        Serial.print(F("\r\nR1"));
      if (PS3.getButtonClick(R3))
        Serial.print(F("\r\nR3"));*/
}
/*#if 0 // Set this to 1 in order to see the angle of the controller
    if (printAngle) {
      Serial.print(F("\r\nPitch: "));
      Serial.print(PS3.getAngle(Pitch));
      Serial.print(F("\tRoll: "));
      Serial.print(PS3.getAngle(Roll));
    }
#endif*/
  }
}
