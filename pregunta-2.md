# Pregunta 2: Definition of Physical Layer Requirements (5 puntos)

## Elabore el Definition of physical layer requirements (los requisitos para el Physical Layer de la IoT Solution). Considere: a) número y tipos de nodos sensores y actuators; b) Target uncertainty (incertidumbre objetivo), relacionada con las cantidades físicas medidas por cada sensor; c) Target accuracy and precision (Exactitud y precisión objetivo) de los actuadores; d) Processing Power (Esfuerzo computacional) para los algoritmos de procesamiento de datos que se implementarán en el Edge node.

---

## A) NÚMERO Y TIPOS DE NODOS SENSORES Y ACTUADORES

### A.1 Nodos Sensores

#### Sistemas de Seguimiento Óptico (Según enunciado)
**Descripción**: Múltiples cámaras de alta velocidad ubicadas estratégicamente en el estadio (enunciado)
- **Función**: Capturan video a altas velocidades de fotogramas para seguimiento preciso y triangulación 3D (enunciado)
- **Ubicación**: Alrededor del estadio desde diferentes ángulos (enunciado)
- **Procesamiento**: Software de visión artificial procesa datos de video para ubicación precisa 3D (enunciado)
- **Ejemplos mencionados**: Hawk-Eye como sistema ampliamente utilizado (enunciado)
- **Integración**: Los datos se introducen en GlassCourt OS para mostrar gráficos dinámicos (enunciado)
- **Outputs**: Trayectorias de jugadores, zonas de tiro, superposiciones estadísticas (enunciado)
- **Número**: Múltiples cámaras según cobertura necesaria y objetos a rastrear (enunciado)

#### Sensores Basados en Red de Anclaje (Según enunciado)
**Descripción**: Red de sensores de anclaje ubicados en las instalaciones (enunciado)
- **Función**: Comunicarse con pequeñas etiquetas de seguimiento que llevan los jugadores (enunciado)
- **Ejemplo específico**: ShotTracker como socio de ASB mencionado en enunciado
- **Implementación**: Dispositivos de captura colocados en la cancha (enunciado)
- **Jugadores**: Cada jugador lleva un sensor para localización continua (enunciado)
- **Balón**: Sensores integrados en el balón para rastrear posición y velocidad de giro (enunciado)
- **Integración**: Datos se transfieren al sistema operativo GlassCourt (enunciado)
- **Capacidades**: Proyectar diagramas de entrenamiento en tiempo real (enunciado)
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
- **LumiFlex**: Matriz de alta densidad para versión avanzada (enunciado)
- **Señalización básica**: Tiras LED integradas más sencillas para líneas multideportivas (enunciado)
- **Determinación de cantidad**: Depende directamente del tamaño de cancha y resolución deseada (enunciado)
- **Integración**: Sincronización perfecta con pantallas LED y cubos de video (enunciado)
- **Control**: Sistema operativo GlassCourt controla LEDs para mostrar imágenes dinámicas (enunciado)

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
- **Propósito**: Garantizar visualización fiable de ubicaciones de jugadores y balón (enunciado)
- **Importancia**: Para que las mediciones de sensores sean útiles, incertidumbre debe ser mínima (enunciado)
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
- **Propósito**: Mantener sincronización precisa de datos de diversas fuentes (enunciado)
- **Importancia**: Requisito fundamental para rendimiento constante del sistema (enunciado)
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
- **Propósito**: Obtener gráficos nítidos y salida visual fluida en toda la cancha (enunciado)
- **Requerimiento**: Controladores LED y sistemas de control de alta calidad (enunciado)
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
- **CPU de alto rendimiento**: Gestiona control del sistema, tráfico de red y procesamiento de datos (enunciado)
- **GPU de alto rendimiento**: Acelera visión artificial, análisis de IA/ML y tareas de renderizado (enunciado)
- **Memoria de alta velocidad**: Adecuada para soportar alto rendimiento de datos (enunciado)
- **Almacenamiento de alta velocidad**: Esencial para demandas de procesamiento en tiempo real (enunciado)  
- **Interfaces de red de alta velocidad**: Esenciales para soportar alto rendimiento de datos en tiempo real (enunciado)

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
