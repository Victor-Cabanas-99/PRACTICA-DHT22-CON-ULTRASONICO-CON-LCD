# PRACTICA-DHT22-CON-ULTRASONICO-CON-LCD
## INTRODUCCION 
### Descripcion 
Se realizara una medición con un sensor ULTRASONICO y DHT 22 donde se mostrara la distancia, temperatura y humedad en una pantalla LCD 
La Esp32 es una tarjeta de adquisición de datos, paralo cual en esta practica ocuparemos un sensor (DTH11) con una pantalla LCD216 para adquirir datos de temperatura y humedad del entorno cada segundo y mostrarlar los datos en la panatlla, se usara un simulador llamado WOKWI.
## MATERIAL A UTILIZAR
- [WOKWI](https://wokwi.com/projects/new/esp32)
- TARJET ESP32
- SENSOR ULTRASONICO
- LCD 16X2 2IC
## INSTRUCCIONES
Insertar el codigo dado de la practica, se realizara la misma actividad que la practica anterior mostrando datos de quien esta programando:


```
const int Trigger = 4;   //Pin digital 4 para el Trigger del sensor
const int Echo = 2;   //Pin digital 2 para el Echo del sensor

#include <LiquidCrystal_I2C.h> //Libreria de LCD
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4
#include "DHTesp.h" //Libreria de DHT

const int DHT_PIN = 15; //pin del sensor de temperatura
DHTesp dhtSensor;
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0

}

void loop() {

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
 
  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
  //delay(2000); 
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  Serial.println("---");
  delay(2000);          //Hacemos una pausa de 200ms

  lcd.clear(); 
  lcd.setCursor(0, 0); //coordenadas del LCD 
  lcd.print("MODULO V");
  lcd.setCursor(0, 1);
  lcd.print("Mecatronica");
 delay(2000);

lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Victor Cabanas");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Mecanica");
  delay(2000);

 lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
  delay(2000);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  delay(2000);

}
```
2. Instalar la libreria de **LiquidCrystal I2C** y  **DHT sensor library for ESPx** como se muestra en la siguente imagen.

![]()

3. Hacer la conexion de **LCD 16X2 2IC**, la **HC-SR04 ULTRASONIC DISTANCE SENSOR** y el **DHT sensor library for ESPx** con la **ESP32** como se muestra en la siguente imagen.

![]()

### Instrucciónes de operación

1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la distancia *doble click* al sensor **HC-SR04 ULTRASONIC DISTANCE SENSOR**
4. Colocar la temperatura y humedad *doble click* al sensor **DHT sensor library for ESPx**

## Resultados

Cuando haya funcionado, verás los valores dentro del monitor serial como se muestra en la siguente imagen.
![]()

## Librerías

1. **LiquidCrystal I2C**
2. **DHT sensor library for ESPx**

