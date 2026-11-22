# Processing – Interfaz gráfica y comunicación con Arduino

## Descripción

Este programa desarrolla una interfaz gráfica interactiva en Processing que permite controlar dos LEDs conectados a una placa Arduino mediante comunicación serial USB.

La interfaz permite enviar órdenes a Arduino mediante clics del mouse y visualizar los cambios de estado de los LEDs mediante indicadores gráficos.

También recibe información desde Arduino cuando se presionan los pulsadores físicos.

## Tecnologías utilizadas

- Processing.
- Biblioteca `processing.serial`.
- Comunicación serial USB.
- Arduino.

## Interfaz gráfica

La ventana tiene una resolución de 640 x 360 píxeles y contiene:

- Dos botones virtuales: E1 y E2.
- Dos indicadores circulares: L1 y L2.

Los indicadores cambian de color según el estado de cada LED:

| Indicador | Encendido | Apagado |
|---|---|---|
| L1 | Verde | Gris |
| L2 | Rojo | Gris |

## Funcionamiento

El programa realiza dos tareas principales:

### 1. Recepción de datos desde Arduino

Processing verifica si hay información disponible mediante:

```java
myPort.available()
```

Cuando recibe un carácter desde Arduino, utiliza:

```java
myPort.read()
```

Los caracteres recibidos permiten actualizar los indicadores gráficos:

| Dato recibido | Acción |
|---|---|
| `'1'` | Cambia el estado visual de L1 |
| `'2'` | Cambia el estado visual de L2 |

### 2. Envío de datos hacia Arduino

La interfaz detecta los clics del mouse sobre los botones E1 y E2.

Cuando se hace clic en E1:
- Se detecta la posición del mouse.
- Se identifica el botón seleccionado.
- Se envía el carácter `'1'` a Arduino.
- Se actualiza el indicador visual L1.

Cuando se hace clic en E2:
- Se detecta la posición del mouse.
- Se identifica el botón seleccionado.
- Se envía el carácter `'2'` a Arduino.
- Se actualiza el indicador visual L2.

## Funciones principales

- `setup()`: configura la ventana gráfica y establece la conexión serial.
- `draw()`: actualiza continuamente la interfaz y procesa los datos recibidos.
- `enRect()`: verifica si el cursor del mouse se encuentra dentro de un rectángulo.
- `cuatrobotones()`: dibuja los botones y los indicadores, y detecta los clics.

## Comunicación serial

Se utiliza la biblioteca:

```java
import processing.serial.*;
```

La conexión se establece mediante:

```java
myPort = new Serial(this, portName, 9600);
```

La velocidad de comunicación es de 9600 baudios, igual que en Arduino.

Para seleccionar el puerto serial se utiliza:

```java
Serial.list()[0]
```

El índice debe corresponder al puerto COM donde está conectado Arduino.

## Cómo ejecutar

1. Conectar Arduino a la computadora mediante USB.
2. Cargar previamente el programa correspondiente en Arduino.
3. Cerrar el Monitor Serie del IDE de Arduino.
4. Abrir el archivo `.pde` en Processing.
5. Verificar que el puerto serial seleccionado corresponda al Arduino.
6. Ejecutar el programa.

**Importante:** Si aparece el error `ArrayIndexOutOfBoundsException`, verificar que Processing detecte correctamente los puertos seriales disponibles mediante:

```java
println(Serial.list());
```

## Objetivo

Aplicar la comunicación serial entre Processing y Arduino mediante una interfaz gráfica interactiva, integrando el control de salidas digitales, la lectura de entradas físicas y la visualización de estados.
