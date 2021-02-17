
#include <SoftwareSerial.h>

SoftwareSerial mySerial(15, 14);

int oilsensorpin = A1; //oil sensor pin

void setup()
{
Serial.begin(9600);
mySerial.begin(115200);

}
void loop()
{
 
  int sensor_val_current = analogRead(currentsensorpin) ;  
  sendtodgus( 2 , sensor_val_current);
  
}


//Fuction which send data to dgus
void sendtodgus(uint16_t addres , float sendingdata){
  uint8_t data1;
  uint8_t data2;
  uint8_t add1;  //dgus adrress1
  uint8_t add2;  //dgus address2
  uint16_t maindata; //data which you want to send to dgus
 
  add1 = addres;
  
  maindata= sendingdata*100;
  
  data1=highByte(maindata);
  data2=lowByte(maindata); 

        //Main Code
        
          mySerial.write(90);
          mySerial.write(165);
          mySerial.write(5);
          mySerial.write(130);
          mySerial.write(16);//add1
          mySerial.write(add1);//add2
          mySerial.write(data1);// first data send
          mySerial.write(data2); // second data send

}
