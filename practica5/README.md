# Monte Carlo Laser Localization

## 1. Descripción General
He implementado un algoritmo de localización probabilista basado en el filtro de partículas (Monte Carlo). El objetivo ha sido estimar la posición del robot en un mapa conocido, usando un sensor láser y un modelo de movimiento con ruido. Mi enfoque consiste en:

1. **Inicializar** aleatoriamente un conjunto de partículas en todo el espacio libre.  
2. **Propagar** las partículas con la diferencia de la pose real del robot (y un ruido gaussiano).  
3. **Calcular pesos** comparando el láser real con un láser teórico generado por ray tracing.  
4. **Re-muestrear** las partículas, manteniendo las que tienen mayor probabilidad de ser la pose correcta.

## 2. Cálculo de Pesos
Para cada partícula, simulo un láser virtual: transformo la pose de la partícula a coordenadas de mapa, lanzo rayos en varios ángulos y detengo cada rayo al chocar con un obstáculo o al llegar a la distancia máxima. Comparo esa medición teórica con la lectura real del láser del robot usando una probabilidad gaussiana (con cierta sigma). Las partículas cuyas mediciones virtuales se parecen más a la realidad reciben pesos más altos.

## 3. Inicialización Global
Las partículas no se inicializan alrededor de la pose real del robot. En su lugar:
- Obtengo todas las celdas libres en el mapa.  
- Elijo varias de esas celdas de forma aleatoria.  
- Asigno un ángulo aleatorio a cada partícula.  
- De este modo, se lleva a cabo una localización “global” al cubrir todo el espacio libre.

## 4. Parámetros
- **Número de partículas**: probé con 100, 300 y 400. Con 100 va más rápido pero es menos robusto; con 300 o 400 se garantiza mejor convergencia a costa de mayor coste computacional.  
- **Número de rayos del láser**: entre 5 y 30. Cuantos más rayos, más precisa la comparación, pero el algoritmo se vuelve más pesado.  
- **Ruido de propagación**: valores típicos de 0.01 para X, Y y algo más para yaw (por ejemplo 0.05).  
- **Sigma** en la comparación láser-real: con 0.3 penalizo más el error, con 0.5 resulta más permisivo.

## 5. Movimiento del Robot
El robot debe moverse para que el láser proporcione lecturas diferentes y las partículas puedan converger:
1. **Movimiento en círculos** (velocidad lineal y angular constantes).  
2. **Bump and go**: ante detección de obstáculo, gira un número de pasos para evitar colisión.

## 6. Dificultades y Soluciones
- **Escala y origen del mapa**: asegurarse de que `poseToMap` y `mapToPose` coincidan con la realidad física.  
- **Penalización de partículas inválidas**: asignar un peso muy bajo a las que caen en obstáculos o fuera de límites.  
- **Entornos simétricos**: el robot debe recorrer distintas zonas para desambiguar su posición.  
- **Control de ruido**: si es muy alto, las partículas se dispersan excesivamente; si es muy bajo, se atascan.

Ajustando cuidadosamente el número de partículas, rayos y ruidos, he logrado un equilibrio entre precisión y coste computacional. 

## 7. Video de Ejecución
He subido un breve vídeo de demostración en el siguiente enlace:  
[Demostración](https://drive.google.com/file/d/1qGuttKFBFiPRd3e37gjSVTAGl_ChAduh/view?usp=sharing)
