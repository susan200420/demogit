# DemoGit: nodo LoRa con display e-ink

> Placa de nodo LoRa a 915 MHz con microcontrolador ATSAMD21 y display e-ink, para enviar datos a larga distancia y mostrarlos en pantalla.

![Versión](https://img.shields.io/badge/hardware-v0.1.0-blue) ![KiCad](https://img.shields.io/badge/KiCad-10.0-314cb0)

## Descripción

Nodo inalámbrico de bajo consumo que combina un microcontrolador ATSAMD21, una radio LoRa RFM95W a 915 MHz y un display e-ink conectado por SPI. Permite comunicar datos de sensores a larga distancia sin depender de redes celulares o Wi-Fi, y mantener la información visible en pantalla sin consumir energía entre refrescos. Se usaría, por ejemplo, en monitoreo ambiental o agrícola en zonas remotas.

## Diagrama de bloques

GitHub dibuja este diagrama automáticamente (es [Mermaid](https://mermaid.js.org/)).

```mermaid
flowchart LR
    USB["J1 USB Micro-B"] -->|VBUS 5V| REG["U1 AP2112K-3.3<br/>regulador LDO"]
    USB <-->|USB D+/D-| MCU["U3 ATSAMD21G15A<br/>microcontrolador"]
    REG -->|3V3| MCU
    REG -->|3V3| LORA["U2 RFM95W<br/>LoRa 915 MHz"]
    MCU <-->|SPI + CS/RST| LORA
    LORA --> ANT["J2 antena<br/>coaxial"]
    SW1["SW1 pulsador"] --> MCU
    REG -->|3V3| EINK["U4 Display e-ink"]
    MCU <-->|SPI + CS/DC/RST| EINK
```

## Componentes principales

| Ref. | Componente | Función |
|------|-----------|---------|
| U1 | AP2112K-3.3 | Regulador lineal 3.3 V |
| U2 | RFM95W-915S2 | Radio LoRa 915 MHz |
| U3 | ATSAMD21G15A-A | Microcontrolador ARM Cortex-M0+ |
| J1 | USB Micro-B | Alimentación y datos |
| J2 | Conector coaxial | Antena |
| U4 | Display e-ink (E_Ink_Display) | Pantalla de baja energía, controlada por SPI |

## Cálculos de diseño

La resistencia de pull-up del reset (R2) consume, con el botón presionado,
$I = \frac{V_{CC}}{R_2} = \frac{3.3\,V}{10\,k\Omega} = 0.33\,mA$.

Potencia disipada en el regulador LDO (U1) durante la transmisión LoRa:

$$
P_{LDO} = (V_{in} - V_{out}) \cdot I = (5\,V - 3.3\,V) \cdot 150\,mA \approx 0.26\,W
$$

Autonomía estimada con una batería de 1000 mAh y un consumo promedio de 2 mA:

$$
t = \frac{C_{bat}}{I_{prom}} = \frac{1000\,mAh}{2\,mA} = 500\,h \approx 21\ \text{días}
$$

## Interfaz SPI del display

![Diagrama de tiempo SPI](docs/spi-eink.svg)

Fuente editable: [`docs/spi-eink.json5`](docs/spi-eink.json5) ([WaveDrom](https://wavedrom.com/))

## Consumo de energía

![Consumo por modo](docs/consumo.svg)

Fuente editable: [`docs/consumo.vl.json`](docs/consumo.vl.json) ([Vega-Lite](https://vega.github.io/vega-lite/)). Valores ilustrativos.

## Estructura del repositorio

```
DemoGit/
├── DemoGit.kicad_pro      # proyecto KiCad
├── DemoGit.kicad_sch      # esquemático
├── DemoGit.kicad_pcb      # layout
├── sym-lib-table          # librerías de símbolos del proyecto
├── Library/               # símbolos propios (E_Ink_Display)
├── docs/                  # diagramas: fuentes (.json5, .json) y SVG exportados
└── README.md              # este archivo
```

## Cómo abrir el proyecto

1. Instala [KiCad 10](https://www.kicad.org/download/).
2. Clona el repositorio:
   ```bash
   git clone https://github.com/susan200420/demogit.git
   ```
3. Abre `DemoGit.kicad_pro` con KiCad.

## Historial de versiones

Ver la pestaña [Releases](../../releases) del repositorio. Cada release incluye el PDF del esquemático.

| Versión | Fecha | Cambios |
|---------|-------|---------|
| v0.1.0 | 2026-10-26 | Primer release: esquemático base + display e-ink |

## Autor

- Susan Lozano Bernardo ([@susan200420](https://github.com/susan200420))
