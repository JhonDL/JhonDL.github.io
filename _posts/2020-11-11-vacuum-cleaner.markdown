---
layout: page
title:  "Práctica 2: Vacuum cleaner"
date:   2020-12-12 20:45:14 +01
categories: jekyll update
---

Ejercicio 2 de  Robotica Movil [JdeRobot Academy.](http://jderobot.github.io/RoboticsAcademy/exercises/MobileRobots/vacuum_cleaner)

Descripcion del ejercicio: Tenemos una casa que el robot tiene que limpiar, no tenemos ningun sistema de autolocalizacion. Usaremos el laser y los bumper para hacer un choca-gira pseudoaleatorio, simulando los aspiradores robots actuales de gama entrada. Se puede mejorar implementando diferentes algoritmos para cubrir la maxima superficie, seguir paredes, seguir una espiral, forma de estrella, etc. 

Esta practica ha sido afrontada usando dos metodos diferentes, inicialmente se ha afrontado usando un choca-gira basico. El otro metodo ha sido usando algun algortimo que maximice la superficie limpiada.

Para el primer caso, se ha hecho una maquina de estados que cuando el robot choca, se devuelve un poco y gira de manera aleatoria. 

En el segundo caso se ha usado la misma maquina de estados, incluyendo un modo de cambio de habitacion que se usa despues de pasado cierto tiempo, de esta manera el robot limpia varias zonas de la casa. 

