# Investigación de Hardware - Equipo 3

## 1. Plataforma Base: ESP32 + LoRa

El ESP32 es un microcontrolador de bajo costo y muy bajo consumo de energía que incluye Wi-Fi y Bluetooth. Posee un procesador de doble núcleo, superando ampliamente a las placas Arduino tradicionales en versatilidad. En este proyecto, se combina con un chip LoRa para permitir la comunicación a larga distancia. Es compatible con el ecosistema Meshtastic que se planea implementar para la red mesh.

**Módulos considerados:** Se evalúan dispositivos como el Lilygo T-Beam o T-Echo. El T-Beam es muy usado porque ya integra el ESP32, el chip LoRa y un módulo GPS en una sola placa, reduciendo fallas en conexiones manuales.

## 2. Sensores Ambientales

Para cumplir con el objetivo de la Etapa 6 (Telemetría ambiental), se integrarán sensores climáticos. El sensor **BME280** es el más recomendado por su capacidad de medir temperatura, humedad y presión atmosférica mediante el protocolo I2C (solo 2 cables de datos). Son componentes diseñados para operar con bajo consumo, fundamentales para los repetidores solares autónomos.

**Conexión:** Estos sensores suelen usar protocolos de comunicación como I2C o SPI, que el ESP32 maneja fácilmente.

## 3. Posicionamiento: GPS en la Montaña

**Función:** El GPS permite obtener las coordenadas exactas (latitud y longitud) del puestero. Esta información se envía por la red LoRa para que, en caso de emergencia, se sepa dónde buscar. Se deben priorizar módulos con *Hot Start* rápido para minimizar el consumo de batería en campo. Módulos como el **NEO-6M** son estándar y compatibles con el ESP32.

**Desafío:** En los cañones profundos de Malargüe, la señal de los satélites puede ser difícil de captar. Por eso, el hardware debe tener una antena GPS con buena sensibilidad.

## 4. Protección Física: Carcasas y Estanqueidad

**IP67:** Los dispositivos deben estar protegidos por cajas estancas con certificación mínima IP67 (protección total contra polvo y resistencia a inmersión en agua). Esto es vital para soportar la nieve y el "viento blanco".

**Materiales:** Se recomiendan filamentos como **ABS o ASA** para la impresión 3D de las carcasas, ya que resisten mejor los rayos UV y las temperaturas de hasta -20°C que el plástico común.

**Resistencia térmica:** El hardware debe operar en un rango extremo, desde el calor del verano hasta los -20°C en invierno.

## 5. Interfaz de Usuario

**Botón de SOS:** El diseño debe incluir un botón físico de emergencia que sea fácil de presionar incluso con guantes o en condiciones de frío extremo.

## 6. Estado Actual y Próximos Pasos

Actualmente no se ha comprado hardware. El siguiente paso para este equipo es definir la lista de materiales (BOM) para la Prueba de Concepto, asegurando la compatibilidad con el sistema de energía solar que diseñará el Equipo 2.
