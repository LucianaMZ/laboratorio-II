Sistema Automatizado de Clasificación de Objetos por Ciclos
Este proyecto consiste en una celda de manufactura robotizada desarrollada en CoppeliaSim, diseñada para la generación, transporte, manipulación y conteo de cubos de distintos colores (Rojo, Amarillo y Azul) de manera secuencial y automatizada.

🚀 Arquitectura del Sistema
El sistema se divide en cuatro módulos principales interconectados mediante scripts de Lua:

1. Generador de Suministros (Spawner)
Ubicado en el origen de la línea, este módulo se encarga de la creación dinámica de la materia prima.

Función: Clona un objeto base (CuboBase) cada 15 segundos.

Lógica de Color: Utiliza un array de colores para asignar tonos Rojo, Amarillo y Azul de forma rotativa.

Parámetros: Cambia las propiedades del objeto de estático a dinámico para permitir la interacción física.

2. Brazo Robot 1 (Recolección y Alimentación)
Controla un brazo con una garra RG2 para alimentar la línea principal.

Detección: Sensor de proximidad externo que activa el ciclo de movimiento.

Control de Tiempo: Implementa una máquina de estados basada en el tiempo de simulación (sim.getSimulationTime).

Manipulación: Utiliza el concepto de "emparentamiento" (setObjectParent) para sujetar el cubo y moverlo entre cintas transportadoras.

3. Brazo Robot 2 (Clasificador Secuencial)
Es el núcleo lógico del proceso de separación.

Algoritmo de Clasificación: A diferencia de un sensor de color, este brazo utiliza un Contador de Ciclos.

Secuencia: 1.  Cubo 1 ➡️ Posición Caja Azul.
2.  Cubo 2 ➡️ Posición Caja Roja.
3.  Cubo 3 ➡️ Posición Caja Amarilla.

Reinicio: Al completar el tercer cubo, el contador vuelve a 1, permitiendo un flujo infinito.

4. Estaciones de Depósito (Sensores de Conteo)
Tres estaciones finales equipadas con sensores de proximidad independientes.

Lógica de Flanco: Detecta el paso de "nada" a "objeto" para evitar conteos múltiples de un mismo cubo.

Feedback: Informa en tiempo real a través de la consola y la barra de estado de CoppeliaSim la cantidad acumulada en cada caja.

🛠️ Tecnologías Utilizadas
Simulador: CoppeliaSim (V-REP).

Lenguaje: Lua.

Actuadores: Motores de revolución (Joints) y pinza neumática RG2.

Sensores: Sensores de proximidad de tipo Rayo (Ray type).

📋 Instrucciones de Ejecución
Abrir la escena en CoppeliaSim.

Asegurarse de que los nombres de los objetos coincidan con las rutas definidas en los scripts (/SensorCR, /SensorCAM, /SensorCAZ, etc.).

Presionar el botón Play.

Observar el progreso en la Consola de Mensajes y la Barra de Estado inferior.

🧑‍💻 Autor
Luciana Mariel Zapana Examen Final de Robótica / Tecnica Universitaria en Automatización y Robótica 2026
