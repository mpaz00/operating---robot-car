# operating---robot-car
int ENA=5;
int ENB=6;
int IN1=7;
int IN2=8;
int IN3=9;
int IN4=11;
float d=1;
int degRot=90;
int left;
int right;
float v=1.2;
int rv;
char cmd;
void setup() {
  
Serial.begin(9600);


pinMode(ENA,OUTPUT);
pinMode(ENB,OUTPUT);
pinMode(IN1,OUTPUT);
pinMode(IN2,OUTPUT);
pinMode(IN3,OUTPUT);
pinMode(IN4,OUTPUT);
digitalWrite(ENA,HIGH);
digitalWrite(ENB,HIGH);
}

void loop() {
int wv;
wv=(v-.35)/.0075;
left=wv;
right=wv;
setSpeed(left,right);
while (Serial.available()==0){
}
cmd=Serial.read();
if (cmd=='G'){
  Serial.println("Forward");
  forward(d,v);  
}
if (cmd=='B'){
  Serial.println("Backward");
  backward(d,v);  
}
if (cmd=='R'){
  Serial.println("Right");
  turnRight(degRot,wv);  
}
if (cmd=='L'){
  Serial.println("Left");
  turnLeft(degRot,wv);  
}
if (cmd=='d'){
  Serial.println("Set distance");
  delay(500);

  while (Serial.available()==0){
  }
cmd=Serial.read();

    if (cmd=='1'){
    Serial.println("Distance=1");
    d=1;
  }
    if (cmd=='2'){
    Serial.println("Distance=2");
    d=2;
  }
      if (cmd=='3'){
    Serial.println("Distance=3");
    d=3;
  }
      if (cmd=='4'){
    Serial.println("Distance=4");
    d=4;
  }
      if (cmd=='5'){
    Serial.println("Distance=5");
    d=5;
  }
      if (cmd=='6'){
    Serial.println("Distance=6");
    d=6;
  }
      if (cmd=='7'){
    Serial.println("Distance=7");
    d=7;
  }
      if (cmd=='8'){
    Serial.println("Distance=8");
    d=8;
  }
      if (cmd=='9'){
    Serial.println("Distance=9");
    d=9;
  }
}

if (cmd=='v'){
  Serial.println("Set speed");
  delay(500);
   while (Serial.available()==0){
    
  }
  delay(100);
  cmd=Serial.read();
    if (cmd=='1'){
    Serial.println("rv=1");
    rv=1;
  }
    if (cmd=='2'){
    Serial.println("rv=2");
    rv=2;
  }
      if (cmd=='3'){
    Serial.println("rv=3");
    rv=3;
  }
      if (cmd=='4'){
    Serial.println("rv=4");
    rv=4;
  }
      if (cmd=='5'){
    Serial.println("rv=5");
    rv=5;
  }
      if (cmd=='6'){
    Serial.println("rv=6");
    rv=6;
  }
      if (cmd=='7'){
    Serial.println("rv=7");
    rv=7;
  }
      if (cmd=='8'){
    Serial.println("rv=8");
    rv=8;
  }
      if (cmd=='9'){
    Serial.println("rv=9");
    rv=9;
  }
  v=(1.16/9.)*rv+1.1;

}
if (cmd=='r'){
  Serial.println("Set rotation");
  delay(100);
  while (Serial.available()==0){
  }
  cmd=Serial.read();
  delay(100);
  if (cmd=='1'){
    Serial.println("Rotation=1");
    v=1;
  }
    if (cmd=='2'){
    Serial.println("Rotation=2");
    v=2;
  }
    if (cmd=='3'){
    Serial.println("Distance=3");
    v=3;
  }
      if (cmd=='4'){
    Serial.println("Distance=4");
    v=4;
  }
      if (cmd=='5'){
    Serial.println("Distance=5");
    v=5;
  }
      if (cmd=='6'){
    Serial.println("Distance=6");
    v=6;
  }
      if (cmd=='7'){
    Serial.println("Distance=7");
    v=7;
  }
      if (cmd=='8'){
    Serial.println("Distance=8");
    v=8;
  }
      if (cmd=='9'){
    Serial.println("Distance=9");
    v=9;
  }
  wv=(v-.35)/.0075;
}
}
void setSpeed(int leftVal,int rightVal){
  analogWrite(ENA,leftVal);
  analogWrite(ENB,rightVal);
}
void forward(float d, float v){
float t;
digitalWrite(IN1,HIGH);
digitalWrite(IN2,LOW);
digitalWrite(IN3,LOW);
digitalWrite(IN4,HIGH);
t=d/v*1000;
delay(t);
stopCar();
}
void backward(float d, float v){
float t;
digitalWrite(IN1,LOW);
digitalWrite(IN2,HIGH);
digitalWrite(IN3,HIGH);
digitalWrite(IN4,LOW);
t=d/v*1000;
delay(t);
stopCar();
}
void turnRight(int deg, int wv){
  float t;
stopCar();
delay(100);
analogWrite(ENA,125);
analogWrite(ENB,125);
digitalWrite(IN1,HIGH);
digitalWrite(IN2,LOW);
digitalWrite(IN3,HIGH);
digitalWrite(IN4,LOW);
t=(deg+6)/136.29*1000.;
delay(t);
stopCar();
analogWrite(ENA,wv);
analogWrite(ENB,wv);
}
void turnLeft(int deg, int wv){
float t;
analogWrite(ENA,125);
analogWrite(ENB,125);
digitalWrite(IN1,LOW);
digitalWrite(IN2,HIGH);
digitalWrite(IN3,LOW);
digitalWrite(IN4,HIGH);
t=(deg+6)/136.29*1000.;
delay(t);
stopCar();
analogWrite(ENA,wv);
analogWrite(ENB,wv);
}
void stopCar(){
digitalWrite(IN1,LOW);
digitalWrite(IN2,LOW);
digitalWrite(IN3,LOW);
digitalWrite(IN4,LOW);
}

void calF(){
digitalWrite(IN1,HIGH);
digitalWrite(IN2,LOW);
digitalWrite(IN3,LOW);
digitalWrite(IN4,HIGH);
delay(5000);
stopCar();
}
void calB(){
digitalWrite(IN1,LOW);
digitalWrite(IN2,HIGH);
digitalWrite(IN3,HIGH);
digitalWrite(IN4,LOW);
delay(5000);
stopCar();
}
void calR(int wv){
stopCar();
analogWrite(ENA,125);
analogWrite(ENB,125);
digitalWrite(IN1,HIGH);
digitalWrite(IN2,LOW);
digitalWrite(IN3,HIGH);
digitalWrite(IN4,LOW);
delay(3000);
analogWrite(ENA,wv);
analogWrite(ENB,wv);
stopCar();
}
void calL(int wv){
analogWrite(ENA,125);
analogWrite(ENB,125);
digitalWrite(IN1,LOW);
digitalWrite(IN2,HIGH);
digitalWrite(IN3,LOW);
digitalWrite(IN4,HIGH);
delay(5000);
analogWrite(ENA,wv);
analogWrite(ENB,wv);
stopCar();
}
