# Pregunta 2: Definition of Physical Layer Requirements (5 puntos)

## Elabore el Definition of physical layer requirements (los requisitos para el Physical Layer de la IoT Solution). Considere: a) número y tipos de nodos sensores y actuators; b) Target uncertainty (incertidumbre objetivo), relacionada con las cantidades físicas medidas por cada sensor; c) Target accuracy and precision (Exactitud y precisión objetivo) de los actuadores; d) Processing Power (Esfuerzo computacional) para los algoritmos de procesamiento de datos que se implementarán en el Edge node.

---

## A) NÚMERO Y TIPOS DE NODOS SENSORES Y ACTUADORES

### A.1 Nodos Sensores

#### Sistemas de Seguimiento Óptico
**Número de unidades**: 8-16 cámaras por cancha estándar
- **Tipo**: Cámaras de alta velocidad para seguimiento 3D
- **Especificaciones técnicas**:
  - Resolución: 1920x1080 mínimo, preferible 4K
  - Frecuencia de captura: 240-1000 fps
  - Sensor: CMOS de alta sensibilidad
  - Lente: Gran angular con corrección de distorsión
- **Ubicación**: Perímetro superior del estadio con ángulos de cobertura optimizados
- **Interfaz de comunicación**: Ethernet Gigabit (GigE Vision)
- **Alimentación**: PoE+ (Power over Ethernet) 60W por unidad

#### Sensores Inerciales en Jugadores (IMU - Inertial Measurement Units)
**Número de unidades**: 10-12 sensores por equipo (máximo 24 por partido)
- **Tipo**: IMU de 9 grados de libertad (9-DOF)
- **Componentes integrados**:
  - Acelerómetro 3-axis: ±16g con resolución 16-bit
  - Giroscopio 3-axis: ±2000°/s con resolución 16-bit
  - Magnetómetro 3-axis: ±4900μT
- **Frecuencia de muestreo**: 500 Hz mínimo
- **Comunicación**: BLE 5.0 o protocolo propietario de baja latencia
- **Batería**: Autonomía mínima 4 horas de juego continuo
- **Factor de forma**: Wearable integrado en uniforme o calzado

#### Sensores de Balón
**Número de unidades**: 2-4 balones instrumentados por partido
- **Tipo**: Sensor IMU miniaturizado + chip de posicionamiento
- **Especificaciones**:
  - IMU 6-DOF integrado en el centro del balón
  - Sensor de presión para detectar contactos
  - Chip UWB (Ultra-Wideband) para posicionamiento preciso
- **Comunicación**: UWB + BLE para redundancia
- **Batería**: Carga inalámbrica, autonomía 8 horas
- **Resistencia**: IPX7 para resistencia a impactos y humedad

#### Anclas de Posicionamiento UWB
**Número de unidades**: 12-20 anclas por cancha
- **Tipo**: Transceptores UWB de alta precisión
- **Especificaciones**:
  - Frecuencia: 3.5-6.5 GHz (banda UWB)
  - Precisión de distancia: ±10 cm
  - Alcance: 50-100 metros en línea de vista
- **Ubicación**: Perímetro de la cancha a diferentes alturas
- **Sincronización**: Red de tiempo sincronizada con precisión de nanosegundos
- **Alimentación**: PoE estándar, 15W por unidad

### A.2 Nodos Actuadores

#### Sistema LED de Visualización Principal
**Número de módulos**: Variable según resolución y tamaño
- **Configuración LumiFlex (Alta resolución)**:
  - Densidad: 2.5mm pixel pitch
  - Módulos por m²: 160-200 módulos
  - Total para cancha 420 m²: 67,200-84,000 módulos
- **Configuración Líneas Básicas**:
  - LEDs RGB integrados en tiras
  - Resolución: 10mm pixel pitch
  - Total: 8,400-10,500 módulos

#### Especificaciones Técnicas de LEDs
- **Tipo**: LED SMD RGB de alta potencia
- **Brillo máximo**: 1,500-3,000 nits
- **Profundidad de color**: 16-bit por canal (48-bit total)
- **Frecuencia PWM**: 3,840 Hz mínimo (sin parpadeo)
- **Vida útil**: >100,000 horas
- **Temperatura de operación**: -20°C a +60°C

#### Controladores LED
**Número de unidades**: 50-200 controladores según configuración
- **Tipo**: Controladores LED de alta frecuencia
- **Capacidad**: 16-32 puertos de salida por controlador
- **Interfaz de entrada**: Ethernet con protocolo propietario o ArtNet/sACN
- **Procesamiento local**: FPGA para rendering en tiempo real
- **Sincronización**: Genlock para sincronía perfecta entre controladores

#### Sistema de Audio Integrado (Opcional)
**Número de unidades**: 8-12 altavoces direccionales
- **Tipo**: Arrays de altavoces beam-forming
- **Potencia**: 200-500W por unidad
- **Frecuencia**: 50 Hz - 20 kHz
- **Ubicación**: Integrados en estructura superior de la cancha

---

## B) TARGET UNCERTAINTY (Incertidumbre Objetivo)

### B.1 Incertidumbre Espacial

#### Seguimiento de Posición de Jugadores
- **Objetivo establecido**: <10 cm en todas las dimensiones (X, Y, Z)
- **Desglose por sistema**:
  - Sistema óptico (cámaras): ±5 cm en plano XY, ±8 cm en Z
  - Sistema UWB: ±3 cm en plano XY, ±5 cm en Z
  - Fusión de sensores: ±2 cm combinado (mejora mediante filtro Kalman)

#### Seguimiento de Balón
- **Objetivo mejorado**: <5 cm para trayectoria
- **Especificaciones**:
  - Posición en reposo: ±2 cm
  - Durante movimiento rápido: ±5 cm
  - Rotación (spin): ±10 RPM

#### Factores de Incertidumbre Considerados
- **Calibración de cámaras**: Distorsión de lente, alineación
- **Sincronización temporal**: Desfase entre sistemas
- **Condiciones ambientales**: Iluminación, reflejos, oclusiones
- **Interferencia electromagnética**: Afectación en sistemas UWB

### B.2 Incertidumbre Temporal

#### Sincronización Global del Sistema
- **Objetivo establecido**: <20 ms entre todas las fuentes de datos
- **Implementación**:
  - Reloj maestro distribuido via PTP (Precision Time Protocol)
  - Sincronización de cámaras: ±1 ms
  - Sincronización de sensores IMU: ±5 ms
  - Compensación de latencias de red: Algoritmos adaptativos

#### Timestamp Accuracy
- **Resolución temporal**: 1 ms mínimo
- **Drift compensation**: Corrección automática de deriva de relojes
- **Buffer management**: Compensación de jitter en comunicaciones

### B.3 Calibración y Mantenimiento de Precisión

#### Procedimientos de Calibración
- **Calibración geométrica**: Mapeo 3D de la cancha con precisión milimétrica
- **Calibración de color**: Uniformidad de LED con tolerancia ΔE<2
- **Calibración temporal**: Sincronización verificada cada 24 horas

#### Monitoreo Continuo
- **Validación en tiempo real**: Comparación entre sistemas redundantes
- **Alertas de deriva**: Notificación cuando incertidumbre supera umbrales
- **Recalibración automática**: Ajustes dinámicos durante operación

---

## C) TARGET ACCURACY AND PRECISION (Exactitud y Precisión de Actuadores)

### C.1 Precisión del Sistema de Visualización LED

#### Precisión Espacial de Píxeles
- **Objetivo establecido**: Precisión submilimétrica
- **Especificaciones técnicas**:
  - Tolerancia de posición por LED: ±0.5 mm
  - Planitud del piso: ±1 mm en superficie total
  - Alineación entre módulos: ±0.2 mm

#### Precisión de Color y Brillo
- **Uniformidad de color**: ΔE <2.0 (imperceptible al ojo humano)
- **Uniformidad de brillo**: ±3% en toda la superficie
- **Precisión temporal de color**: Cambios <16.7 ms (60 fps mínimo)
- **Profundidad de color**: 16-bit por canal RGB (281 trillones de colores)

### C.2 Precisión de Renderizado Gráfico

#### Resolución Gráfica
- **Pixel pitch**: 2.5 mm para LumiFlex (resolución ultra alta)
- **Densidad**: 160,000 píxeles/m²
- **Resolución total**: 67.2-84 millones de píxeles (cancha estándar)

#### Precisión Geométrica
- **Mapeo de coordenadas**: Transformación mundo real ↔ píxeles con precisión <1 píxel
- **Corrección de perspectiva**: Compensación automática para diferentes ángulos de vista
- **Anti-aliasing**: Suavizado de líneas y curvas en tiempo real

### C.3 Precisión Temporal de Actuación

#### Latencia de Respuesta
- **Tiempo de respuesta LED**: <1 ms desde señal a cambio visible
- **Sincronización entre módulos**: ±100 μs (microsegundos)
- **Frecuencia de actualización**: 3,840 Hz (eliminación total de flicker)

#### Coherencia Temporal
- **Frame rate mínimo**: 60 fps para contenido fluido
- **Frame rate óptimo**: 120-240 fps para deportes de alta velocidad
- **Latencia total de visualización**: <16.7 ms (1 frame a 60 fps)

---

## D) PROCESSING POWER (Esfuerzo Computacional para Edge Nodes)

### D.1 Arquitectura de Edge Computing

#### Número de Edge Nodes Requeridos
- **Configuración mínima**: 1 Edge Node potente para funciones básicas
- **Configuración óptima**: 3-5 Edge Nodes para LumiFlex con seguimiento
- **Distribución de carga**:
  - Node 1: Procesamiento de video y visión artificial
  - Node 2: Fusión de sensores y tracking algorithms
  - Node 3: Renderizado gráfico y control LED
  - Nodes 4-5: Redundancia y balanceamiento de carga

### D.2 Especificaciones por Edge Node

#### Capacidad de CPU
- **Procesador**: Intel Xeon o AMD EPYC (server-grade)
- **Núcleos**: 16-32 cores físicos mínimo
- **Frecuencia**: 2.8-3.5 GHz base, boost hasta 4.5 GHz
- **Cache**: L3 cache 32-64 MB
- **Arquitectura**: x86_64 con extensiones AVX-512 para procesamiento vectorial

#### Capacidad de GPU para Aceleración
- **GPU principal**: NVIDIA RTX A6000 o superior
- **CUDA Cores**: 10,752 cores mínimo
- **Tensor Cores**: 336 cores de 3ra generación para AI/ML
- **VRAM**: 48 GB GDDR6 mínimo
- **Bandwidth de memoria**: 768 GB/s
- **Múltiples GPUs**: Configuración SLI/NVLink para cargas extremas

#### Memoria RAM
- **Capacidad total**: 128-256 GB DDR4/DDR5
- **Velocidad**: 3200-4800 MHz
- **Configuración**: ECC (Error Correcting Code) para confiabilidad
- **Distribución**:
  - 32-64 GB para OS y servicios base
  - 64-128 GB para buffers de video en tiempo real
  - 32-64 GB para modelos AI/ML y cache de algoritmos

#### Almacenamiento de Alta Velocidad
- **Almacenamiento primario**: 2-4 TB NVMe SSD PCIe 4.0
- **IOPS**: >1,000,000 IOPS para acceso aleatorio
- **Throughput**: >7 GB/s lectura secuencial
- **Configuración RAID**: RAID 0 para performance, RAID 1 para redundancia crítica

### D.3 Algoritmos Computacionalmente Intensivos

#### Visión Artificial y Detección de Objetos
- **Algoritmo**: YOLO v8 optimizado para deportes
- **Throughput requerido**: 240-1000 fps por cámara
- **Latencia objetivo**: <5 ms por frame
- **Carga computacional**: 15-25 TFLOPS por cámara de alta velocidad

#### Seguimiento Multi-Objeto (Multi-Object Tracking)
- **Algoritmo**: DeepSORT o FairMOT optimizado
- **Objetos simultáneos**: 12-24 jugadores + 1-2 balones
- **Predicción de trayectoria**: Filtros Kalman extendidos
- **Carga computacional**: 5-10 TFLOPS para seguimiento completo

#### Fusión de Sensores
- **Algoritmo**: Extended Kalman Filter (EKF) o Particle Filter
- **Frecuencia de procesamiento**: 500-1000 Hz
- **Latencia objetivo**: <2 ms
- **Carga computacional**: 1-2 TFLOPS para fusión multimodal

#### Renderizado Gráfico en Tiempo Real
- **Engine**: Unreal Engine 5 o motor personalizado
- **Resolución**: 67-84 millones de píxeles
- **Frame rate**: 60-240 fps
- **Efectos**: Particle systems, physics simulation, lighting
- **Carga computacional**: 20-40 TFLOPS para renderizado completo

### D.4 Interfaces de Red de Alta Velocidad

#### Conectividad Principal
- **Ethernet**: 10 Gigabit mínimo, preferible 25/40 Gigabit
- **Puertos**: 4-8 puertos de red para redundancia
- **Protocolo**: TCP/IP optimizado + protocolos de tiempo real
- **Latencia de red**: <1 ms en LAN dedicada

#### Comunicación Inter-Node
- **InfiniBand**: 100 Gbps para comunicación entre Edge Nodes
- **RDMA**: Remote Direct Memory Access para latencia ultra-baja
- **Cluster networking**: Topología de malla para máxima redundancia

### D.5 Gestión Térmica y Energética

#### Disipación de Calor
- **TDP total por node**: 800-1200W bajo carga máxima
- **Sistema de refrigeración**: Líquida de circuito cerrado
- **Temperatura operativa**: Máximo 80°C en componentes críticos
- **Monitoreo térmico**: Sensores en tiempo real con throttling adaptativo

#### Eficiencia Energética
- **Fuente de alimentación**: 80 PLUS Titanium (94%+ eficiencia)
- **Gestión de energía**: Dynamic voltage and frequency scaling (DVFS)
- **Modos de ahorro**: Idle states durante períodos de baja actividad

### D.6 Software y Middleware

#### Sistema Operativo
- **OS**: Ubuntu Server 22.04 LTS o CentOS Stream
- **Kernel**: Optimizado para tiempo real (RT kernel patches)
- **Scheduler**: CFS modificado para prioridades de tiempo real

#### Framework de Desarrollo
- **Lenguajes**: C++ para algoritmos críticos, Python para AI/ML
- **Librerías**: OpenCV, PCL, TensorRT, CUDA toolkit
- **Middleware**: ROS2 o framework personalizado para comunicación

#### Monitoreo y Telemetría
- **Métricas en tiempo real**: CPU, GPU, memoria, red, temperatura
- **Alertas proactivas**: Machine learning para detección de anomalías
- **Dashboard**: Grafana con métricas de rendimiento en tiempo real
