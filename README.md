ARDUINO PROGRAMS
2. Measure the distance using ultrasonic sensors and make an LED Blink using Arduino
const int trigPin = 9;
const int echoPin = 10;
const int ledPin = 3;
long duration;
int distance;
void setup(){
 pinMode(trigPin, OUTPUT);
 pinMode(echoPin, INPUT);
 pinMode(ledPin, OUTPUT);
 Serial.begin(9600);
}
void loop(){
 digitalWrite(trigPin, LOW);
 delayMicroseconds(2);
 digitalWrite(trigPin, HIGH);
 delayMicroseconds(10);
 digitalWrite(trigPin, LOW);
 duration = pulseIn(echoPin, HIGH);
 distance = duration*0.0343/2;
 Serial.print(duration);
 Serial.print(" Distance: ");
 Serial.print(distance);
 Serial.print(" cm");
 Serial.println();
 if(distance<10){
 digitalWrite(ledPin, HIGH);
 }
 else{
 digitalWrite(ledPin, LOW);
 }
 delay(500);

}
3. Detect the vibration of an object using Arduino
const int vibrationPin = 2;
const int ledPin = 7;
void setup() {
 pinMode(vibrationPin, INPUT);
 pinMode(ledPin, OUTPUT);
 Serial.begin(9600);
}
void loop() {
 int vibrationState = digitalRead(vibrationPin);
 if (vibrationState == LOW) {
 digitalWrite(ledPin, HIGH);
 Serial.println("Vibration Detected!");
 delay(500);
 } else {
 digitalWrite(ledPin, LOW);
 delay(500);
 }
}
4. Temperature Notification using Arduino.
#include <DHT.h>
#define DHTPIN 2
#define DHTTYPE DHT11
DHT dht(DHTPIN, DHTTYPE);
const float tempThreshold = 30.0;
void setup() {
 Serial.begin(115200);
 unsigned long startMillis = millis();
 while ((millis() - startMillis) < 5000) {
 Serial.println("Initializing DHT Sensor...");
 }
 dht.begin();
}
void loop() {
 float temp = dht.readTemperature();
 float humidity = dht.readHumidity();
 if (isnan(temp) || isnan(humidity)) {
 Serial.println("Failed to read from DHT sensor!");
 delay(2000);
 return;
 }
 Serial.print("Temperature: ");
 Serial.print(temp);
 Serial.print(" °C, Humidity: ");
 Serial.print(humidity);
 Serial.println(" %");
 if (temp > tempThreshold) {
 Serial.println("ALERT: Temperature exceeded threshold!");
 }
 delay(5000);
}
5. LDR to vary LED Light intensity using Arduino.
int light;
void setup() {
 pinMode(8, OUTPUT); // LED connected to digital pin 8
 Serial.begin(9600); // Start serial communication
}
void loop() {
 light = analogRead(A0); // Read LDR value from analog pin A0
 Serial.print("LDR Value: ");
 Serial.println(light); // Print LDR value for observation
 if (light > 250) {
 digitalWrite(8, HIGH); // Turn ON LED when it's bright
 // digitalWrite(13, HIGH); // Uncomment if using built-in LED
 } else {
 digitalWrite(8, LOW); // Turn OFF LED when it's dark
 // digitalWrite(13, LOW); // Uncomment if using built-in LED
 }
 delay(200); // Delay for stability
}
 delay(100); // Short delay to avoid flickering
}
