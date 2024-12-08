# ULTRASONICO CON LCD
## Practica con un sensor ultrasonico en una placa de desarrollo ESP32 y un LCD de 12C 
Este repositorio muestra como podemos programar una **ESP32** con el sensor **HC-SR04** y mostrar los datos optenidos en un **LCD 12c**.

### Introducción
**Descripción:** 
La **ESP32** la utilizamos en un entorno de adquision de datos, en esta practica ocuparemos un **sensor ultrasonico** para medir la distancia del entorno, como tambien un **LCD de 12c** para visualizar los datos opotenidos, todo siendo simulado en una pagina llamda **WOKWI**

### Material Necesario
Para realizar esta practica necesitas lo siguiente:
- WOKWI
- Tarjeta ESP32
- Sensor ultrasonico HC-SR04
- LCD (16x2) 12c

### Requisitos previos:
Para poder usar este repositorio necesitas entrar a la plataforma WOKWI.

### Instrucciones de preparación de entorno:
1.-Abrir la terminal de programación y colocar la siguente programación:
```
const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0

  lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros


  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
lcd.clear(); 
  lcd.setCursor(4, 0); //Coordenadas para imprimir en la LCD
  lcd.print("MODULO V");
  lcd.setCursor(6, 1);
  lcd.print("AIyM");
 delay(2000);

lcd.clear(); //Limpiar el texto en la LCD
  lcd.setCursor(2, 0);
  lcd.print("diego bahena");
  lcd.setCursor(6, 1);
  lcd.print("I.E.E");
  delay(2000);
  
lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) + "cm");
  lcd.setCursor(0, 1);
  delay(2000);

  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(2000);          //Hacemos una pausa de 200ms
}
```

2.- Instalar la libreria de **LiquidCrystal I2C** como se muestra en la siguente imagen.

![image](https://github.com/user-attachments/assets/a27adc47-0de2-43f7-b74d-93e9396c6586)

3.- Hacer la conexion de **HC-SR04** con la **ESP32** y el **LCD 12C** como se muestra en la siguente imagen.

![image](https://github.com/user-attachments/assets/a9cfda3d-41d6-419a-a799-1885e876a45c)

### Instrucciónes de operación
- Iniciar simulador.
- Visualizar los datos en el LCD.
- Colocar la distancia dando click al sensor ultrasonico HC-SR04
  
### Resultados
Cuando haya funcionado, verás los valores dentro del LCD como se muestra en la siguente imagen.

![image](https://github.com/user-attachments/assets/460fab28-2b6c-43e6-bbf0-16aadb15c145)

![image](https://github.com/user-attachments/assets/01d7563e-aa48-4749-87e6-ec79e90b4fd8)

![image](https://github.com/user-attachments/assets/a5255ad3-65c3-4330-8676-7f36e45c2711)

### Desarrollado por 
Diego David Bahena Galan

[GitHub](https://github.com/DiegoDBG)
