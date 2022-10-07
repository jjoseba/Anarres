---
layout: post
title:  Configurar Wifi de portátiles antiguos (Linux)
date:   2020-09-21 14:00:00 +0100
categories: linux 
---

Durante el confinamiento, desde [Agua de Mayo](https://asociacionaguademayo.org/) creamos un grupo de apoyo vecinal/red de cuidados para ayudar a familias del barrio que pudiesen encontrarse en situación de desamparo. Entre las distintas necesidades que identificamos, una de ellas fue la falta de ordenadores en algunas familias de cara a la vuelta al curso escolar y la posibilidad de que las clases empezasen con una modalidad online. Organizamos una recogida de ordenadores de segunda mano, con la idea de recuperarlos instalándoles un Linux y todas las herramientas de ofimática, internet y demás que pudiesen hacer falta para su uso en la escuela. 

La respuesta original (mucho más extensa, en inglés) la encontré en los [foros de AskUbuntu](http://askubuntu.com/questions/55868/installing-broadcom-wireless-drivers), traduzco aquí para tenerlo localizado para futuro y por si puede venirle bien a alguien que se maneje regular con el idioma de Chéspir.

<!--more-->

Sin más dilación, estos son los pasos a seguir:

### 1. Conocer el tipo de modelo de tarjeta Broadcom

Hay un montón de adaptadores de red Broadcam diferentes, cada día hay nuevos. La clave para encontrar el driver correcto para cualquier tarjeta de red es encontrar el PCI.ID de la misma. Para ello, en terminal podemos ejecutar el siguiente comando:

```
lspci -nn -d 14e4:
```

Esto devuelve algo parecido a lo siguiente si tienes un adaptador Broadcom (el ID 14e4 del ejemplo es en la mayoría de los casos el de las tarjetas inalámbricas):
```
Broadcom Corporation BCM4306 802.11bgn Wireless Network Adapter [14e4:4320] (rev 03)
```

El PCI.ID en este ejemplo es **14e4:4320** como se puede ver entre corchetes. En algunos casos especiales también será necesaria la revisión concreta del controlador (que aparece entre paréntesis). Con lo que ya tenemos identificado que nuestro adaptador de red es `[14e4:4320] (rev 03)`.


### 2. Actualizar el sistema

Como probablemente se trate de una instalación nueva, lo primero actualizaremos la lista de paquetes del sistema, y la lista de PCI.IDs, por si han aparecido nuevos IDs de Broadcom desde que se compiló la distribución de Linux que se ha instalado en la máquina:

    sudo apt update
    sudo update-pciids

Ahora, utilizando el PCI.ID que encontramos antes, tenemos que buscarlo en la lista de debajo para encontrar el método para instalar el driver asociado. Ahora simplemente tocaría quedarse con el nombre del paquete que necesitamos, en el caso del ejemplo podemos ver que el paquete a instalar es  `firmware-b43-installer` (específico de Broadcom) y el paquete `linux-firmware` (para hacerse cargo de otros drivers relacionados).


    PCI.ID      	    18.04 LTS 	 	                 20.04+
    ------------------------------------------------------------------------------------
    14e4:0576	    	Special Case                      UNKNOWN      
    14e4:1713  	    	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4301  	    	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4306	    	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4306 rev 02	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4306 rev 03	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4307	    	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4311	    	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4311 rev 01   	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4312	        firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4313	    	firmware-b43-installer            firmware-b43-installer / linux-firmware      		   
    14e4:4315       	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4315 rev 01    firmware-b43-installer            firmware-b43-installer / linux-firmware
    14e4:4318	        firmware-b43-installer            firmware-b43-installer / linux-firmware      		    
    14e4:4318 rev 02    firmware-b43-installer            firmware-b43-installer / linux-firmware      		    
    14e4:4319	        firmware-b43-installer            firmware-b43-installer / linux-firmware      		   
    14e4:4320 rev 02	firmware-b43-installer            firmware-b43-installer / linux-firmware      		   
    14e4:4320 rev 03	firmware-b43-installer            firmware-b43-installer / linux-firmware      		
    14e4:4321	    	firmware-b43-installer            firmware-b43-installer / linux-firmware  
    14e4:4324           firmware-b43-installer            firmware-b43-installer / linux-firmware      	
    14e4:4325		    firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4328		    firmware-b43-installer            firmware-b43-installer / linux-firmware
    14e4:4328 rev 03	bcmwl-kernel-source               bcmwl-kernel-source      
    14e4:4329		    bcmwl-kernel-source	              bcmwl-kernel-source        
    14e4:432a	       	bcmwl-kernel-source	              bcmwl-kernel-source        
    14e4:432b           bcmwl-kernel-source	              bcmwl-kernel-source        
    14e4:432c  	       	bcmwl-kernel-source	              bcmwl-kernel-source        
    14e4:432d	    	bcmwl-kernel-source	              bcmwl-kernel-source       
    14e4:4331	    	firmware-b43-installer            firmware-b43-installer / linux-firmware          
    14e4:4335	    	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4350	    	firmware-b43-installer            firmware-b43-installer / linux-firmware  
    14e4:4353	    	Special Case 		              UNKNOWN        
    14e4:4353 rev 01   	Special Case 		              UNKNOWN                 
    14e4:4357	    	Special Case 		              UNKNOWN        
    14e4:4358	    	bcmwl-kernel-source	              bcmwl-kernel-source
    14e4:4359	    	firmware-b43-installer	          firmware-b43-installer / linux-firmware       
    14e4:4360	    	firmware-b43-installer            firmware-b43-installer / linux-firmware    
    14e4:4365	    	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    14e4:4365 rev 01	bcmwl-kernel-source               bcmwl-kernel-source      
    14e4:43a0 	    	bcmwl-kernel-source	              bcmwl-kernel-source
    14e4:43ae rev 02    UNKNOWN                           UNKNOWN  	  
    14e4:43b1 	    	bcmwl-kernel-source	              bcmwl-kernel-source      	 
    14e4:43b1 rev 03    bcmwl-kernel-source               bcmwl-kernel-source              
    14e4:43c3 rev 04    UNKNOWN                           firmware-b43-installer / linux-firmware                      
    14e4:4727	    	bcmwl-kernel-source		          bcmwl-kernel-source        
    14e4:4727 rev 01   	Special Case                      Special Case         
    14e4:a962	    	firmware-b43-installer            firmware-b43-installer / linux-firmware      
    ------------------------------------------------------------------------------------


### 3. Instalar el paquete 

>  **Importante** - Si habías intentado instalar manualmente los drivers por otros medios alternativos, es necesario revertir cualquiera de esos cambios para evitar posibles conflictos, incluyendo ficheros de configuración modificados o paquetes de drivers instalados a través de `apt-get` u otro gestor de paquetes.

Vale, ahora simplemente necesitamos instalar el paquete. En el caso de que tengamos la posibilidad de conectar un cable ethernet al ordenador, el proceso será sencillo, ya que podemos utilizar el gestor de paquetes para descargarlo de forma online como haríamos normalmente:

    sudo apt install firmware-b43-installer
    sudo apt install linux-firmware

Para todos los casos hay que instalar el paquete `linux-firmware`. Este paquete siempre estará al día con los últimos drivers Broadcom en conjunción con los binarios específicos que hayas necesitado dependiendo del PCI.ID del driver. Una vez hecho esto, solo queda reiniciar para que se apliquen los cambios:

    sudo reboot

En algunos casos excepcionales, si después de instalar el paquete `firmware-b43-installer` el controlar continúa sin funcionar correctamente, habrá que eliminar el módulo `b43`, volver a activarlo e incluso desbloquearlo con `rfkill`:

     sudo modprobe -r b43
     sudo modprobe b43    
     sudo rfkill unblock all  

En el caso de no disponer de la opción de conectar el ordenador a internet usando un cable ethernet la cosa se complica un poco, haciendo falta un nivel un poco mayor del básico de administración de Linux:

* Para el paquete `firmware-b43-installer` ver [esta respuesta](https://askubuntu.com/a/730813/167850).
* Para `bcmwl-kernel-source`, hay que seguir [este proceso](https://askubuntu.com/questions/626642/how-to-install-broadcom-wireless-drivers-offline/626653#626653) (aviso, un poco farragoso).
