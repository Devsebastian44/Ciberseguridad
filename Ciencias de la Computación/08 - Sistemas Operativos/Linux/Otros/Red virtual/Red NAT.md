En VirtualBox podemos conectar las interfaces de red virtuales de una maquina virtual a distintos tipos de redes.

![[Programación/Sistemas Operativos/Linux/Otros/Red virtual/Img/Imagen1.png]]

Una red NAT es una red que crea VirtualBox que permite compartir dicha red con varias máquinas virtuales. Además, VirtualBox con este tipo de red va a proporcionar una puerta de enlace con salida a internet en la dirección de host numero 1 de la red.

## Creando una red NAT

Primero vamos al menú de VirtualBox Archivo Herramientas Network Manager y creamos una nueva red NAT.

![[Programación/Sistemas Operativos/Linux/Otros/Red virtual/Img/Imagen2.png]]

## Configurando las Máquinas Virtuales

Ahora vamos a configurar las interfaces de red virtuales de las maquinas virtuales y poder conectar entre si a través de la red NAT.

![[Programación/Sistemas Operativos/Linux/Otros/Red virtual/Img/Imagen3.png]]