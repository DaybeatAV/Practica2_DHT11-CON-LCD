# PRACTICA2_DHT11-Con-LCD
En este respositorio se mostrará como programar con DHT11 Y LCD en una ESP32

## INTRODUCCION

### DESCRIPCION

Utilizaremos una tarjeta ```Esp32``` en un entorno de adquision de datos, por lo cual en esta practica ocuparemos un sensor ```DTH11``` para obtener la temperatura y humedad del entorno; se debe dejar claro que en esta practica se utilizará el simulador -[WOKWI](https://wokwi.com/) con el que ya se ha trabajo en la práctica pasada.
Además se agregará una pantalla ```LCD I2C``` para observar los datos esperados en cada cierto intervalo de tiempo.

## MATERIAL NECESARIO

Para realizar esta practica necesitas lo siguiente:

- [WOKWI](https://wokwi.com/)

- Tarjeta ESP32

- Sensor DHT11

- Pantalla LCD 16X2 (I2C)

## INSTRUCCIONES

### Requisitos previos

Se necesitará entrar a la plataforma [WOKWI](https://wokwi.com/) para poder observar y manipular este repositorio.

### Instrucciones de preparación de entorno

1.Abrir la terminal de programación y colocar la siguente programación:

```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  
  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");

  lcd.setCursor(0, 0);
  lcd.print("   DIPLOMADO");
  lcd.setCursor(0, 1); 
  lcd.print(" AUTOMATIZACION");
   delay(2000);
  lcd.clear();

   lcd.setCursor(0, 0);
  lcd.print(" JAQUELINE R.H");
  lcd.setCursor(0, 1); 
  lcd.print("   INDUSTRIAL");
   delay(2000);
  lcd.clear();
   lcd.setCursor(0, 0);
  lcd.print("   07-06-2025");
  delay(2000);
  lcd.clear();
  
  
  lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1); 
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");
 

  delay(2000);
   lcd.clear();
}
```


2.Instalar la libreria de DHT sensor library for ESPx como se muestra en la siguente imagen
