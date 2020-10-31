---
layout: page
title:  "Práctica 1: Follow line"
date:   2020-10-28 15:45:14 +01
categories: jekyll update
---

Ejercicio 1 de [JdeRobot Academy.](http://jderobot.github.io/RoboticsAcademy/)

El problema es: dado un escenario, que es una pista de carreras, el cual tiene una linea roja en el medio de toda la carretera. Se tiene que seguir con nuestro robot (en este caso un coche de carreras), la linea roja.

![Foto1](/assets/Ejercicio.png)

Esta práctica ha sido afrontada usando un sistema reáctivo de teoría de control clásica. Se han ido usando diferentes sistemas de control (P, D y PD) y observando los diferentes resultados.

Inicialmente el primer problemas fue detectar la linea roja que hay que seguir.

Para conseguir esto, fue utilizada la libreria OpenCV en Python. De la siguiente manera se consigue detectar la posicion de la linea roja desde la camara:
	1. Creamos una mascara de valores de hsv a filtrar.
	2. Aplicamos la máscara
	3. Pasamos de HSV a GreyScale y aplicamos threshold para quedarnos con una imagen binaria.
	4. Calculamos los momentos de una imagen binaria.
	5. Dados los momentos, calculamos la posicion central en la imagen.

El siguiente problema era empezar a aplicar los diferentes tipos de sistemas de control.

<h3>Utilizando un control P.</h3>

Utilizando la formula 
u = -Kp * e

Este sistema funciona pero solo si la velocidad es muy baja.

Video de funcionamiento: [link](https://youtu.be/-ROnRFohZRg)

<h3>Utilizando un control D.</h3>

u = -Kd * d

Este sistema funciona al doble de velocidad que el control P, sin embargo el coche hace giros muy bruscos y la velocidad no se puede mejorar mucho más.

Video de funcionamiento: [link](https://youtu.be/5PEbRGuIPhY)

<h3>Utilizando un control PD.</h3>

u = -Kp * e + -Kd * d

Este método funciona bastante bien, el mejor tiempo conseguido fue 1:35
Las constantes utilizadas fueron Kp: 0.005 y Kd: 0.0125

Video de funcionameinto: [link](https://youtu.be/KqStwGGt0Y0)

<h3>Otras mejoras:</h3>

<h3>Usando la media de error.</h3>

En la curva mas larga del circuito, el coche va recto, gira, recto, gira, constantemente haciendo movimientos un poco tambaleantes. Se intentará hacer un giro mas fluido utilizando una media de errores cogiendo una muestra de los 5 ultimos errores.

Este sistema no funciona con media de 5, pues el tiempo de respuesta es excesivamente alto. Sin embargo hacer la media de 2 hace que la curvas sean mucho mas fluidas incluso, nos permite elevar un poco la velocidad.

Mejor tiempo con este sistema, 1:03 funcionando muy fluido.

<h3>Estados.</h3>

El siguiente paso fue utilizar un sistema de estados, en el que se acelera mas en una recta, y se ralentiza en las curvas mas cerradas.
De esta manera conseguimos un tiempo mejor funcionando el coche de manera muy fluido.

Utilizando 3 casos, recta, curva abierta y curva cerrada conseguimos maximizar la velocidad.

Mejor tiempo con este sistema, 0:56

Video de funcionamiento: [link](https://youtu.be/m9XaOQkO_kA)

Forzando un poco las velocidades el tiempo se mejora hasta 0:48, pero el coche oscila bastante.

Video de funcionamiento: [link](https://youtu.be/OE7XwsHXRr0)

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
