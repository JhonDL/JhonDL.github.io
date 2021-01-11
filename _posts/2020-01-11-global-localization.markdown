---
layout: page
title:  "Práctica 4: Global Localization"
date:   2020-12-12 20:45:14 +01
categories: jekyll update
---

Ejercicio 4 de  Robotica Movil [JdeRobot Academy.](http://jderobot.github.io/RoboticsAcademy/exercises/AutonomousCars/global_navigation/)

![Foto1](/assets/mundo.png)

Descripcion del ejercicio: Tenemos una ciudad, la cual ya se nos entrega mapeada, la idea es navegar el robot a traves de la ciudad a cualquier punto utilizando el algoritmo Gradient Path Planning (GPP). 

El problema lo dividí en los siguientes subproblemas:
	1. Diferenciamos los obstaculos, de las calles en el mapa
	2. Creamos una seria de ondas, que inician en el punto destino, y van autoreplicandose en su frente de onda. Aumentando el valor del punto, por cada replica creada, esto representa la distancia. Se propaga hasta el robot y 10 unidades mas.
	3. Almacenamos una lista de puntos obstaculo que es donde acaban las ondas.
	4. Añadimos penalizacion a los puntos al rededor de los obstaculos.
	5. Iniciando en el robot, hacemos el recorrido tomando los puntos con menor penalizacion, lo cual nos llevara al destino evitando obstaculos.
	6. Finalmente el coche navega siguiendo la ruta establecida.

El primer punto fue relativamente sencillo, en el mapa proporcionado 0 indica obstaculo, y 255 calle. 

El segundo punto fue mas complejo, crear los frentes de onda incrementales lo hice con una serie de bucles for hasta llegar al coche, y aumenté la onda 10 veces mas para conocer que habia al rededor del coche.
El hecho de aumentar la onda 10 veces mas que el coche fue complicado, ya que en determinados puntos la onda llegaba por dos o mas zonas al coche, la solucion paso por iniciar un contador una vez que llegaba la onda al coche.

![Foto1](/assets/problema-onda.png)


La lista de puntos para penalizar fue tambien un paso complicado. Finalmente determine que la penalizacion de los obstaculos sería igual que el punto con valor maximo + 1, asi no dependía de que tan lejos estubiera el coche del destino para que los obstaculos tubieran un valor coherente. La penalizacion fue de 3 pixeles alrededor, el primero igual que el de obstaculo, el segundo de maximo /1.2 y el tercero de maximo/4. Así las penalizaciones tampoco dependían del tamaño del mapa. No añadí mas pixeles de penalización ya que penalizaba la calle entera. En la siguiente imagen se puede ver como sería con 4 pixeles de penalización, penalizaba las calles estrechas casi por completo. 

![Foto1](/assets/problema-penalizaciones.png)

Las penalizaciones se aplicaron de manera perimetral a cada punto obstaculo, comprobando si ese punto tenia un valor penalizado antes de incrementarlo, asi evitaba incrementos dobles que me ocasionara puntos penalizados al rededor de varios obstaculos con mayor valor que el obstaculo en si.

La parte de crear la ruta la hize analizando los 8 pixeles al rededor de cada punto desde el coche, y tomando el de menor valor, creando una lista que sería la ruta de puntos a seguir. A veces se quedaba bloqueado al encontrarse en puntos en los que el pixel posterior tiene el mismo valor que el actual, para evitar este problema a medida que avanza, actualiza el valor del pixel por el que pasa añadiendo 1. 

Finalmente el robot toma en cuenta el punto siguiente y el suyo, y orientandose correctamente hacia el punto, se dirige a cada punto hasta llegar a la meta. Para evitar que este constantemente dando vueltas para posarse en el punto meta exacto. He hecho que el robot de por correcto estar a menos de 4 pixeles de la meta. 

Video de funcionamiento: [link](https://youtu.be/-F_W4i852a4)
