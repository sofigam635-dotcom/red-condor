# Equipo 2: Energía - Investigación

## 1. Paneles Solares

### Tipos principales

- **Monocristalino**: Células de un solo cristal de silicio. Color negro uniforme. Mayor eficiencia.
- **Policristalino**: Múltiples cristales. Color azul y aspecto cuadriculado. Menor eficiencia y más barato.

### Comparación

| Aspecto          | Monocristalino     | Policristalino    |
|------------------|--------------------|-------------------|
| Eficiencia       | 18-22%             | 15-17%            |
| Rendimiento frío | Mejor              | Inferior          |
| Espacio          | Genera más por m²  | Necesita más área |
| Precio           | Más caro           | Más económico     |

**Recomendación para Red Cóndor:**  
Usar **monocristalino**. Mejor rendimiento en baja insolación y temperaturas frías, y permite paneles más pequeños (importante en nodos y repetidores).

### Orientación e inclinación en Malargüe (≈ 35,5°S)

- Orientación: **Norte** (azimut 0°).
- Inclinación fija recomendada: **30-35°** (compromiso anual).
- Para priorizar invierno: **40-50°**.
- En verano se puede bajar a 20-25° si el soporte lo permite.

**Nota:** En invierno la producción solar baja significativamente (aproximadamente a la mitad o menos que en verano). La nieve sobre el panel puede anular la generación hasta que se limpie o se deslice.

### Potencia orientativa

- Nodo sensor de bajo consumo: 5-10 W
- Repetidor / gateway: 10-30 W (o más según carga)

---

## 2. Baterías

### Tecnologías

| Tipo          | Ventajas                          | Desventajas                          | Aptitud para Malargüe |
|---------------|-----------------------------------|--------------------------------------|-----------------------|
| Plomo-ácido   | Barata                            | Pesada, pocos ciclos, muy mal en frío | Mala                  |
| Li-Ion (NMC)  | Alta densidad                     | Sensible a frío y calor, menos segura | Regular               |
| **LiFePO4**   | Segura, larga vida, mejor en frío | Más cara y pesada que Li-Ion         | **Mejor opción**      |

### LiFePO4 – Puntos importantes

**Ventajas reales:**
- 2000-5000+ ciclos
- Química más segura (menor riesgo de incendio)
- Puede descargarse profundamente con menos daño
- Descarga aceptable hasta aproximadamente -20 °C (con pérdida de capacidad)

**Limitación crítica (no se puede omitir):**
> Las baterías LiFePO4 **no se deben cargar por debajo de 0 °C**.  
> Cargar a temperaturas bajo cero provoca lithium plating (daño permanente de la celda).  
> En Malargüe, donde las mínimas de invierno frecuentemente bajan de 0 °C, es obligatorio:
> - Usar BMS con corte de carga por baja temperatura, **y/o**
> - Aislamiento térmico de la batería, **y/o**
> - Calentador (que consume energía de la propia batería).

Sin una estrategia clara para este punto, la autonomía real en invierno se degrada fuerte.

---

## 3. Consumo Energético del ESP32 + LoRa

### Valores de referencia

| Modo                    | Corriente típica      | Comentario                              |
|-------------------------|-----------------------|-----------------------------------------|
| Deep Sleep (bien hecho) | 10-50 µA              | Solo con placa optimizada y periféricos apagados |
| Deep Sleep (placa común)| 0,5-5 mA              | Muchas placas de desarrollo gastan esto |
| Light Sleep             | 0,8-2 mA              | Radio puede seguir parcial activa       |
| Activo / TX LoRa        | 80-150 mA (picos)     | Depende de potencia de transmisión      |

**Consumo promedio realista:**
- Con deep sleep agresivo + transmisiones cada 30-60 min: se puede apuntar a **0,5-2 mA** promedio.
- Con transmisiones más frecuentes o GPS activo: fácilmente 3-10 mA o más.

**Importante:** Los valores de 2-5 mA promedio que se manejan en algunos documentos son conservadores (altos). Para nodos de muy bajo consumo se debe apuntar más abajo, pero hay que **medirlo** en el prototipo real. Las estimaciones teóricas suelen ser optimistas.

### Cómo reducir consumo

- Deep Sleep + wake-up por timer (o por sensor).
- Apagar Bluetooth, WiFi y GPS cuando no se usen.
- Intervalos de transmisión largos (30-60 min o más).
- Usar módulos LoRa que realmente entren en sleep (no todos lo hacen bien).
- Evitar placas de desarrollo con reguladores de alta corriente de reposo.

---

## 4. Autonomía y Dimensionamiento

### Fórmula básica (mejorada)

Donde:
- Capacidad útil = capacidad nominal × profundidad de descarga segura (DoD) × factor de temperatura
- En frío la capacidad disponible baja (a -10 °C puede quedar 70-80% de la nominal)

### Ejemplo orientativo (nodo sensor)

| Parámetro                    | Valor ejemplo          |
|-----------------------------|------------------------|
| Batería                     | 20 Ah LiFePO4 (12,8 V) ≈ 256 Wh |
| DoD seguro                  | 80%                    |
| Factor frío                 | 0,75                   |
| Capacidad útil aproximada   | ≈ 150 Wh               |
| Consumo diario objetivo     | 1-3 Wh                 |
| Autonomía teórica           | 50-150 días            |
| Autonomía realista invierno | 7-20 días (según sol y frío) |

**Diseño recomendado:**
- Dimensionar para **al menos 7-10 días** sin sol en condiciones de invierno.
- Incluir telemetría del estado de batería (voltaje + temperatura).

### Dimensionamiento orientativo

| Tipo de nodo       | Panel          | Batería LiFePO4     | Comentario                     |
|--------------------|----------------|---------------------|--------------------------------|
| Sensor de puesto   | 5-10 W         | 10-30 Ah            | Priorizar bajo consumo         |
| Estación de rescate| 10-20 W        | 30-60 Ah            | Más margen de autonomía        |
| Gateway / repetidor| 30-80 W        | 100 Ah o más        | Mayor consumo continuo         |

---

## 5. Resumen de recomendaciones técnicas

1. **Panel:** Monocristalino, orientado al Norte, inclinación 30-40°.
2. **Batería:** LiFePO4 obligatoria. Resolver sí o sí el problema de carga bajo 0 °C.
3. **Consumo:** Medir en prototipo real. No confiar solo en datasheets.
4. **Autonomía:** Diseñar con margen de invierno (nubes + nieve + frío).
5. **Telemetría:** Incluir reporte del estado de batería y temperatura.
6. **Controlador de carga:** Preferir MPPT con corte por baja temperatura.

---

**Nota:**  
Esta investigación es una base. Los números de consumo y autonomía deben validarse con mediciones reales en prototipos antes de usarlos como referencia definitiva para el diseño final.

