---
layout: page
title:  "Práctica 5: Drone Cat and Mouse"
date:   2020-02-11 20:45:14 +01
categories: jekyll update
---

Practica 5 de  Robotica Movil [JdeRobot Academy.](http://jderobot.github.io/RoboticsAcademy/exercises/Drones/drone_cat_mouse)

![Foto1](/assets/image.png)
Dron gato azul, dron raton rojo

Descripcion del ejercicio: Tenemos que controlar un dron para que persiga a otro, el movimiento de este otro es desconocido y muy rápido.

El problema lo dividí en los siguientes subproblemas:
	1. Filtro de color para conocer el punto central del dron raton en la camara
	2. Obtener tambien el ancho del dron raton en pixeles de imagen para conocer la distancia
	3. Usar un control PD para controlar cada aspecto del dron gato, velocidad lineal, velocidad de altura y angulo
	4. Incluir paciencia si el dron gato pierde momentaneamente al dron raton, seguir buscandolo en la misma direccion
	5. Incluir modo busqueda, si el gato pierde al raton se mueve hacia atras hasta verlo

El primer punto fue relativamente sencillo, opencv incluye multiples herramientas para procesar la imagen y conseguir la información buscada. Utilizando los momentos para obtener el punto central, conozco su posicion en la camara.

El hecho de no disponer de un sensor laser para la distancia complicó la manera de conseguirla. Con la camara y el ancho en pixeles del dron raton, se podia aproximar la distancia a la que estaban los drones.

El control PD fue la parte más complicada del ejercicio. Al tener que controlar tres grados de libertad a la vez, el cambio en la constante P o D de un eje afectaba a los demás. Inicialmente con el control P funcionaba de manera muy brusca. Hize un plan mas sencillo para el raton para probar los primeros intentos

Formula control P: u = P * error

[link](https://youtu.be/52wa69ViV9I)

Despues ajustando la constante P, añadiendo un margen para el error y finalmente el componente derivativo del control conseguí que el dron gato funcionara lo suficientemente suave como para seguir al dron raton.

Formula control PD: u = P * error + D * error_incremental

Aun asi, como se puede observar para cabecear el dron gato al moverse hacia atras o adelante se pierde facilmente al raton de la imagen. Por lo que un modo de busqueda de raton era necesario.

Este modo se hizo moviendo el dron gato hacia atras y esperando a ver al dron raton, era necesario una busqueda muy rápida por lo que el uso de la camara ventral lo descarté por la problematica de cambiar de camaras. Usando una sola camara se consigue que el dron gato rapidamente vuelva a seguir al raton.

Finalmente el dron gato puede seguir al dron raton a cierta distancia, sin chocarse con este y sin perderlo. Aún asi los movimientos a tanta velocidad son un poco bruscos.

Video de funcionamiento: [link](https://youtu.be/y4wcACB30rE)