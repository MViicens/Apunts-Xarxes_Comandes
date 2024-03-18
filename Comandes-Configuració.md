# 1. COMANDES GENERALS I SHOWS
## 1.1 COMANDES BÀSICAS
Basicament, aqui s'ensenya com ficar un **Nom** al *Router/Switch* i també la comande perquè no fagi ping a dominis que no existeixen o que no te conexió.

### Implementació d'un nom a un dispositiu de Xarxa
> Mode de configuració: **Configure Terminal**
```
hostname <nom>
```

### Treure la comprovació de Dominis
> Mode de configuració: **Configure Terminal**
```
no ip domain lookup
```

### Guardar la configuració del *Router/Switch*
> Mode de configuració: **Enable**
```
copy running-config startup-config
```

### Assignar una IP a una Interficie/Vlan
> Mode de configuració: **Configure Terminal**
```
interface <tipu> <port>
ip address <ip> <mascara>
no shutdown
```
> [!NOTE]
> Hi han diferents tipus de ports, aquest són els que hem tractat nosaltres:
> - **Serial -->** *serial 0/0/0*
> - **Fast -->** *FastEthernet 0/0*
> - **Giga -->** *GigaEthernet 0/0*

## 1.2 COMANDES D'ACTIVACIÓ DE CONTRASENYES I CONEXIÓ REMOTA
En aquesta secció enseñarem a com ficar contrasenyas a l'inici de sessió de del *Router/Switch*, per accedir el mode ***Enable*** i també per el **Telnet** i **SSH**.

### Configuració de contrasenya per accedir al *Router/Switch*
> Mode de configuració: **Configure Terminal**
```
enable password <contrasenya>
line console 0
password <contrasenya>
login
```

### Configuració de contrasenya per accedir al mode **Enable** del *Router/Switch*
> Mode de configuració: **Configure Terminal**
```
enable secret <contrasenya>
```

### Configuració de contrasenya per accedir desde **Telnet** al *Router/Switch*
> Mode de configuració: **Configure Terminal**
```
line vty 0 4
password <contrasenya>
login 
```

### Activació de la conexió remota **SSH** al *Router/Switch*
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

## 1.3 VISUALITZACIÓ DE PARÀMETRES
En aquesta secció s'ensenyen les comandes per poder veure les configuracións que estem fent o ja venien configurades al *Router/Switch*.

### Visualitzar la configuració (ACTUAL)
> Mode de configuració: **Enable**
```
show running-config
```

### Visualitzar la configuració (AMB LA QUE ARRANCA EL DISPOSITIU)
> Mode de configuració: **Enable**
```
show startup-config
```

### Visualitzar la Taula d'Enrutament
> Mode de configuració: **Enable**
```
show ip route
```
> [!NOTE]
> Al ensenyar la taula, surten unes lletres al costat de les IPs, aquesta es la forma de interpretar-ho:
> - **C -->** Interficie directament conectada.
> - **S -->** Ruta estàtica.
> - **S * -->** Ruta estàtica per defecte.

### Visualitzar el Estat de les Interficies
> Mode de configuració: **Enable**
```
show ip interface brief
```

### Visualitzar la Configuració dels dispositius que estant Directament Conectats
> Mode de configuració: **Enable**
```
show cdp neighbors detail
```

### Visualitzar la llista de IPs proporcionades amb les MACs
> Mode de configuració: **Enable**
```
show ip dhcp binding
```
> [!TIP]
> Una altre comanda que et pot ser útil és: `show ip dhcp server statistics`. El que fa és mostra informació relacionada amb el nombre de missatges DHCPv4 que s'han enviat i rebut.


# 2. COMANDES PER CONFIGURACIÓ DE UN ROUTER
## 2.1 CONFIGURACIÓ DEL ENRUTAMENT
Ara que ja hem fet lo bàsic, ara entrarem amb totes les comandes per el **Router**.

### Configuració amb RIP:
> Mode de configuració: **Configure Terminal**
```
router rip
network <nom_xarxa>
```
> [!NOTE]
> El protocol RIP versió 1, **NO** té en compte les màscaras. El format de la IP, `<nom_xarxa>`, ha de ser com el següent:
> - **Exemple 1 -->** *192.168.1.0*
> - **Exemple 2 -->** *10.0.0.0*

### Configuració amb RIP Versió 2:
> Mode de configuració: **Configure Terminal**
```
router rip
version 2
network <nom_xarxa>
```
> [!NOTE]
> El protocol RIP versió 2, **SI** té en compte les màscaras. El format de la IP, `<nom_xarxa>`, ha de ser com el següent:
> - **Exemple 1 -->** *192.168.2.0*
> - **Exemple 2 -->** *12.0.0.0*

### Configuració amb Enrutament Estàtic:
> Mode de configuració: **Configure Terminal**
```
ip route <nom_xarxa> <mascara> <desti>
```
> [!NOTE]
> Per aclar una mica el enrutament estàtic, teniu la següent llegenda:
> **<nom_xarxa>:** El nom de la xarxa que volem trobar.
> **<mascara>:** La màscara de la xarxa que busquem.
> **<desti>:** Per on ha da pasar el router per trobar la xarxa desti *(Ha de sert la IP del següent salt, ho sigui que un Router conectat directament al nostre Router)*.

## 2.2 CONFIGURACIÓ DE SUBPORTS
Aquest apartat és per explicar la configuració de **Subports**, que ens es útil quan hem de configurar **VLANs**.
> Mode de configuració: **Configure Terminal**
```
interface <tipu> <port>.<subport>
encapsulation dot1q <num>
no shutdown
``` 
> [!CAUTION]
> Es important fer un `no shutdown` al **port principal**.

## 2.3 CONFIGURACIÓ DE DHCP

Aquesta configuració **(DHCP)** serveix perquè el Router asigni IPs automàtiques a la teva xarxa, també és pot configurar alguns paràmetres en concret.

### Creació de una Pool DHCP:
> Mode de configuració: **Configure Terminal**
```
ip dhcp pool <nom_rang>
network <nom_xarxa> <mascara>
default-router <ip_gateway>
dns-server <ip_dns>
domain-name <domini>
``` 

### IPs Reservades / IPs Excluides:
> Mode de configuració: **Configure Terminal (DHCP)**
```
ip dhcp excluded-address <ip>
ip dhcp excluded-address <primera_ip> <ultima_ip> 
```
> [!NOTE]
> Aquesta comanda es pot utilizar amb una IP en concret *(primera comanda)* o també pots aplicar-ho en un rang *(segona comanda)*.

# 3. COMANDES PER CONFIGURACIÓ DE UN SWITCH
Ara que ja hem vist lo bàsic i la configuració del router, ara entrarem amb totes les comandes per configurar el **Switch**.

## 3.1 CONFIGURACIÓNS INICIALS
Aquest apartat es centra en la configuració de una IP al Switch i com ficar noms a les VLANs.

### Configuració de una IP a un Switch:
> Mode de configuració: **Configure Terminal**
```
interface <vlan> <num_vlan>
ip address <ip> <mascara>
no shutdown
```
> [!CAUTION]
> En el switch les IP es fiquen a les **VLAN**, **NO** als **PORTS**.

### Assignar un nom a una VLAN:
> Mode de configuració: **Configure Terminal (VLAN)**
```
name <nom>
```

### Configuració de uns Rangs de Ports:
> Mode de configuració: **Configure Terminal**
```
interface range <tipu> <port>-<port>
```

## 3.2 CONFIGURACIÓ DE MODES ALS PORTS
### Port mode Access:
> Mode de configuració: **Configure Terminal**
```
interface <tipu> <port>
switchport mode access
switchport access <vlan> <num_vlan>
```

### Port mode Trunk:
> Mode de configuració: **Configure Terminal**
```
interface <tipu> <port>
switchport mode trunk
switchport trunk allowed <vlan> <num_vlan>,<num_vlan> / <num_vlan>-<num_vlan> 
```
> [!CAUTION]
> Sempre ha de estar la **VLAN 1 incluida**.

## 3.3 SEGURARTAT DEL SWITCH
Aquesta seguretat es vasa en les restriccions que es poden fer als ports del Switch a partir de un filtre de MACs.
> Mode de configuració: **Configure Terminal**
```
interface <tipu> <port>
switchport port-security
switchport port-security mac-address sticky
switchport port-security violation <tipu-proteccio>
switchport port-security mac-address <mac>
```
> [!NOTE]
> Aqui hi ha una llegenda sobre el `<tipu-protecció>`:
> - **restrict -->** Permet el trànsit de dispositius autoritzats, però registra una violació de seguretat.
> - **protect -->** Descarta el trànsit de dispositius no autoritzats sense registrar una violació.
> - **shutdown -->** Apaga el port en cas de violació de seguretat.
