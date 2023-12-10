#define trigPin  6
#define echoPin  5
#define buzzer 4
#define motor 7

long duration, Distanceincm;
void setup() {
pinMode(trigPin, OUTPUT);
pinMode(echoPin, INPUT);
pinMode(buzzer,OUTPUT);
pinMode(motor,OUTPUT);
Serial.begin(9600);
}
void loop() 
{ 
  digitalWrite(trigPin, HIGH);
  delay(15);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  Distanceincm = duration/58;
  Serial.print("Distance in Cm = ");
  Serial.print(Distanceincm);
  Serial.println();
  if(Distanceincm<=100){
    digitalWrite(buzzer,HIGH);
    Serial.println("buzzwr_on");
    delay(100);
    digitalWrite(buzzer,LOW);
    Serial.println("buzzer_off");
    delay(50);
    digitalWrite(buzzer,HIGH);
    delay(100);
    digitalWrite(buzzer,LOW);

    digitalWrite(motor,HIGH);
    delay(500);
    digitalWrite(motor,LOW);
  }
  delay(200);
  
}
