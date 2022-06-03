# Johny Silva Mendes
# **Practica 6: Buses de comunicación II (SPI)**

Objetivo: usar los buses de comunicación SPI mediante la lectura y escritura de tarjetas de memoria SD.

## **1) void setup()**

```cs
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>

File myFile;

void setup(){

Serial.begin(9600);
Serial.print("Iniciando SD ...");

SPI.begin(18,19,23,4);

if(! SD.begin(4)){
  Serial.println("No se pudo inicializar");
  return;
}
  
Serial.println("inicializacion exitosa");

// Escribimos en el fichero
myFile = SD.open("/archivo.txt",FILE_WRITE); 
myFile.println("Escritura en SD correcta.");
myFile.close();

myFile=SD.open("/archivo.txt"); //Abrimos, mostramos y leemos
  if (myFile) {
    Serial.println("archivo.txt:");
    while (myFile.available()) {
      Serial.write(myFile.read());
    }
    myFile.close(); 
  }
  
  else {
    Serial.println("Error al abrir el archivo");
  }
}

void loop(){}
```

### Funcionamiento del programa
Se declaran las librerías para facilitar esta comunicación deseada. 
-- SPI.h  
-- SD.h
A continuación se creaa un objeto de la clase *File* llamado *myFile* para poder abrir y cerrar el fichero de la SD para poder leerlo o escribir en él.



En primer lugar, haremos uso de tres librerias en las que destacamos la librería SPI y SD. También tendremos que declarar una variable de tipo File a la que llamaremos "myFile".

```cpp
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>

File myFile;
```

Una vez dentro del setup(), se establece el baud rate a 9600. Se imprime por pantalla que se está iniciando la SD. 
Si todo sale correcto se procederá con la escritura. En caso contrario se avisará mostrando un mensaje.
```cpp
void setup(){

Serial.begin(9600);
Serial.print("Iniciando SD ...");

SPI.begin(18,19,23,4);

if(! SD.begin(4)){
  Serial.println("No se pudo inicializar");
  return;
}
  
Serial.println("inicializacion exitosa");

// Escribimos en el fichero
myFile = SD.open("/archivo.txt",FILE_WRITE); 
myFile.println("Escritura en SD correcta.");
myFile.close();

myFile=SD.open("/archivo.txt"); //Abrimos, mostramos y leemos
  if (myFile) {
    Serial.println("archivo.txt:");
    while (myFile.available()) {
      Serial.write(myFile.read());
    }
    myFile.close(); 
  }
  
  else {
    Serial.println("Error al abrir el archivo");
  }
}
```
Para realizar la escritura el programa abrirá el fichero llamado
 "archivo.txt" y en caso de que no exista la sentencia "FILE_WRITE" creará el fichero y procederá a abrirlo. 
 A continuación se escribirá en el fichero y posteriormente se imprimirá por el puerto série. 

### Salida por Terminal 

```cpp
Iniciando SD ...sd init ok
inicializacion exitosa
Escritura en SD correcta.
```