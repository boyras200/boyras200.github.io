---
layout: post
title: Tratamiento de la tty
subtitle: Que es y como tratar la tty
cover-img: /assets/img/tratamiento-tty/icono.jpg
thumbnail-img: /assets/img/tratamiento-tty/icono.jpg
tags: [linux, instalación, metasploitable2]
excerpt: "En este post vamos a instalar la máquina virtual vulnerable llamada Metasploitable2. Esta nos sirve para practicar una gran cantidad de vulnerabilidades comunes."
---


## ¿Qué es la tty?

La tty es un dispositivo de entrada y salida de comandos que utilizamos en Linux. Si te preguntas que diferencia tiene con la terminal, la respuesta es ninguna. El término viene, porque antiguamente, se introducían los comandos por un lugar diferente del que salía el resultado. Este salía por la tty. No hay que confundir la shell con la tty, ya que la función de la shell es interpretar los comandos que introducimos para tomar acciones.

## ¿Qué es un tratamiento de la tty??

Cuando nos referimos a un tratamiento de la tty o un tratamiento de la terminal, lo que hacemos es cambiar los ajustes de nuestra terminal para que nos sea más sencilla de usar y no nos de problemas a la hora de ejecutar determinadas acciones y comandos.  

## Preparando una reverse shell para tratar la tty:

Ahora vamos a ver como hacer un tratamiento de la tty. Para este ejemplo vamos a utilizar la plataforma dvwa en la máquina virtual Metasploitable2. Si no la tienes instalada te dejo un artículo explicando como hacerlo aquí abajo. 

[Instalar Metasploitable 2](https://boyras200.github.io/instalar-metasploitable2) 

Tenemos que iniciar nuestra máquina virtual Metasploitable2 (máquina víctima), y nuestro kali linux <br>
(máquina de atacante, no es necesario que sea kali linux).

Hacemos un fping para buscar la IP de Metasploitable2:

![](/assets/img/tratamiento-tty/IP.png)

Vemos que nuestra IP es la 192.168.47.156, entonces la única IP que podría ser metasploitable2 es la 192.168.47.129. Ya que la 
192.168.47.2 es el router de la red. 

Ahora vamos a entrar a dvwa. Para entrar a la web simplemente ponemos la IP de la máquina en el navegador:

![](/assets/img/tratamiento-tty/web.png)

Ahora entramos al directorio de dvwa clicando en el enlace:

![](/assets/img/tratamiento-tty/web2.png)

Observamos un panel de inicio de sesión. El usuario es admin y la contraseña password. Una vez ya tenemos acceso a dvwa vamos al apartado de Dvwa Security, lo que vamos a hacer ahora es cambiar el nivel de seguridad de la página a "low":

![](/assets/img/tratamiento-tty/web3.png)

![](/assets/img/tratamiento-tty/web3-1.png)

Ahora vamos a preparar nuestra reverse shell en php. Para esto vamos a usar la conocida reverse shell de PentestMonkey. Lo primero es ir a la página `https://www.revshells.com` :

![](/assets/img/tratamiento-tty/revshell4.png)

En la parte de IP escribimos nuestra dirección IP, podemos ejecutar el comando **hostname -I** para comprobarla. Como puerto vamos a poner el 4444. Ahora vamos a seleccionar la reverse shell de PentestMonkey y descargárnosla:

![](/assets/img/tratamiento-tty/revshell.png)

Una vez le hayamos dado al botón de descarga nos aparecerá lo siguiente:

![](/assets/img/tratamiento-tty/revshell2.png)

Le ponemos el nombre "monkey.php". Después le damos a OK y ya tenemos la reverse shell descargada, lo siguiente es moverla a la carpeta de descargas:

![](/assets/img/tratamiento-tty/revshell3.png)

Una vez trasladada ya podemos empezar. Ahora vamos a subir la reverse shell a la página:

![](/assets/img/tratamiento-tty/web4.png)

En el apartado Upload seleccionamos nuestra reverse shell con el botón Browse y le damos a Upload:

![](/assets/img/tratamiento-tty/web5.png)

![](/assets/img/tratamiento-tty/web6.png)

## Tratando la tty:

Una vez subida nos da la ruta donde se ha subido nuestra reverse shell. La ruta absoluta sería esta <br>
-> http://{IP-DE-METASPLOITABLE2}/dvwa/hackable/uploads/monkey.php  <br>
Primero nos ponemos a la escucha con el comando **nc -lvnp 4444** y después entramos a link. En nuestra terminal vemos esto:

![](/assets/img/tratamiento-tty/web7.png)

Ahora vamos a proceder con el tratamiento de la tty. Los comandos son los siguientes:

```
script /dev/null -c bash   #Nos crea una shell en bash
Control z                  #Suspende la sesión
stty raw -echo;fg          #Recupera la shell
reset                      #Reinicia la shell
xterm                      #Indicamos el tipo de terminal que queremos utilizar
export TERM=xterm          #Asigna a la variable TERM xterm
export SHELL=bash          #Asigna bash a la variable SHELL
stty rows {TUS-FILAS}      #Para saber qué poner aquí ejecutar el comando stty -a
stty columns {COLUM}       #Para saber qué poner aquí ejecutar el comando stty -a 
```

![](/assets/img/tratamiento-tty/web9.png)

Después de ejecutar el comando **stty raw -echo;fg** ejecutamos lo siguiente y ya estaría:

![](/assets/img/tratamiento-tty/web8.png)

Ya tenemos una tty completamente tratada y funcional.

Espero que os haya gustado y hayaís entendido todos los pasos. Si no es así podéis contactar conmigo. Hasta la próxima!!!
