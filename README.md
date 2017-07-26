# X11VNC
Acceso remoto por VNC
UBUNTU

<b>1.Instalar X11VNC</b>

```bash
$ sudo apt-get update
$ sudo apt-get install x11vnc
```
<b>2. Crear Password </b>
```bash
$ x11vnc -storepasswd

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
<b>4. Configurar autoinicio en el arranque via upstart o systemd</b>

<b>4.1 Configurar autoinicio en el arranque via upstart</b>
Creamos el archivo x11vnc.conf

```bash
$ sudo vi /etc/init/x11vnc.conf
```
Agregamos el siguiente contenido:

```
# description "Configurar autoinicio en el arranque x11vnc "

description "x11vnc"

start on runlevel [2345]
stop on runlevel [^2345]

console log

respawn
respawn limit 20 5

exec /usr/bin/x11vnc -auth guess -forever -loop -noxdamage -repeat -rfbauth /home/<--user-->/.vnc/passwd -rfbport 5900 -shared
```

<b>4.2 Configurar autoinicio en el arranque via systemd</b>

Creamos el archivo x11vnc.service

```bash
$ sudo vi /lib/systemd/system/x11vnc.service
```
Agregamos el siguiente contenido:

```
# description "Configurar autoinicio en el arranque x11vnc "

[Unit]
Description=Start x11vnc at startup.
After=multi-user.target

[Service]
Type=simple
ExecStart=/usr/bin/x11vnc -auth guess -forever -loop -noxdamage -repeat -rfbauth /home/<--USERNAME-->/.vnc/passwd -rfbport 5900 -shared

[Install]
WantedBy=multi-user.target

```
Guardamos el archivo y luego ejecutamos la siguientes comandos

```bash
sudo systemctl daemon-reload
sudo systemctl enable x11vnc.service
```

<b>5.Reiniciar maquina</b>

```bash
$ sudo reboot
```
