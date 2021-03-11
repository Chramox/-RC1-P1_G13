# Práctica 1

## Integrantes
| Fernando Josue Tello Valiente - 201800714 | Juan Marcos Ibarra Lopez - 201801345 | Jorge Daniel Juarez Aldana - 201807022 | Jose Carlos Jimenez - 201801195 |
|:-------------------------------------------------------------------------------:|:----------------------------------------------------------------------------:|:----------------------------------------------------------------------------------:|:----------------------------------------------------------------------------------:|
| [![](https://github.com/FerJoTello.png?size=150)](https://github.com/FerJoTello)    | [![](https://github.com/Chramox.png?size=150)](https://github.com/Chramox)   | [![](https://github.com/joorgej.png?size=150)](https://github.com/joorgej)   | [![](https://github.com/Jose-Carlos-Jimenez.png?size=150)](https://github.com/Jose-Carlos-Jimenez)   |
| <a href="https://github.com/FerJoTello" target="_blank">`github.com/FerJoTello`</a> | <a href="https://github.com/Chramox" target="_blank">`github.com/Chramox`</a> | <a href="https://github.com/joorgej" target="_blank">`github.com/joorgej`</a> | <a href="https://github.com/Jose-Carlos-Jimenez" target="_blank">`github.com/Jose-Carlos-Jimenez`</a> |


## Descripción
Fue solicitada una infraestructura de red para una compañía, donde se especifica previamente dos topologías de red, y a partir de ellas fue configurada la red para brindar comunicación a los equipos de acuerdo a las necesidades que presentan.

Dicha compañía cuenta con 3 departamentos: **informática**, **contabilidad**, y **ventas**. La comunicación se restringe a los usuarios del mismo departamento y con su servidor web.

A continuación se explica la construcción y configuración realizada.

## Topología
La construcción de la red se realizó con el software **GNS3**, el cual brinda una simulación gráfica del funcionamiento de varios dispositivos de red. También permite virtualizar máquinas para poder trabajar con ellas y tener un ambiente de ejecución más parecido a situaciones reales.

Cada topología fue diseñada en máquinas físicas distintas.

### Topología 1
![Topología1](https://cdn.discordapp.com/attachments/694808399358984302/819367861164310628/unknown.png)

Se configuraron todos los equipos de una infraestructura de red para una empresa la cual cuenta con tres sitios web, uno para cada departamento, los cuales son: 
- Ventas
- Informática
- Contabilidad

Cada departamento cuanta con una VLAN distinta para asegurarse que no exista comunicación entre ellos, garantizando así la seguridad de la información entre cada departamento. Estas VLAN son descritas más adelante.

### Topología 2
![Topología2](https://media.discordapp.net/attachments/733900007299874866/819375413125709845/unknown.png?width=895&height=373)

Cada departamento requiere de un servidor, los cuales son máquinas virtuales con sistema operativo Linux (Ubuntu). En cada una de estas máquinas se encuentra hospedada la página web de cada departamento, las cuales cuentan con un encabezado que las identifica y un tema informativo en específico. La vista de estas páginas se encuentran en el apartado de **Páginas web**.

### Conexión entre topologías
Como se mencionó anteriormente, las topologías se encuentran en máquinas físicas distintas, por lo que es necesario conectarlas de alguna forma. Para ello se utiliza una VPN con conexión UDP, utilizando la herramienta OpenVPN, esto se logra por medio del servicio EC2 de Amazon en el cual se montó una máquina virtual que está situada en el este de Estados Unidos y que sirve como un intermediario entre las dos máquinas físicas.

![OpenVPN funcionando](https://media.discordapp.net/attachments/733900007299874866/819375840232079380/unknown.png?width=335&height=574)


## Parámetros de la red
A continuación se enlista la información de la configuración que se realizó en la red. Considerando que esta práctica pertenece al grupo 13, se encuentran dentro de las IP's el número **13** como se solicitó.
### VLAN
- Informática: 23
- Ventas: 33
- Contabilidad: 43
### IP's
- Informática: 
	- VPC: 192.168.113.30
	- VM: 192.168.113.15
	- Server: 192.168.113.150
- Ventas: 
	- VPC: 192.168.213.30
	- VM: 192.168.213.15
	- Server: 192.168.213.150
- Contabilidad: 
	- VPC: 192.168.13.30
	- VM: 192.168.13.15
	- Server: 192.168.13.150

## Configuración VPC's
![VPC](https://media.discordapp.net/attachments/694808399358984302/819378952345878548/unknown.png?width=541&height=243)

Con el comando **ip** se configuran la IP y Máscara de Red CIDR para las máquinas virtuales simuladas de GNS3.
## Configuración de Switch (VLAN)
![switch vlan](https://cdn.discordapp.com/attachments/733900007299874866/819377300301807666/unknown.png)

En cada switch se configuraron los puertos Ethernet según correspondiera, ya sea añadiendo el puerto a una **VLAN** o cambiando su tipo a truncal.

## Configuración de VPN
![cloud](https://cdn.discordapp.com/attachments/694808399358984302/819380871140081674/unknown.png)

Para conectar las topologías, se indica el puerto local, el host remoto (este lo brinda la VPN) y el puerto remoto. Estas configuraciones se realizan en un objeto **Cloud**.

## Configuración de IP's (Windows)
![switch vlan](https://media.discordapp.net/attachments/694808399358984302/819380445942382662/unknown.png?width=669&height=502)

Las máquinas virtuales con sistema operativo Windows se configuran a través del protocolo **TCP/IPv4** de su respectivo controlador de red.

## Configuración de IP's (Linux)
![OpenVPN funcionando](https://media.discordapp.net/attachments/733900007299874866/819381627615969300/unknown.png?width=466&height=396)

Las máquinas virtuales con sistema operativo Linux (Ubuntu) se configuran a través del protocolo **TCP/IPv4** de su respectivo controlador de red.

## Páginas web
Cada página web contiene un encabezado con la información del departamento, el grupo, sus integrantes, y un tema desarrollado relacionado al curso de Redes de Computadoras 1. A continuación se muestran unas imágenes de las páginas web.
### Departamento Informática
El tema de la página del departamento de informática es el de **Subsistemas de cableado estructurado**.
![Página de Informática](https://media.discordapp.net/attachments/694808399358984302/819374109254483968/unknown.png?width=895&height=414)
### Departamento Ventas
El tema de la página del departamento de informática es el de **Redes punto a punto**.
![Páginas de Ventas](https://media.discordapp.net/attachments/694808399358984302/819374319351889940/unknown.png?width=895&height=410)
### Departamento Contabilidad
El tema de la página del departamento de informática es el de **Red multipunto**.
![Página de Contabilidad](https://media.discordapp.net/attachments/694808399358984302/819373993982296115/unknown.png?width=895&height=409)
