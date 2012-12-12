arduino-plant
=============

self watering arduino plant 

/*
 
  
  Reads a soil moisture sensor and turns on the relay that controls the water pump.
  
  The soil moisture sensor involves a 10K resistor between the ground and A1 pins
  and a probe connected to pin A1 and another connected to +5V. These probes or sensors 
  are inserted an inch apart in the plant's soil.
  
 */


// Analog input pin that the soil moisture sensor is attached to
const int analogInPin = A1;  

// value read from the soil moisture sensor
int sensorSoilValue = 0; 

 /* if the readings from the soil sensor drops below the value of dryValue then turn on the pump. 
 I tried to find an integer that would water the plant when it is almost dry and not too dry this is incase the water  tank is empty 
 I still have time to water the plant where as if its too dry and the water reservoir is empty the plant will not get watered
*/
int drySoilValue = 500;   

void setup() {
  
  pinMode(12, OUTPUT);
  
  // start serial communications at 9600 bps:
  Serial.begin(9600); 
}

void loop() {
  // read the analog in value:
  sensorSoilValue = analogRead(analogInPin);                   

  //Turns on the water pump if the soil is dry
  //Increasing the delay will increase the amount of water pumped
  if(sensorSoilValue < drySoilValue){
    digitalWrite(12, HIGH);
    delay(10000);
    digitalWrite(12, LOW);
  }
    
  // print the sensor to the serial monitor:
  Serial.print("sensor = " );                       
  Serial.println(sensorSoilValue);  


  delay(500);                     
}
