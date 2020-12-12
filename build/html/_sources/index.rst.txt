.. gbot_seeds_v1 documentation master file, created by
   sphinx-quickstart on Sat Dec 12 00:04:09 2020.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Documentacion gbot_seeds
=========================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:

.. image:: ../source/2_.png

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`


.. contents:: 
   :depth: 4

**************************************
Pasos a seguir para iniciar el sistema
**************************************

El sistema cuanta con un robot y un joystick. El robot debe encenderse primero siguiendo los pasos que se detallan en encendido del robot.
Una ves completado los pasos del encendido del robot puede iniciarse el encendido del joystick. Se deben respetar estos pasos si se quiere iniciar correctamente los nodos del sistema

**************************************
Encendido Robot
**************************************

IMPORTANTE
------------

Para encender el robot es necesario, NO OLVIDAR, prender la pequeña llave de precarga que se encuentra en la parte superior de la caja de encendio. Esta palanca se encuentra apagada cuando apunta hacia la caja.

-Verificar que el dock USB se encuentra apagado, si la salida que va hacia la camara USB esta prendida el sistema puede no iniciar de forma correcta

1-Encender la llave de precarga del robot, la palanca debera quedar apuntando hacia afuera. lo que indica que esta prendida (apunta hacia la caja cuando esta apagada)

2-Encender llave de alimentacion general (arriba a la derecha)

3-Encender computadora y espera 30 segundos aproximadamente.

4-Encender resto de las llaves 

5-Encender interruptor camara RGB

.. image:: ../source/1_.png

IMPORTANTE
----------

La llave de encendido de alimentacion (arriba a la derecha) tiene posicion invertida respecto del resto, con lo cual estara encendida cuando apunta hacia abajo. El resto de las llaves estaran encendidas cuando apuntan hacia abajo (sentido inverso)

**********************************************
Conectarse remotamente al robot usando celular
**********************************************

1- desconectar los datos del telefono

2- conectarse al wifi gbot_seeds, la contraseña es "semilleros"

3- Abrir la aplicacion de android JuiceSSH y conectarse a la IP:192.168.1.105 como root, contraseña: odroid 

   Si no esta cargada la conexion se debe seleccionar en conexion rapida y entrar, sino puede utilizarse del menu de las recientes utilizadas

.. image:: ../source/4_.png

4-ejecutar el comando:

::

  sudo systemctl stop robot.service
  sudo systemctl start robot.service

5-esperar 30 segundos a que inicie el sistema ROS del robot.Echo esto puede desconectarse la consola tipeando
   
::
  
  exit

********************************************************
Conectarse remotamente al robot usando Notebook (ubuntu)
********************************************************

1- conectarse al wifi gbot_seeds, la contraseña es "semilleros"

2- Abrir una consola y ejecutar:
::

  ssh -l root 192.168.1.105

3:Introducir la contraseña: odroid


4-ejecutar el comando:

::

  sudo systemctl stop robot.service
  sudo systemctl start robot.service

5-esperar 30 segundos a que inicie el sistema ROS del robot. Echo esto puede desconectarse la consola tipeando

::
  
  exit

**************************************
Chequeo de camaras (solo notebook)
**************************************

Una ves que el robot ha iniciado si todo funciona de forma correcta, deberia levantar todos los perifericos de hardware (ej. camara RGB, camara estereo, control de motores,encoders,etc). Se debe realizar un chequeo de que la camara se encuentra en funcionamiento lo que ademas permitira corregir angulo y posicion de ser necesario.
Para esto sera necesario estar conectado al wifi del robot:

1- conectarse al wifi gbot_seeds, la contraseña es "semilleros"

2-abrir una consola y ejecutar:

2- Abrir una consola y ejecutar:

::

  export ROS_MASTER_URI=http://192.168.1.105:11311
  rosrun rviz rviz rosrun -d /home/javier/Desktop/gbot_seeds.rviz

3-Ejecutado el comando anterior deberia abrirse el entorno de rviz (ROS Visualization) y se deberia mostrar la camara RGB lateral. (ver imagen)

.. image:: ../source/5_.png

Posibles Errores
----------------

-Si cuando se ejecuta el comando del punto 2 aparece el error "UNABLE TO CONNECTO TO THE MASTER", revisar que la red wifi este conectada correctamente al robot.
-Volver a ejecutar (estando dentro de la consola del robot) los siguientes comandos

::

  sudo systemctl stop robot.service
  sudo systemctl start robot.service

**************************************
Iniciar Joystick
**************************************

IMPORTANTE
----------

Asegurarse que antes de encender el interruptor del joystick (llave palanca de la caja blanca) el Joystick de PS3 se encuentra conectado al cable microUSB (ver imagen). Si esto no se hace no funcionara luego y requerira apagar 

.. image:: ../source/3_.png

Pasos a seguir:
---------------

1-Encender la llave palanca de la caja del joystick. Esto iniciara la placa de control del joystick. El sistema puede tardar hasta 1 minuto en encender y se vinculara automaticamente al robot utilizando un topic de ros (/joy)

2-Luego de 1 minuto y habiendo cumplido los pasos del apartado encendido del robot, el joystick deberia autovincularse al robot y de esta forma deberia poder manejarse. 

IMPORTANTE:
-----------

El control tiene un mecanismo de seguridad, si no se aprieta la "x" y se mantiene presionado este boton el robot no se movera. Presionando la "x" y moviendo el stick izquierdo del joystick el robot se movera en proporcion a cuanto se presione el mando.


  
