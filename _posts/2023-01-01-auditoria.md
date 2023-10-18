---
layout: post
title: Cosas a comprobar
subtitle: Sacatan sacatun tan tan tan 
cover-img: /assets/img/auditoria/icono.png
thumbnail-img: /assets/img/auditoria/icono.png
tags: [auditoria]
excerpt: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
---

Hecho por boyras200

<br>
<br>



## Cosas a comprobar

```
Mirar si esta el usuario Auditoria creado, despues ejecutar:

  Windows. Simbolo del sistema, con permisos de administrador.
  net user Usuario-Auditoria D2z14IdWykPO /add
  net localgroup Administradores Usuario-Auditoria /add
```

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

Dejar su tiempo a que se ejecute cada comando.

Mirar la IP publica y privada del dispositivo. 

Publica -> `https://www.cual-es-mi-ip.net/`

Privada -> CMD. Despues un ipconfig.

Sacarle fotos a estas IP

Por si acaso dejo lo del router.

## Router (actualizado)

Primero entramos en `https://www.cual-es-mi-ip.net/`

![](/assets/img/auditoria/ip.png)

Ahora vamos a `http://192.168.100.1/`

Ponemos las credenciales root:admin

Encontramos algo como esto:

![](/assets/img/auditoria/huwai.png)


Vamos a advanced:

![](/assets/img/auditoria/huwai2.png)

Vamos a fordward rules:

![](/assets/img/auditoria/huwai3.png)


Vamos a IPv4PortMapping:

![](/assets/img/auditoria/huwai4.png)


Le damos a new:

![](/assets/img/auditoria/huwai5.png)


Ponemos la IP privada:

![](/assets/img/auditoria/huwai6.png)


Le damos a add:

![](/assets/img/auditoria/huwai7.png)


Ponemos los siguientes parametros:

![](/assets/img/auditoria/huwai8.png)

Le damos a apply

# Ya debería estar funcionando todo.
