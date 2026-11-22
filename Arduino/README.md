# Arduino – Control de LEDs y pulsadores

## Descripción

Este programa permite controlar dos LEDs mediante dos pulsadores físicos y recibir órdenes desde una interfaz gráfica desarrollada en Processing.

La comunicación entre Arduino y Processing se realiza mediante comunicación serial USB a una velocidad de 9600 baudios.

## Componentes utilizados

- 1 placa Arduino.
- 2 pulsadores.
- 2 LEDs.
- Resistencias para los LEDs.
- Cables de conexión.
- Cable USB.

## Conexiones

| Componente | Pin Arduino |
|---|---|
| Pulsador E1 | Pin digital 2 |
| Pulsador E2 | Pin digital 3 |
| LED L1 | Pin digital 8 |
| LED L2 | Pin digital 9 |

Los pulsadores utilizan la configuración `INPUT_PULLUP`, por lo que deben conectarse entre el pin digital correspondiente y GND.

## Funcionamiento

El programa realiza dos tareas principales:

### 1. Lectura de pulsadores físicos

Arduino lee el estado de los pulsadores mediante `digitalRead()`.

Cuando se presiona E1:
- Se invierte el estado de L1.
- Se actualiza la salida digital del pin 8.
- Se envía el carácter `'1'` a Processing.

Cuando se presiona E2:
- Se invierte el estado de L2.
- Se actualiza la salida digital del pin 9.
- Se envía el carácter `'2'` a Processing.

### 2. Recepción de datos desde Processing

Arduino verifica si hay información disponible mediante `Serial.available()`.

Luego utiliza `Serial.read()` para leer el carácter recibido.

| Dato recibido | Acción |
|---|---|
| `'1'` | Cambia el estado del LED L1 |
| `'2'` | Cambia el estado del LED L2 |

## Comunicación serial

La comunicación se inicializa mediante:

```cpp
Serial.begin(9600);
```

Se utilizan los caracteres `'1'` y `'2'` para identificar las órdenes correspondientes a cada LED.

## Funciones utilizadas

- `pinMode()`: configura los pines como entradas o salidas.
- `digitalRead()`: lee el estado de los pulsadores.
- `digitalWrite()`: controla los LEDs.
- `Serial.begin()`: inicializa la comunicación serial.
- `Serial.write()`: envía información a Processing.
- `Serial.available()`: verifica si hay datos recibidos.
- `Serial.read()`: lee los datos enviados desde Processing.
- `delay()`: introduce una pausa de 200 milisegundos.

## Cómo ejecutar

1. Conectar Arduino a la computadora mediante USB.
2. Abrir el archivo `.ino` en Arduino IDE.
3. Seleccionar la placa Arduino correspondiente.
4. Seleccionar el puerto COM.
5. Cargar el programa en la placa.
6. Cerrar el Monitor Serie antes de ejecutar Processing.

**Importante:** Processing debe utilizar la misma velocidad serial de 9600 baudios.
