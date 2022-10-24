author: Álvaro Ramos Albertos
summary: Resumen del CodeLab
id:Proyecto2
categories: codelab, markdown
enviroments: web
status: published
feedback link: un enlace en el que los usuarios puedan darte feedback (quizás creando un issue en un repositorio de git)
analytics account: ID de Google


## Introducción
En esta guía configuramos un sistema informático para que un actor malicioso no pueda alterar la secuencia de arranque con fines de acceso ilegítimo
## Ocultación del arranque
Vamos a ocultar el arranque del GRUB2 para que ningún usuario pueda seleccionar ninguna opción. 
En una terminal metemos su -root 
A continuación metemos nano /etc/default/grub y abrimos el archivo de configuración del grub
Cambiamos la opción GRUB_TIMEOUT=5 por GRUB_TIMEOUT=0 y nos debe quedar algo asi

Guardamos con control O y salimos con control z
## Contraseña de arranque
En este apartado ponemos una contraseña para que solo pueda arrancar el GRUB un superusuario
Modificamos el archivo /etc/grub.d/40_custom metiendo set superusers="root" y password root (PASS)
Ciframos la contraseña con grub -mkpasswd-pbkdf2 y también podemos editar los permisos para que solo se modifique con un root con chmod 700 /etc/grub.d/40_custom

## Copia de seguridad
En este paso tenemos que realizar un tar en los archivos de configuración del arranque metiendo lo siguiente:
	tar -cvf /etc/default/grub grub.tar
	tar -cvf /etc/grub.d/40_custom 40_custom.tar

## Otras opciones de seguridad
Esta opción se realiza al principio de la instalación, en los primeros parámetros que podemos tocar, aunque es una opción secundaria. 
Iniciamos una  partición manual seleccionando el disco de nuestra máquina y creando una tabla de particiones. 
Seleccionamos el espacio libre y una prueba con la raiz /boot para una partición con todo lo necesario para el arranque. 
Ponemos tambien una partición para /swap, /, /home y /var
Ciframos las particiones dandole a configurar los volúmenes cifrados y seguimos para alante. 
