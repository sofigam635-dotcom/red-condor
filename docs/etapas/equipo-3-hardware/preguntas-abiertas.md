# Preguntas Abiertas - Equipo 3: Hardware

Este documento contiene los interrogantes técnicos que el **Equipo 3** debe resolver antes de avanzar a la **Etapa 1 (Prueba de concepto)**. Dado que el proyecto se encuentra en **fase de diseño conceptual** y aún **no se ha adquirido hardware**, estas dudas son críticas para definir la primera compra.

## 1. Microcontrolador (ESP32)

- **Consumo Energético:** ¿Cuál es el modelo de ESP32 (S3, C3 o estándar) que ofrece el mejor balance entre potencia de procesamiento y bajo consumo en modo *deep sleep*?
- **Ecosistema:** ¿Existen placas de desarrollo que ya integren el chip LoRa y el ESP32 para reducir fallas en las conexiones manuales?

## 2. GPS y Localización en Montaña

- **Efecto Cañón:** ¿Cómo se comportará la precisión de los módulos GPS en las zonas de Bardas Blancas donde las paredes de la montaña pueden bloquear satélites?
- **Velocidad de Respuesta:** ¿Qué módulos garantizan un *Hot Start* rápido para no agotar la batería del nodo móvil?
- ¿El módulo GPS del T-Beam comercial tiene la potencia suficiente para captar satélites dentro de los cañones profundos de Bardas Blancas?

## 3. Sensores Ambientales (Etapa 6)

- **Resistencia al Clima:** ¿Qué sensores de temperatura y humedad pueden operar de forma continua a -20°C sin descalibrarse durante los temporales invernales?
- **Interfaz de Comunicación:** ¿Es más eficiente utilizar sensores con protocolo I2C o SPI para minimizar la cantidad de cables?

## 4. Protección y Carcasas (IP67)

- **Estanqueidad:** ¿Cómo asegurar el sellado de los puntos de salida para las antenas externas y los botones de pánico para cumplir con la norma IP67?
- **Materiales:** ¿Qué filamentos de impresión 3D (ABS, ASA o PETG) ofrecen la mejor resistencia estructural y protección contra los rayos UV en Malargüe?
- **Condensación:** ¿Es necesario incluir válvulas de compensación de presión para evitar que la humedad interna dañe el ESP32?
- ¿Es necesario algún tipo de aislante térmico dentro de la carcasa?
- ¿Cuál es la mejor caja IP67 en relación calidad-precio disponible en el país?
- ¿Necesitamos antena GPS externa para mejorar la recepción en zonas con obstrucciones?

## 5. Interacción de Usuario

- **Ergonomía:** ¿Cómo diseñar el botón de alerta para que un puestero pueda accionarlo de forma segura incluso usando guantes de abrigo pesados?

## 6. Disponibilidad y Durabilidad

- ¿Se pueden conseguir estos módulos (T-Beam / T-Echo) fácilmente en Argentina a través de proveedores locales o dependemos de la importación directa?
- ¿El puerto USB-C de carga es lo suficientemente resistente para el uso rudo del puestero en la montaña?
- ¿Deberíamos considerar pines de carga magnéticos para evitar roturas?
- ¿Cómo afecta el frío extremo de -20°C a los componentes soldados y a la pantalla (si el nodo tiene una)?
- ¿Qué tan resistente es la electrónica en general a las vibraciones y golpes de la montaña?
