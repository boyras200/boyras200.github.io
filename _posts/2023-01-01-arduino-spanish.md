---
layout: post
title: Como poner el teclado de un digispark en español
subtitle: Como poner el teclado de un digispark en español
cover-img: /assets/img/arduino-spanish/icono.png
thumbnail-img: /assets/img/arduino-spanish/icono.png
tags: [fácil, arduino, digispark, español]
excerpt:  "En este post vamos a ver como cambiar el idioma de la inyección de texto en un Dgispark. Para esto simplemente tenemos que cambiar una librería por otra que nos vamos a descargar"
---

## Como poner el teclado de un Digispark en español

En este post vamos a ver como poner el idioma de un Digispark en español, esto es bastante sencillo. 

{INSTALAR ARDUINO}


El problema del teclado viene de la librería con la que simulamos un teclado en arduino (DigiKeyboard.h). Esta reconoce el teclado como uno en inglés y no en español. Por culpa de este problema no se pueden utilizar la mayoría de símbolos, como el "=". Ahora vamos a ver como sustituir la librería en español por una en inglés para solucionar este problema.

Lo primero es descargarse la librería en español:

`https://github.com/Dasor/digispark-keyboard-layout-Spanish/blob/master/DigiKeyboard.h`

Le damos click derecho al botón de "Raw" y le damos a "Guardar enlace como":

![](/assets/img/arduino-spanish/descargar.png)

Ahora nos guardamos el archivo:

![](/assets/img/arduino-spanish/descargar2.png)

Una vez lo tenemos descargado vamos a copiarlo con click derecho y copiar:

![](/assets/img/arduino-spanish/paso.png)


Ahora que está copiado, pulsamos Windows + R , escribimos el siguiente comando:


![](/assets/img/arduino-spanish/paso2.png)


Le damos a aceptar y ahora vamos entrando en las siguientes carpetas:


![](/assets/img/arduino-spanish/paso3.png)

![](/assets/img/arduino-spanish/paso4.png)

![](/assets/img/arduino-spanish/paso5.png)

![](/assets/img/arduino-spanish/paso6.png)

![](/assets/img/arduino-spanish/paso7.png)

![](/assets/img/arduino-spanish/paso8.png)

![](/assets/img/arduino-spanish/paso9.png)

![](/assets/img/arduino-spanish/paso9.png)

![](/assets/img/arduino-spanish/paso10.png)

![](/assets/img/arduino-spanish/paso11.png)


Hacemos click derecho en el archivo y le damos a eliminar:


![](/assets/img/arduino-spanish/paso12.png)

Ahora ya eliminado vamos a pegar nuestro archivo en español:


![](/assets/img/arduino-spanish/paso13.png)

![](/assets/img/arduino-spanish/paso14.png)

Ya tenemos el archivo en español, ahora podemos insertar texto con un Digispark correctamente con un programa como este, por ejemplo :

```
#include "DigiKeyboard.h"                                
                                                         
void setup() {                                           
  pinMode(1, OUTPUT);                                    
}                                                        
                                                         
void loop() {                                            
                                                         
  DigiKeyboard.update();                                 
  DigiKeyboard.sendKeyStroke(0);                         
  DigiKeyboard.delay(500);                               
                                                         
  DigiKeyboard.sendKeyStroke(KEY_R, MOD_GUI_LEFT); //run 
  DigiKeyboard.delay(300);                               
  DigiKeyboard.println("firefox.exe"); //Abre firefox    
  DigiKeyboard.delay(250);                               
  DigiKeyboard.println("Rijaba1 es un capo);                    
                                                         
  digitalWrite(1, HIGH); //Luz roja cuando el rograma termina  
  DigiKeyboard.delay(90000);                                  
  digitalWrite(1, LOW);                                        
  DigiKeyboard.delay(5000);                                   
