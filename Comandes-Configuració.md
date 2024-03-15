# COMANDES DE CONFIGURACIÓ DE DISPOSITIUS DE XARXA
## 1.1 COMANDES BÀSICAS (GENERALS)
Basicament, aqui s'ensenya com ficar un **Nom** al *Router/Switch* i també la comande perquè no fagi ping a dominis que no existeixen o que no te conexió.

### Implementació d'un nom a un dispositiu de Xarxa:
> Mode de configuració: **Configure Terminal**
```
hostname <nom>
```

### Treure la comprovació de Dominis:
> Mode de configuració: **Configure Terminal**
```
no ip domain lookup
```

### Guardar la configuració del *Router/Switch*:
> Mode de configuració: **Enable**
```
copy running-config startup-config
```

### Assignar una IP a una Interficie/Vlan:
> Mode de configuració: **Configure Terminal**
```
interface <port>
ip address <ip> <mascara>
no shutdown
```

## 1.2 COMANDES D'ACTIVACIÓ DE CONTRASENYES I CONEXIÓ REMOTA (GENERALS)
En aquesta secció enseñarem a com ficar contrasenyas a l'inici de sessió de del *Router/Switch*, per accedir el mode ***Enable*** i també per el **Telnet** i **SSH**.

### Configuració de contrasenya per accedir al *Router/Switch*:
> Mode de configuració: **Configure Terminal**
```
enable password <contrasenya>
line console 0
password <contrasenya>
login
```

### Configuració de contrasenya per accedir al mode **Enable** del *Router/Switch*:
> Mode de configuració: **Configure Terminal**
```
enable secret <contrasenya>
```

### Configuració de contrasenya per accedir desde **Telnet** al *Router/Switch*:
> Mode de configuració: **Configure Terminal**
```
line vty 0 4
password <contrasenya>
login 
```

### Activació de la conexió remota **SSH** al *Router/Switch*:
> Mode de configuració: **Configure Terminal**
```
ip domain-name <domini>
crypto key generate rsa

ip ssh version 2
ip ssh time-out 60
ip ssh authentication-retries 2
line vty 0 4
transport input SSH
```
> [!CAUTION]
> Abans de fer auqesta configuració, necessites que el dispositiu tingui el **Hostname** i el **Telnet** previament configurat. 
> També en cas de no tenir el domini, pots utilitzar aquest: **rto.cisco.com**

##
