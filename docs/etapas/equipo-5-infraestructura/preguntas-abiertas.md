# Preguntas Abiertas y Variables a Validar - Equipo 5

Este documento establece las incertezas técnicas, los parámetros de campo no confirmados y los puntos de fallo institucionales que deben validarse empíricamente antes del despliegue definitivo.

## 1. Radiofrecuencia y Propagación en Terreno (RF First)

- **Atenuación Real por Topografía:** ¿Cuál es la pérdida de propagación empírica (RSSI y SNR) en los cañones y quebradas del corredor Bardas Blancas - Puesto Piuquenes?
- **Ubicación Óptima de Repetidores:** ¿Cuántos nodos repetidores fijos se requieren exactamente para eliminar las sombras de radiofrecuencia entre los puestos y el Gateway principal?
- **Ganancia de Antenas:** ¿Qué patrón de radiación y ganancia (dBi) equilibran el alcance en quebradas con una baja carga eólica sobre los mástiles?

## 2. Consumo Energético y Selección de Servidores de Borde

- **Autonomía del Gateway x86:** El uso de una PC reciclada (ej. Intel Core i5-3320M) supone un consumo de 15W a 35W. En un corte de energía prolongado en Bardas Blancas, ¿cuántas horas soporta la UPS antes del apagado del sistema?
- **Factibilidad de Arquitectura ARM:** ¿Es posible e idóneo reemplazar la PC x86 por una Single Board Computer (SBC) de bajo consumo (<5W, ej. Raspberry Pi 4 o Bananapi) para extender la autonomía energética?
- **Aislamiento Térmico de Baterías:** ¿Qué espesor de aislamiento interno requiere la caja estanca para mantener las celdas LiFePO4 por encima de 0 °C durante la recarga fotovoltaica en heladas de -20 °C?

## 3. Usabilidad y Adopción Humana

- **Diseño de Interfaz Simplificada:** Considerando que los puesteros operan bajo frío y estrés, ¿se puede sustituir la aplicación de smartphone por un dispositivo físico tipo "botón de pánico rugerizado"?
- **Perfil de Autonomía Requerida:** ¿Cuántos días consecutivos permanece un puestero en la alta montaña sin posibilidad de recargar el nodo?

## 4. Coordinación Institucional y Protocolo de Respuesta

- **Modelo de Flujo de Alertas:** ¿Quién recibe operativamente el mensaje de auxilio? ¿Defensa Civil de Malargüe cuenta con capacidad técnica para integrar alertas digitales directas o la llamada debe ser canalizada por personal escolar?
- **Formalización de Acuerdos:** ¿Qué marco legal o convenio se requiere firmar con Gendarmería Nacional y Defensa Civil para dar validez operativa al protocolo de rescate?

## 5. Regulaciones y Licencias de Radiofrecuencia

- **Banda Homologada:** ¿Qué parámetros de frecuencia (433 MHz vs 915 MHz) y límites de potencia de transmisión (eIRP) autoriza ENACOM para uso comunitario escolar sin licencia de radioaficionado?
