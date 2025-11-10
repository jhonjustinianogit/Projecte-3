# Solució: T04: Serveis de directori. LDAP

## 1. Objecte de l'Encàrrec

L'objecte del present Plec és la instal·lació, configuració i validació d'un servei OpenLDAP en un entorn virtualitzat basat en Ubuntu Server. Aquest servei s'ha de configurar per actuar com a directori centralitzat d'usuaris i grups per al domini de proves innovatechXX.test.

## 2. Requeriments d'Infraestructura Inicial
El consultor ha de verificar la correcta configuració de la infraestructura virtual abans d'iniciar la implementació:

## 2.1. Configuració de la màquina Server (Server Hostname). 
"server.innovatechXX.test"

- Primero entramos a la configuración ejecutando el comando: 

![foto1](img/T1.png)

- Una vez entramos hemos de configurar y poner el Server Hostname y ponemos server.innovatech14.test server 

![foto2](img/T2.png)

- Para asegurarnos que lo hemos hecho bien, ejecutamos el comando hostname y hostname -f

![foto3](img/T3.png)

## 2.2. Interfície de Xarxa Pública.
"NAT (Per accés a Internet i descàrrega de paquets)"

- Para poner red en NAT salimos de la máquina virtual y en virtualbox nos vamos a la configuración y en el apartado de red en adaptador 1 ponemos red NAT

![foto4](img/T4.png)

## 2.3. Interfície de Xarxa Privada.
"Host-Only (Per a comunicació privada amb el Client virtual  i la màquina física)"

- Para poner una segunda red, igual que antes entramos a la configuración y en red habilitamos el segundo adaptador y ponemos adaptador de solo anfitrión

![foto5](img/T5.png)

- Después hacemos el siguiente comando para entrar a la configuración y habilitar y configurar el segundo adaptador que es de sólo anfitrión, el comando es: 

![foto6](img/T6.png)

- Una vez dentro ponemos el segundo adaptador lo hacemos poniendo enp0s8 y más abajo ponemos dhcp4: true para que se habilite. 

![foto7](img/T7.png)

- Guardamos los cambios y hacemos la comanda sudo netplan apply para aplicar los cambios

![foto8](img/T8.png)

- Después de eso por último hacemos la comanda ip a para ver las ips 

![foto9](img/T9.png)

## 3. Tasques d'Implementació i Configuració del Servidor LDAP
"La Consultora EverPia ha de complir estrictament amb les següents tasques d'instal·lació i configuració:"

## 3.1. Instal·lació i Configuració Base d'OpenLDAP

## 3.1.1. Instal·lació del servei OpenLDAP.
"S'ha de mostrar el resultat de la comanda slapcat per validar la instal·lació base"

- Para instalar ejecutamos la siguiente comanda:

![foto10](img/T10.png)

- Nos pedirá que pongamos una contraseña a la cuál le ponemos usuari.

![foto11](img/T11.png)

![foto12](img/T12.png)

- Una vez instalado tenemos que comprobar que esté activo y en funcionamiento, lo hacemos ejecutando la siguiente comanda:

![foto13](img/T13.png)

![foto14](img/T14.png)

- Ahora que ya hemos visto que está activo y en funcionamiento, comprobamos que el directorio se ha creado con el nombre que queremos, para eso hacemos la comanda: sudo slapcat

![foto15](img/T15.png)

## 3.1.2. Configuració de la base de dades.
"Nom del Domini: innovatechXX.test"

- Para poner el nombre del dominio tenemos que reconfigurar, para eso ejecutamos la siguiente comanda para reconfigurar:

![foto16](img/T16.png)

- Una vez le demos a reconfigurar nos saldrá un mensaje, al cuál le tenemos que decir “que no queremos cancelar la configuración” por tanto le tenemos que dar al “NO”

![foto17](img/T17.png)

- Después le tenemos que poner el nombre correspondiente al directorio que queremos crear, en este caso ponemos: innovatech14.test” 

![foto18](img/T18.png)

- Después ahora sí que hemos de poner el nombre de la organización, que también le he puesto innovatech14.test

![foto19](img/T19.png)

## 3.1.3. Configuració de la contrasenya d'administrador.
"Contrasenya: p@ssw0rd"

- Ponemos la contraseña, que en este caso tiene que ser y por tanto ponemos: p@ssw0rd

![foto20](img/T20.png)

- Después nos pedirá que pongamos nuevamente para confirmar y por supuesto también ponemos: p@ssw0rd

![foto21](img/T21.png)

- Después le tenemos que dar a “si” por que lo que nos dice es que cuando se elimine el paquete también se elimine la BD creada 

![foto22](img/T22.png)

- Después le damos a “si” también por que lo que nos dice es que si queremos mover la base de datos antigua, por tanto le damos a “si” para que se nos mueva la información del directorio existente a una carpeta backup

![foto23](img/T23.png)

- Por último compramos que se ha modificado la información del directorio y para que este bien

![foto24](img/T24.png)

## 3.1.4. Creació d'Unitats Organitzatives (OU) inicials.
"S'han de crear dues OUs: users i groups mitjançant un fitxer .ldif"

- Para crear la OU hacemos la siguiente comanda:

![foto25](img/T25.png)

- Después tenemos que poner lo que pone en la imagen, que es para crear la OU de users y de groups

![foto26](img/T26.png)

- Por último lo agregamos con la comanda siguiente:

![foto27](img/T27.png)

## 3.1.5. Validació de les Unitats Organitzatives.
"Realitzar una consulta amb ldapsearch que mostri totes les OUs creades al directori"

- Para que nos muestre todos los resultados, tenemos que hacer la siguiente comanda: ldapsearch -xLLL  -b “dc=innovatech14,dc=test” ou=*. “Con el ou=* le estamos diciendo que nos muestre la OU creada anteriormente”.

![foto28](img/T28.png)




