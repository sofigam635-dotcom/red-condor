# Propuestas y Especificaciones Técnicas - Equipo 5

Este documento define las especificaciones mecánicas, la estandarización de componentes, los mecanismos de autorecuperación por software y el plan de trabajo por fases para la infraestructura de la Red Cóndor.

## 1. Estandarización de Gabinetes Exteriores y Nodos Repetidores (IP67)

Todo equipo expuesto a la intemperie en alta montaña debe ajustarse a los siguientes requisitos constructivos:

1. **Envolvente Exterior:** Cajas estancas con certificación IP67 mínima, construidas en poliéster reforzado con fibra de vidrio o policarbonato con pintura blanca reflectante resistente a radiación UV.
2. **Sellado e Interfaces:** Prensaestopas metálicos con junta tórica y conectores coaxiales (SMA/N) sellados con manguito termocontraíble con resina.
3. **Protección Contra Descargas:** Descargador de sobretensiones gaseoso (Gas Discharge Tube) en la línea de antena, conectado a jabalina de puesta a tierra dedicada.
4. **Compartimento Térmico Subterráneo / Aislado:** Baterías LiFePO4 alojadas en un compartimento interno recubierto con aislante térmico (poliestireno expandido o aerogel), separado de las paredes exteriores del gabinete.

## 2. Estrategia de Autorecuperación de Hardware y Sistema (Watchdog)

Para prevenir fallos catastróficos o congelamientos en nodos y gateways remotos sin acceso presencial:

* **Restablecimiento por Energía:** Configuración obligatoria del parámetro de BIOS `Restore AC Power Loss = Power On` en plataformas x86.
* **Watchdog del Kernel:** Activación del dispositivo de perro de guardia del sistema operativo (`/dev/watchdog`) en Linux Debian.
* **Script de Monitoreo e Invocación de Redundancia:**

```bash
#!/bin/bash
# Script de monitoreo de conectividad para el Gateway Red Cóndor
LOG_PATH="/var/log/watchdog_redcondor.log"
BROKER_IP="127.0.0.1"
# Verificar estado de la VPN Tailscale y Broker MQTT
if ! systemctl is-active --quiet tailscaled; then
    echo "$(date '+%Y-%m-%d %H:%M:%S'): Servicio Tailscale caído. Reiniciando..." >> $LOG_PATH
    systemctl restart tailscaled
fi
if ! nc -z $BROKER_IP 1883; then
    echo "$(date '+%Y-%m-%d %H:%M:%S'): Broker MQTT inaccesible. Reiniciando contendores..." >> $LOG_PATH
    cd /opt/redcondor && docker-compose restart mosquitto
fi
