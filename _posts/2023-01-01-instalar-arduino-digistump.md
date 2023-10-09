---
layout: post
title: Como instalar Arduino IDE  para Digispark
subtitle: Instalando Arduino y Digistump
cover-img: /assets/img/instalar-arduino-digistump/icono2.png
thumbnail-img: /assets/img/instalar-arduino-digistump/icono2.png
tags: [arduino, digistump, digispark]
excerpt: "En este artículo vamos a ver como Instalar Arduino IDE, los drivers para Digispark y sus librerías correspondientes. Espero que lo disfrutéis y que os sea de mucha ayuda."
---

Hecho por boyras200

<br>
<br>

## Como instalar Arduino IDE para Digispark 

En este post vamos a ver como Instalar Arduino IDE y los drivers para Digispark(digistump).

Lo primero es irnos a la página oficial de Arduino - `https://www.arduino.cc/en/software`


En la web vemos esto: 

![](/assets/img/instalar-arduino-digistump/paso1.png)

Bajamos y encontramos las opciones de descarga:

![](/assets/img/instalar-arduino-digistump/paso2.png)

Seleccionamos la opción para Windows. Le damos al botón "Just Download":

![](/assets/img/instalar-arduino-digistump/paso3.png)

Ahora en la carpeta de descargas vamos a extraer el archivo con Winrar. 

 - [Instalar Winrar](https://www.youtube.com/watch?v=6yk3dd74A2c&t=8s) 

Extraemos el archivo:

![](/assets/img/instalar-arduino-digistump/paso4.png)

![](/assets/img/instalar-arduino-digistump/paso5.png)

Una vez extraído tenemos dos carpetas. Entramos en la segunda para ejecutar Arduino IDE:

![](/assets/img/instalar-arduino-digistump/paso6.png)

![](/assets/img/instalar-arduino-digistump/paso8.png)

Después de hacer doble click sobre "Arduino IDE.exe", tenemos que permitir acceso a todas las peticiones que nos aparezcan en la pantalla. Puede que nos pida descargar unas cosas, simplemente tenemos que aceptarlo todo. Ahora ya tenemos Arduino IDE instalado:

![](/assets/img/instalar-arduino-digistump/paso9.png)

Lo siguiente va a ser instalar los drivers para el Digispark (digistump). <br>

- [Instalar Drivers](https://github.com/digistump/DigistumpArduino/releases/download/1.6.7/Digistump.Drivers.zip)

Una vez instalados vamos a extraer su contenido:

![](/assets/img/instalar-arduino-digistump/paso21.png)

![](/assets/img/instalar-arduino-digistump/paso22.png)

Entramos en la carpeta. Vemos otra en la que volvemos a entrar:

![](/assets/img/instalar-arduino-digistump/paso23.png)

Seguidamente instalaremos los drivers haciendo doble click sobre "Install Drivers.exe":

![](/assets/img/instalar-arduino-digistump/paso24.png)

Le tenemos que dar permisos e instalar todo lo que nos pida. Ahora ya tenemos los drivers instalados. Lo siguiente es descargarnos la librería Digistump. Lo vamos a hacer así:

![](/assets/img/instalar-arduino-digistump/paso10.png)

Después de clicar en Preferences vemos un panel, ahora pegamos la siguiente url:

![](/assets/img/instalar-arduino-digistump/paso12.png)

```
http://digistump.com/package_digistump_index.json
```

Le damos a OK. A continuación nos dirigimos a la sección "Boards Manager" de Arduino IDE. Nos vamos a descargar la placa Digispark para poder meter programas en esta. Simplemente buscamos Digistump y descargamos el primero haciendo click en el botón "INSTALL":

![](/assets/img/instalar-arduino-digistump/paso13.png)

![](/assets/img/instalar-arduino-digistump/paso14.png)

Cuando esté instalado vemos el icono de "INSTALLED". Lo siguiente es seleccionar la placa para hacer unas pruebas:

![](/assets/img/instalar-arduino-digistump/paso15.png)

Después de seleccionar la opción de Digispark normal deberíamos ver esto:

![](/assets/img/instalar-arduino-digistump/paso16.png)

Finalmente vamos a subir nuestro programa:

![](/assets/img/instalar-arduino-digistump/paso17.png)

```
const int ledPin = 1;

void setup()
{
  pinMode(ledPin, OUTPUT);
}

void loop()
{
  digitalWrite(ledPin, HIGH);
  delay(550);
  digitalWrite(ledPin, LOW);
  delay(250);
  digitalWrite(ledPin, HIGH);
  delay(250);
  digitalWrite(ledPin, LOW);
  delay(500);
  digitalWrite(ledPin, HIGH);
  delay(1000);
  digitalWrite(ledPin, LOW);
  delay(250);
}

```

Este es un programa muy simple, hace que la luz del Digispark se encienda y se apague. Primero compilamos el programa con el botón de "PLAY" y después lo subiremos con el botón "UPLOAD", que están a la izquierda y a la derecha respectivamente:

![](/assets/img/instalar-arduino-digistump/paso18.png)

Deberíamos ver algo parecido a esto en la parte inferior:

![](/assets/img/instalar-arduino-digistump/paso19.png)

Ya es el momento de conectar el Digispark a nuestro ordenador. Si todo va bien deberíamos ver algo como esto:

![](/assets/img/instalar-arduino-digistump/paso25.png)

