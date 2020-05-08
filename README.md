# lokaverkefni-vesm-2020-cypertruck
ég heiti Alli B á github svo ef eh er að þá ætti að vera hægt að finna lokaverkefnin þar.


# dagbók

þetta var seinasta verkefnið sem ég ákvað að burja á og var það frekar seint. 2 dögum fyrir skil var ég buinn að vera að reinast með þetta að reina að senda I2C á milli beggja arduinoana en það gekk ekki mjög vel. ég náði samt að redda því einhverneigin og hélt áfram að uppfila í allar hinar kröfunar(fjærlægðar skinjari, skjár, móttorar). ég var svo heppin að fá hjálp frá honnum Stefáni þegar ég þurfti mest á hjálp að halda og verð ég æfinlega þákklátur!! þetta burjaði allt að takka á sig mynd og var þetta allt gert á 2 daga tímaspani
áður en skila þurfti verkefninu.

það var bara á seinustu klukkutimunum sem ég áhvað að sittja sem eftir var án pássu og pússla saman kubbunum. að mínu matti kom bíllinn og fjasteringin mjög vel út. ég fékk innblástur frá Cyper-truck frá tesla.



## circuit
https://www.tinkercad.com/things/2dihxWdtn4A-lokaverkefni-bill/editel?sharecode=w6HJQyCKhXec9kof2yqfGziXjouK6UmRCtT94QZievw



## 3D hönnun
https://www.tinkercad.com/things/crYuZ8b0IR0-cyper-truck-lokaverk-vsm2020/edit?sharecode=PwgfVcyu7e3zETZ0mH1ORJfDxj1Y-Upvc9HXLZxie8I

# THE CODE
## fjastering
#include <Servo.h>

Servo serv1, serv2;
const int trigPin = 1;
const int echoPin = 2;
long duration;
int CM;
int pos = 0;


Servo myservo;  // create servo object to control a servo

int potpin = 0;  // analog pin used to connect the potentiometer
int val;    // variable to read the value from the analog pin





int forward = 0;
int backward = 0;
int right = 0;
int left = 0;


void setup()
{
  pinMode(echoPin, INPUT);
  
  pinMode(8, INPUT);
  pinMode(12, INPUT);
  
  pinMode(trigPin, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(9, OUTPUT);
  
  digitalWrite(8,HIGH);
  digitalWrite(12,HIGH);
  
  digitalWrite(3,LOW);
  
  digitalWrite(5,LOW);
  digitalWrite(6,LOW);
  
  digitalWrite(9,LOW);
  serv1.write(0);
  serv2.write(0);
  serv1.attach(11);
  serv2.attach(7);
  
	
  myservo.attach(10);  // attaches the servo on pin 9 to the servo object
}

void loop()
{
  
  digitalWrite(trigPin, LOW);
  
  delayMicroseconds(2);
  
  digitalWrite(trigPin, HIGH);
  
  delayMicroseconds(10);
  
  digitalWrite(trigPin, LOW);
  
  
  duration = pulseIn(echoPin, HIGH);
  CM = duration*0.034/2;
  
  forward = digitalRead(12);
  
  backward = digitalRead(8);
  right = digitalRead(7);
  
  left = digitalRead(11);
  

  
  digitalWrite(3,LOW);
  digitalWrite(5,LOW);
  digitalWrite(6,LOW);
  digitalWrite(9,LOW);

  if(backward == 0)
  {
    
  if(CM <= 50){
  digitalWrite(3,LOW);
    
  digitalWrite(5,LOW);
    
  digitalWrite(6,LOW);
    
  digitalWrite(9,LOW);
  }
    
    else{
    digitalWrite(6,HIGH);
    digitalWrite(9,HIGH);
    }
    
  }

  if(forward == 0)
    
  {
  if(CM <= 50){
    
  digitalWrite(3,LOW);
  digitalWrite(5,LOW);
  digitalWrite(6,LOW);
  digitalWrite(9,LOW);
  }
    
    
    else{
    digitalWrite(3,HIGH);
    digitalWrite(5,HIGH);
    }
  }
  
  val = analogRead(potpin);// reads the value of the potentiometer (value between 0 and 1023)
  val = map(val, 0, 1023, 0, 180);     // scale it to use it with the servo (value between 0 and 180)
  myservo.write(val);                  // sets the servo position according to the scaled value
  delay(15);

  }
 
 ## bíllin
 
 #include <Wire.h>
#include <LiquidCrystal.h>
LiquidCrystal Skjar(6 , 7, 5, 4, 3, 2);

const int trigPin = 11;

const int echoPin = 10;
long duration;

int CM;

bool forward , backward , right , left =0;
void setup()
{
  Skjar.begin(16,2);
  
  
  
  pinMode(echoPin, INPUT);
  
  pinMode(trigPin, OUTPUT);
  


}

void loop()
{
 
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  
  digitalWrite(trigPin, HIGH);
  
  delayMicroseconds(10);
  
  digitalWrite(trigPin, LOW);
  
  duration = pulseIn(echoPin, HIGH);
  CM = duration*0.034/2;
  
  Skjar.setCursor(0,0); 
  Skjar.print("Fjarlaegd=");
  Skjar.print(CM); 
  Skjar.print("cm");
  
  
  

  if (CM > 100){ 
    Skjar.setCursor(0,1);    
    
    Skjar.print("Meters: ");
    Skjar.print(CM/100);
    Skjar.print("     ");
  	delay(2);
  }
 
  if (CM >51 and CM < 79){
  	Skjar.setCursor(0,1);
    Skjar.print("Passadu Tig!");
  }
  
  
  
  if (CM <= 50){
	Skjar.setCursor(0,0);
    Skjar.print("ekki áfram!!!        ");
    
    Skjar.setCursor(0,1);
    Skjar.print("kemst ekki!!");
    delay(500);
  }
  
  
  
  if (CM < 100 and CM > 80){
  Skjar.setCursor(0,1);
    
    
  Skjar.print("Meters: 0");
  Skjar.print("         ");
  }
  

}










