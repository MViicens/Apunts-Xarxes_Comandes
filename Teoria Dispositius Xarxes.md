# TEORIA SOBRE DISPOSITIUS DE XARXES (Cisco)
## 1. ROUTERS
### 1.1 Tèoria bàsica sobre el Routers
Un router és un dispositiu de xarxa que s'utilitza per interconnectar diferents xarxes informàtiques i dirigir el trànsit de dades entre elles. Les seves funcions principals són:
- **Interconnexió de Xarxes ->** Actua com a punt de connexió entre diferents xarxes, com la xarxa local (LAN) i la xarxa externa (per exemple, Internet).
- **Enrutament de Dades ->** Determina la millor ruta per enviar les dades des de l'origen fins al destí a través de la xarxa, basant-se en l'adreça IP dels dispositius.
- **NAT _(Network Address Translation)_ ->** Permet que múltiples dispositius d'una xarxa compartixin una única adreça IP externa. Tradueix les adreces IP internes a l'adreça IP pública del router.
- **Firewall ->** Ofereix funcions de seguretat filtrant i controlant el trànsit de dades, bloquejant o permetent l'accés segons les regles establertes.
- **Gestió d'Amplada de Banda ->** Pot prioritzar certs tipus de trànsit per optimitzar el rendiment de la xarxa, com l'streaming de vídeo o les trucades VoIP.
- **Administració Remota ->** Permet la configuració i administració del router a través d'una interfície web o aplicacions mòbils, facilitant el control i monitoratge de la xarxa.

### 1.2 Protocols del Router
En el router traballem amb uns protocols que ens son de molta utilitat.
- **RIP ->** Serveix per poder fer un enrutament automàtic, només sapiguent la conexió en la que esta conectada (veïna) ja fara la feina per tu. Però te un problema, i es que no te compte les Mascares de les IPs.
- **RIP Version 2 ->** És practicament igual al RIP version 1, però aquest *'suposadament'* te en compte les màscares de les IPs. 
- **DHCP ->** La seva utilitat es poder donar una IP a qualsevol dispositiu que es conecti a la seva xarxa. També deixa fer reserves de IPs per certes MAC en concret, retocar els rangs *(de quina IP a quina)* i permet fer varies Pools *(diferents configuracions de DHCP)*.
- **Telnet ->** Aquest protocol el que fa és que ens permet podernos conectar remotament al Router, però les dades estan sense xifrar.
- **SSH ->** Fa el mateix que el Telnet, però les seves dades si estan xifrades.

## 2. SWITCHS
### 2.1 Tèoria bàsica sobre els Switchs
Un switch és un dispositiu de xarxa que s'utilitza per connectar diversos dispositius en una xarxa local (LAN) i dirigir el trànsit de dades entre ells. Les seves funcions principals són:
- **Connexió de dispositius ->** El switch connecta diversos dispositius, com ara ordinadors, impressores, servidors, etc., en una xarxa local.
- **Commutació de paquets ->** Un switch envia els paquets de dades rebuts a través de la seva interfície cap a la interfície adequada que condueixi al destinatari, basant-se en l'adreça MAC del dispositiu.
- **Millora de la banda ampla ->** Permet múltiples connexions simultànies sense afectar el rendiment de la xarxa, ja que els ports del switch poden funcionar a la velocitat de la xarxa.
- **Divisió de dominis de col·lisió ->** En les xarxes ambutides amb switches, cada port es considera un domini de col·lisió separat, el que minimitza els problemes de col·lisió i millora l'eficiència de la xarxa.
- **Detecció d'adreces MAC ->** El switch manté una taula d'adreces MAC per identificar els dispositius connectats als seus ports. Això permet encaminar els paquets de dades de manera eficient.
- **VLAN *(Virtual Local Area Network)* ->** Permet la segmentació lògica d'una xarxa física en múltiples xarxes virtuals, aïllant el trànsit entre elles i millorant la seguretat i el rendiment de la xarxa.
- **PoE *(Power over Ethernet)* ->** Alguns switches ofereixen suport per PoE, que permet alimentar dispositius com ara telèfons IP, càmeres de seguretat o punts d'accés Wi-Fi a través del cable Ethernet, sense necessitat de fonts d'alimentació addicionals. *(Aquest últim no ho hem fet, però pot ser util saber)*.

### 2.2.Protocols del Switch
- **STP ->** és un protocol utilitzat en xarxes commutades per evitar bucles. Bloqueja enllaços redundants per assegurar una sola ruta activa entre els commutadors, millorant la fiabilitat i l'eficiència de la xarxa.
- **Telnet ->** Aquest protocol el que fa és que ens permet podernos conectar remotament al Router, però les dades estan sense xifrar.
- **SSH ->** Fa el mateix que el Telnet, però les seves dades si estan xifrades.
