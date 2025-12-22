# CLAUDIO - Robot Cartesiano para Cosecha Automatizada

Proyecto Final de Ingeniería Mecatrónica

## Descripción

Robot cartesiano automatizado para cosecha inteligente de lechugas en sistemas hidropónicos. Integra control de movimiento de precisión con algoritmos de visión por computadora para detectar, clasificar y cosechar cultivos de forma autónoma.

## Características Principales

- Control jerárquico de 2 niveles (Supervisor + Regulatorio)
- 3 algoritmos de visión por computadora para detección y clasificación
- Sistema de coordenadas basado en marcadores visuales
- Detección en movimiento continuo (sistema de FLAGS y snapshots)

## Estructura del Proyecto

```
CLAUDIO/
├── Nivel_Regulatorio/          # Firmware en C para microcontrolador
│   └── Nivel_Regulatorio/
│       ├── main.c
│       ├── drivers/            # Stepper, servo, gripper, UART
│       └── config/
│
├── Nivel_Supervisor/           # Software de alto nivel en Python
│   ├── main.py                 # Punto de entrada
│   ├── core/                   # RobotController, CameraManager
│   ├── hardware/               # Comunicación UART
│   ├── robot/                  # Control de brazo y trayectorias
│   └── workflows/              # Orquestación de flujos
│
├── Nivel_Supervisor_IA/        # Algoritmos de Inteligencia Artificial
│   ├── Escaner Vertical/       # Detección de tubos (posición Y)
│   ├── Escaner Horizontal/     # Detección de cintas (posición X)
│   ├── Analizar Cultivo/       # Clasificación: Lechuga/Plantín/Vacío
│   └── Correccion Posicion*/   # Ajuste fino
│
├── Documentacion_IAs/          # Documentación técnica (3800+ líneas)
│
└── Informe/                    # Informe técnico completo (LaTeX)
    ├── main.pdf
    └── imagenes/               # 90+ diagramas y figuras
```
**Menú principal**:
1. Inicio simple
2. Inicio completo (homing + escaneos)
3. Inicio completo HARD (calibración total)
4. Cosecha interactiva (clasificación + recolección)
5. Homing simple

## Algoritmos de IA

### 1. Detección de Tubos (Escáner Vertical)
Detecta posiciones Y de tubos PVC usando canal S de HSV + Canny Edge Detection.
- Precisión: ~95% | 10 FPS

### 2. Detección de Cintas (Escáner Horizontal)
Detecta posiciones X de marcadores negros mediante análisis de base.
- Precisión: 96% | 6 FPS

### 3. Clasificación de Cultivos
Clasifica cada planta como Lechuga, Plantín o Vacío usando análisis de contornos verdes/negros.

**Sistema de FLAGS**: Detección en movimiento continuo sin detenciones (10× más rápido).

## Documentación

- [Documentación de IAs](Documentacion_IAs/) - Análisis técnico completo
- [Informe del Proyecto](Informe/main.pdf) - Memoria técnica completa
