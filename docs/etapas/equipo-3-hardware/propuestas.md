
# Propuestas de Diseño de Hardware y Robustez Operativa

Para garantizar un funcionamiento confiable en entornos de clima extremo y alta montaña, el diseño del hardware del nodo se rige por los siguientes criterios técnicos y protocolos de validación:

---

### 1. Interfaz del Botón de Pánico y Prevención de Falsas Alarmas
* **Mecanismo de Activación Secundado:** Se implementará un interruptor de seguridad industrial con tapa rebatible (tipo aviación) o un botón de pulso protegido, diseñado para ser operable fácilmente incluso con guantes de alta montaña y pérdida de motricidad fina por frío.
* **Lógica de Confirmación:** Para evitar falsas alarmas por golpes o presión accidental dentro de equipaje, la activación requiere mantener presionado el botón de pánico de forma continua durante 3 segundos, confirmando el envío exitoso de la alerta mediante una señal sonora (zumbador piezoeléctrico) y de vibración.

---

### 2. Mantenimiento Modular y Estabilidad Mecánica
* **Alojamiento Interno por Rieles:** La carcasa incorporará guías y soportes impresos en 3D para alojar la placa principal, la batería y la antena de forma firme, absorbiendo impactos y vibraciones.
* **Conectores Mecánicos:** Se eliminarán las soldaduras directas entre módulos de recambio frecuente. Las conexiones internas utilizarán conectores con traba de seguridad (tipo JST-XH o bornes a tornillo), lo que permitirá que el personal del colegio realice reemplazos rápidos de componentes defectuosos sin riesgo de desprender pistas o cables.

---

### 3. Protocolo de Prueba de Estanqueidad (Hermeticidad IP67)
* **Validación en Laboratorio Escolar:** Antes de instalar cualquier componente electrónico, las carcasas vacías (ensambladas con sus sellos de goma/silicona y prensacables) se someterán a una prueba de inmersión en agua helada a 1 metro de profundidad durante 30 minutos.
* **Verificación de Cero Filtración:** Se colocará un indicador higroscópico (papel de prueba) en el interior. Si el papel permanece 100% seco al finalizar la inmersión, la carcasa se considerará aprobada para el montaje de la electrónica y posterior entrega a los puesteros.

---

### 4. Gestión Eficiente de Indicadores de Estado
* **Diagnóstico Bajo Demanda:** Para maximizar la autonomía de la batería y evitar fuentes de luz molestas durante la noche, los indicadores LED de estado permanecerán apagados por defecto.
* **Muestreo Temporal:** Al presionar un botón de diagnóstico secundario (o al encender el nodo), un LED bicolor indicará la condición del equipo durante 3 segundos:
  * **Verde fijo:** Conexión de red activa y comunicación OK.
  * **Rojo intermitente:** Batería baja (requiere recarga o reemplazo).
  * **Naranja intermitente:** Buscando cobertura de red.

---

### 5. Especificaciones Complementarias de Hardware
* **Puertos de Carga Robustos:** Se descartan conectores magnéticos expuestos debido a la acumulación de barro y nieve. Se utilizarán conectores USB-C reforzados con tapa estanca de goma de sellado o conectores industriales roscados (tipo GX12).
* **Química de Batería Apta para Sub-Cero:** Para mitigar la pérdida drástica de capacidad que sufren las baterías tradicionales de Litio a temperaturas bajo cero (-20 °C), se seleccionarán celdas de rango industrial o química LiFePO4 especificadas para operar en climas fríos.
* **Componentes de Alta Disponibilidad:** Se priorizará el uso de hardware comercial de amplia disponibilidad (como módulos ESP32 y transceptores LoRa SX1262/SX1276) para facilitar la adquisición local y el reemplazo por lotes pequeños.
