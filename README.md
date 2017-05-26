# X11VNC
Acceso remoto por VNC
UBUNTU

<b>1.Instalar X11VNC</b>

```bash
~$ sudo apt-get update
~$ sudo apt-get install x11vnc
```
<b>2. Crear Password </b>
```bash
x11vnc -storepasswd

Enter VNC password: *********
Verify password: *********  
Write password to /home/<-user->/.vnc/passwd?  [y]/n y
Password written to: /home/<-user->/.vnc/passwd
```
<b>3. Arrancar el servicio vnc</b>
```bash
$ sudo x11vnc -auth guess -forever -loop -noxdamage -repeat \ 
  -rfbauth /home/<-user-->/.vnc/passwd -rfbport 5900 -shared
```






