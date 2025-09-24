# Pregunta 2: Definition of Physical Layer Requirements (5 puntos)

## Elabore el Definition of physical layer requirements (los requisitos para el Physical Layer de la IoT Solution). Considere: a) número y tipos de nodos sensores y actuators; b) Target uncertainty (incertidumbre objetivo), relacionada con las cantidades físicas medidas por cada sensor; c) Target accuracy and precision (Exactitud y precisión objetivo) de los actuadores; d) Processing Power (Esfuerzo computacional) para los algoritmos de procesamiento de datos que se implementarán en el Edge node.

---

## A) NÚMERO Y TIPOS DE NODOS SENSORES Y ACTUADORES

### A.1 Nodos Sensores

#### Sistemas de Seguimiento Óptico (Según enunciado)
**Descripción**: Múltiples cámaras de alta velocidad ubicadas estratégicamente en el estadio (enunciado)
- **Número estimado**: 12-16 cámaras para cancha estándar (420 m²)
- **Frecuencia de captura**: 240-1000 fps para seguimiento de alta velocidad
- **Resolución**: 1920x1080 mínimo por cámara (2.1 MP)
- **Volumen de datos**: ~25-100 GB/minuto por cámara (sin comprimir)
- **Función**: Capturan video a altas velocidades de fotogramas para seguimiento preciso y triangulación 3D (enunciado)
- **Ubicación**: Alrededor del estadio desde diferentes ángulos (enunciado)
- **Procesamiento**: Software de visión artificial procesa datos de video para ubicación precisa 3D (enunciado)
- **Ejemplos mencionados**: Hawk-Eye como sistema ampliamente utilizado (enunciado)
- **Integración**: Los datos se introducen en GlassCourt OS para mostrar gráficos dinámicos (enunciado)
- **Outputs**: Trayectorias de jugadores, zonas de tiro, superposiciones estadísticas (enunciado)
- **Latencia típica**: 15-52 ms según enunciado para sistemas similares

#### Sensores Basados en Red de Anclaje (Según enunciado)
**Descripción**: Red de sensores de anclaje ubicados en las instalaciones (enunciado)
- **Número de anclas**: 16-24 dispositivos por cancha estándar (420 m²)
- **Sensores por jugador**: 1 sensor wearable por jugador (máximo 24 por partido)
- **Sensores en balón**: 1-2 sensores integrados por balón
- **Frecuencia de muestreo**: 100-500 Hz por sensor
- **Alcance de comunicación**: 50-100 metros por ancla
- **Precisión de distancia**: ±10 cm (cumple objetivo <10 cm del enunciado)
- **Función**: Comunicarse con pequeñas etiquetas de seguimiento que llevan los jugadores (enunciado)
- **Ejemplo específico**: ShotTracker como socio de ASB mencionado en enunciado
- **Implementación**: Dispositivos de captura colocados en la cancha (enunciado)
- **Jugadores**: Cada jugador lleva un sensor para localización continua (enunciado)
- **Balón**: Sensores integrados en el balón para rastrear posición y velocidad de giro (enunciado)
- **Integración**: Datos se transfieren al sistema operativo GlassCourt (enunciado)
- **Volumen de datos**: ~50-250 KB/s por sensor activo
- **Ejemplo de uso**: Entrenador dibuja jugada en iPad → aparece como trayectoria iluminada (enunciado)

#### Unidades de Medición Inercial (IMU) Portátiles (Según enunciado)
**Descripción**: IMU portátiles instalados en jugadores y balón (enunciado)
- **Función**: Proporcionar datos precisos de movimiento en tiempo real (enunciado)
- **Ubicación**: En jugadores y en el balón (enunciado)  
- **Propósito**: Complementar los sistemas ópticos para seguimiento completo (enunciado)
- **Integración**: Forma parte del ecosistema de múltiples fuentes de datos (enunciado)
- **Beneficio**: Datos de movimiento directo sin depender solo de visión artificial (enunciado)

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

#### Sistema LED de Visualización (Según especificaciones del enunciado)
**Actuadores en forma de matrices LED** (enunciado):
- **LumiFlex (Alta densidad)**:
  - Pixel pitch: 2.5-5 mm
  - Densidad: 40,000-160,000 LEDs/m²
  - Total cancha 420 m²: 16.8-67.2 millones de LEDs
  - Consumo: >570 W/m² máximo (enunciado)
- **Señalización básica**: 
  - Pixel pitch: 8-12 mm  
  - Densidad: 6,900-15,600 LEDs/m²
  - Total cancha 420 m²: 2.9-6.6 millones de LEDs
  - Consumo: 190 W/m² promedio (enunciado)
- **Controladores necesarios**: 100-500 unidades según resolución
- **Módulos LED por controlador**: 50-200 módulos
- **Determinación de cantidad**: Depende directamente del tamaño de cancha y resolución deseada (enunciado)
- **Integración**: Sincronización perfecta con pantallas LED y cubos de video (enunciado)
- **Control**: Sistema operativo GlassCourt controla LEDs para mostrar imágenes dinámicas (enunciado)
- **Ancho de banda requerido**: 10-40 Gbps para actualización completa

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

#### Seguimiento de Posición de Jugadores (Requisito específico del enunciado)
- **Objetivo del sistema**: Incertidumbre espacial inferior a 10 centímetros para seguimiento de posición (enunciado)
- **Especificaciones numéricas**:
  - Precisión en plano XY: ±8 cm (cumple <10 cm)
  - Precisión en altura Z: ±12 cm 
  - Precisión de velocidad: ±0.5 m/s
  - Área de cobertura: 100% de cancha (420 m²)
  - Objetos simultáneos: 24 jugadores + 2 balones
- **Propósito**: Garantizar visualización fiable de ubicaciones de jugadores y balón (enunciado)
- **Importancia**: Para que las mediciones de sensores sean útiles, incertidumbre debe ser mínima (enunciado)
- **Frecuencia de actualización**: 100-500 Hz para seguimiento fluido
- **Aplicación**: Seguimiento preciso tanto de jugadores como del balón en la cancha (enunciado)

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

#### Sincronización Temporal del Sistema (Requisito del enunciado)
- **Objetivo del sistema**: Incertidumbre temporal inferior a 20 milisegundos (enunciado)
- **Especificaciones numéricas**:
  - Sincronización entre cámaras: ±2 ms
  - Sincronización sensores-cámaras: ±5 ms
  - Drift máximo de relojes: ±10 ms/hora
  - Corrección automática: cada 100 ms
  - Buffer temporal máximo: 50 ms
- **Fuentes de datos simultáneas**: 12-16 cámaras + 24 sensores + sistemas externos
- **Propósito**: Mantener sincronización precisa de datos de diversas fuentes (enunciado)
- **Importancia**: Requisito fundamental para rendimiento constante del sistema (enunciado)
- **Frecuencia de verificación**: 1000 Hz para detección de deriva
- **Aplicación**: Coordinar datos de múltiples sistemas de seguimiento simultáneos (enunciado)

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

#### Precisión de Actuadores LED (Requisitos del enunciado)
- **Objetivo del sistema**: Precisión de píxeles submilimétrica (enunciado)
- **Especificaciones numéricas**:
  - Tolerancia de posición por LED: ±0.5 mm
  - Planitud de superficie: ±1 mm en 420 m²
  - Uniformidad de color: ΔE <2.0 (imperceptible)
  - Uniformidad de brillo: ±3% en toda superficie
  - Precisión geométrica: <1 píxel de error de mapeo
- **Resolución total LumiFlex**: 67.2 millones de píxeles (420 m²)
- **Propósito**: Obtener gráficos nítidos y salida visual fluida en toda la cancha (enunciado)
- **Requerimiento**: Controladores LED y sistemas de control de alta calidad (enunciado)
- **Frecuencia PWM**: 3,840 Hz mínimo para eliminación de flicker
- **Aplicación**: Salida visual precisa para toda la superficie de la cancha (enunciado)

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

#### Número de Edge Nodes Requeridos (Especificaciones exactas del enunciado)
- **Cantidad no estática**: Depende de factores clave que determinan escalabilidad y fiabilidad (enunciado)
- **Configuración mínima**: Un único nodo de borde potente para funciones básicas como cambiar configuraciones estáticas de líneas (enunciado)  
- **Configuración avanzada**: Múltiples Edge nodes para LumiFlex de alta resolución con seguimiento en tiempo real (enunciado)
- **Distribución de cargas computacionales**:
  - Ingesta de datos de cámaras de alta velocidad (enunciado)
  - Ejecución de algoritmos de IA y aprendizaje automático para análisis (enunciado)
  - Representación de contenido visual complejo (enunciado)
- **Factores determinantes**: Tamaño físico de cancha y resolución requerida (enunciado)

### D.2 Especificaciones por Edge Node

#### Especificaciones de Edge Node (Según enunciado)
**Potente nodo de borde equipado con CPU y GPU de alto rendimiento** (enunciado):
- **CPU de alto rendimiento**: 
  - 16-32 cores físicos (Intel Xeon/AMD EPYC)
  - Frecuencia: 2.8-4.5 GHz
  - Cache L3: 32-64 MB
  - Gestiona control del sistema, tráfico de red y procesamiento de datos (enunciado)
- **GPU de alto rendimiento**: 
  - NVIDIA RTX A6000: 10,752 CUDA cores
  - VRAM: 48 GB GDDR6
  - Bandwidth: 768 GB/s
  - Acelera visión artificial, análisis de IA/ML y tareas de renderizado (enunciado)
- **Memoria de alta velocidad**: 
  - 128-256 GB DDR4/DDR5 ECC
  - Velocidad: 3200-4800 MHz
  - Adecuada para soportar alto rendimiento de datos (enunciado)
- **Almacenamiento de alta velocidad**: 
  - 2-4 TB NVMe SSD PCIe 4.0
  - IOPS: >1,000,000 acceso aleatorio
  - Throughput: >7 GB/s lectura secuencial
  - Esencial para demandas de procesamiento en tiempo real (enunciado)
- **Interfaces de red de alta velocidad**: 
  - Ethernet: 25-100 Gbps
  - Puertos: 4-8 para redundancia
  - Latencia: <1 ms en LAN
  - Esenciales para soportar alto rendimiento de datos en tiempo real (enunciado)

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
- **Procesamiento total**: 12-16 cámaras × 20 TFLOPS = 240-320 TFLOPS
- **Memoria requerida**: 8-16 GB VRAM por flujo de cámara
- **Ancho de banda**: 25-100 GB/s por cámara para transferencia de frames

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
- **Resolución**: 67-84 millones de píxeles (cancha 420 m²)
- **Frame rate**: 60-240 fps según aplicación
- **Efectos**: Particle systems, physics simulation, lighting
- **Carga computacional**: 20-40 TFLOPS para renderizado completo
- **Memoria de video**: 32-64 GB para buffers de renderizado
- **Ancho de banda salida**: 40-160 Gbps hacia controladores LED
- **Latencia total**: <16.7 ms (1 frame a 60 fps)

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

---

## TABLA DE ESPECIFICACIONES DE REQUISITOS - PHYSICAL LAYER

| Physical Layer Requirement | Especificación de requisitos |
|---------------------------|------------------------------|
| **Número y tipos de nodos sensores y actuadores** | **SENSORES (Aproximaciones numéricas):**<br/>• **Sistemas ópticos**: 12-16 cámaras de alta velocidad (240-1000 fps) ubicadas estratégicamente (enunciado)<br/>• **Sensores de anclaje**: 16-24 anclas por cancha (420 m²) para comunicarse con etiquetas de seguimiento (enunciado)<br/>• **IMU portátiles**: 24 sensores para jugadores + 2 para balones, frecuencia 100-500 Hz (enunciado)<br/>• **Volumen total de datos**: ~300-1,200 GB/minuto sin procesar<br/><br/>**ACTUADORES (Aproximaciones numéricas):**<br/>• **LumiFlex**: 16.8-67.2 millones de LEDs (pixel pitch 2.5-5 mm) para cancha 420 m² (enunciado)<br/>• **LED básicos**: 2.9-6.6 millones de LEDs (pixel pitch 8-12 mm) para líneas multideportivas (enunciado)<br/>• **Controladores**: 100-500 unidades según resolución<br/>• **Consumo energético**: 239.4 kW máximo (570 W/m² × 420 m²) según enunciado |
| **Target uncertainty (incertidumbre objetivo), relacionada con las cantidades físicas medidas por cada sensor** | **INCERTIDUMBRE ESPACIAL (Aproximaciones numéricas):**<br/>• **Objetivo**: <10 cm para seguimiento de posición (enunciado)<br/>• **Precisión XY**: ±8 cm para cumplir objetivo<br/>• **Precisión Z**: ±12 cm en altura<br/>• **Precisión velocidad**: ±0.5 m/s<br/>• **Cobertura**: 100% de cancha (420 m²)<br/>• **Objetos simultáneos**: 24 jugadores + 2 balones<br/><br/>**INCERTIDUMBRE TEMPORAL (Aproximaciones numéricas):**<br/>• **Objetivo**: <20 ms para sincronización (enunciado)<br/>• **Sincronización cámaras**: ±2 ms<br/>• **Sincronización sensores**: ±5 ms<br/>• **Drift máximo**: ±10 ms/hora<br/>• **Frecuencia verificación**: 1000 Hz<br/>• **Fuentes simultáneas**: 40+ dispositivos de captura |
| **Target accuracy and precision (Exactitud y precisión objetivo) de los actuadores** | **PRECISIÓN ACTUADORES LED (Aproximaciones numéricas):**<br/>• **Objetivo**: Precisión submilimétrica de píxeles (enunciado)<br/>• **Tolerancia posición**: ±0.5 mm por LED<br/>• **Planitud superficie**: ±1 mm en 420 m²<br/>• **Uniformidad color**: ΔE <2.0 (imperceptible)<br/>• **Uniformidad brillo**: ±3% en toda superficie<br/>• **Resolución total**: 67.2 millones píxeles (LumiFlex)<br/>• **Frecuencia PWM**: 3,840 Hz mínimo (enunciado)<br/>• **Latencia visualización**: 20-40 ms (1-2 frames a 50-60 fps) según enunciado<br/>• **Precisión geométrica**: <1 píxel error de mapeo<br/>• **Ancho de banda salida**: 40-160 Gbps hacia LEDs |
| **Processing Power (Esfuerzo computacional) para los algoritmos de procesamiento de datos que se implementarán en el Edge node** | **ESPECIFICACIONES EDGE NODE (Aproximaciones numéricas):**<br/>• **CPU**: 16-32 cores (2.8-4.5 GHz), Cache L3: 32-64 MB, gestiona control del sistema (enunciado)<br/>• **GPU**: NVIDIA RTX A6000 (10,752 CUDA cores), 48 GB VRAM, 768 GB/s, acelera IA/ML (enunciado)<br/>• **Memoria**: 128-256 GB DDR4/DDR5 ECC (3200-4800 MHz) para alto rendimiento (enunciado)<br/>• **Almacenamiento**: 2-4 TB NVMe SSD PCIe 4.0 (>7 GB/s, >1M IOPS) para tiempo real (enunciado)<br/>• **Red**: 25-100 Gbps Ethernet, 4-8 puertos redundantes, <1 ms latencia (enunciado)<br/><br/>**CARGAS COMPUTACIONALES (Aproximaciones numéricas):**<br/>• **Visión artificial**: 240-320 TFLOPS total (12-16 cámaras × 20 TFLOPS)<br/>• **Renderizado**: 20-40 TFLOPS para 67M píxeles a 60-240 fps<br/>• **Configuración mínima**: 1 nodo (líneas estáticas) según enunciado<br/>• **Configuración avanzada**: 3-5 nodos (LumiFlex + seguimiento) según enunciado<br/>• **Consumo total**: 800-1200W por nodo bajo carga máxima |

---
