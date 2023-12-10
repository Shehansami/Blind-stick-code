// Pin assignments
const int TRIGGER_PIN = 6;
const int ECHO_PIN = 5;
const int buzzer = 4;
const int MOTOR_PIN = 7;
// Threshold distances
const int ALERT_DISTANCE = 100; // Alert if object is within 30 cm
// Timing constants
const int BUZZER_ON_TIME = 500; // Buzzer on time in milliseconds
const int MOTOR_ON_TIME = 200; // Haptic motor on time in milliseconds
const int LOOP_DELAY = 50; // Main loop delay in milliseconds
void setup() {
  // Set up pins
  pinMode(TRIGGER_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(MOTOR_PIN, OUTPUT);
  // Start serial communication for debugging
  Serial.begin(9600);
}
void loop() {
  // Send ultrasonic pulse
  digitalWrite(TRIGGER_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIGGER_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIGGER_PIN, LOW);
  // Measure pulse duration
  long duration = pulseIn(ECHO_PIN, HIGH);
  // Calculate distance in cm
  int distance = duration / 58;
  // Debug output
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  // Check for alerts
  if (distance <= ALERT_DISTANCE) {
  // Turn on buzzer
    tone(buzzer, 1000, 1000); // 1KHz
    digitalWrite(MOTOR_PIN, HIGH);
    delay(BUZZER_ON_TIME);
    digitalWrite(MOTOR_PIN, LOW);
    noTone(buzzer); // 1KHz
}
noTone(buzzer); // 1KHz
  // Wait before taking another reading
  delay(LOOP_DELAY);
}
