---
layout: page
title:  "Práctica 3: Obstacle avoidance"
date:   2020-12-12 20:45:14 +01
categories: jekyll update
---

Ejercicio 3 de  Robotica Movil [JdeRobot Academy.](http://jderobot.github.io/RoboticsAcademy/exercises/AutonomousCars/obstacle_avoidance)

![Foto1](/assets/circuito.png)

Descripcion del ejecicio: Tenemos un circuito, con una serie de objetivos y obstaculos, la idea es que el robot (en este caso un coche) avance y no colisione con los obstaculos o paredes. 

Esta practica ha sido afrontada utilizando un algoritmo de navegacion local basado en VFF. 

El problema lo dividi en los siguientes subproblemas: 
	1. Usamos el laser para detectar obstaculos
	2. Creamos un vector obstaculo
	3. Creamos un vector objetivo
	4. Usamos la formula de VFF para crear un vector media.
	5. Ajustamos las constantes para que el sistema funcione de manera fluida y sin colisiones


La primera parte fue la que mas tiempo me llevó. 

Primero eliminé los infinitos del laser (cuando no colisionaba con nada)
El siguiente paso fue hacer vectores con los objetos que el laser detectaba y hacer una media de este. El problema era que esto nos creaba un vector que apuntaba hacia una media de objetos. y queremos evitarlos. 

La solucion fue utilizar la funcion inversa en las distancias para crear un vector que indica una direccion y modulo que evita obstaculos.
d = (1/d)

![Foto1](/assets/form1.png)

En este momento intenté reforumular esta formula para dar aún mas importancia a los objetos cercanos. Lo intenté con la funcion exponencial d=e^(1/x) pero no evadia lo suficiente los objetos lejanos, y para los cercanos daba cambios de sentido muy bruscos.

![Foto1](/assets/form2.png)

La solucion paso por poner una constante en la funcion inversa d=(6/d) de esta manera, tenian aun mas peso los objetos cercanos. 

![Foto1](/assets/form3.png)

Con esto tenía solucionado el vector obstaculo. 

El vector objetivo fue bastante sencillo calculando la posicion absoluta del objetivo y del robot, y pasandolo la posicion relativa del robot. 
Este vector necesitaba tener un maximo ya que si no, demasiada distancia suponia que el robot tomaba demasiados riesgos, para esto calculé el modulo de este vector y le puse un maximo.

Con la formula de VFF
Fresultante = a*Fatractiva + b*Frepulsiva
siendo,
Fatractiva = vector objetivo
Frepulsiva = vector obstaculo
a = 1,7
b = 0.8

Ya estaba solucionado el algoritmo de navegacion local, los motores del robot tenian que seguir este vector.
Para acelerar el robot, utilizé una maquina de estados, en la que reducia la velocidad dependiendo del angulo que debia de girar el robot, y/o la fuerza repulsiva que tenia. 

Video de funcionamiento: [link](https://youtu.be/DJ5CH-dF5FM)