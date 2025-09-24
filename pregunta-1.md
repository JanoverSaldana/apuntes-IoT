# Pregunta 1: Definition of System Requirements (4 puntos)

## Elabore el Definition of system requirements (los requisitos del sistema) en términos de Power Supply (Capacidades de suministro de energía) y restricciones de time-delay.

---

## 1. REQUISITOS DE SUMINISTRO DE ENERGÍA (Power Supply)

### 1.1 Capacidades de Suministro de Energía para el Piso LED

#### Consumo Máximo del Sistema
- **Densidad de energía máxima**: >570 W/m² para tecnología LumiFlex (según enunciado)
- **Área de cancha estándar**: 420 m² (baloncesto estándar según enunciado)
- **Área de instalación grande**: 800 m² (según enunciado para pisos grandes)
- **Consumo total máximo**: 
  - Cancha estándar (420 m²): 239.4 kW (570 × 420 = 239,400 W)
  - Instalación grande (800 m²): 456 kW (570 × 800 = 456,000 W)
- **Tipo de conexión**: CA trifásica con salida de 400 voltios (según enunciado para 800 m²)
- **Factor de demanda**: Condiciones de carga máxima como mostrar blanco sólido (según enunciado)

#### Consumo Promedio Operacional
- **Densidad promedio**: 190 W/m² durante operación normal (según enunciado)
- **Consumo promedio**: 
  - Cancha estándar (420 m²): 79.8 kW (190 × 420 = 79,800 W)
  - Instalación grande (800 m²): 152 kW (190 × 800 = 152,000 W)
- **Eficiencia operacional**: 33.3% del consumo máximo (190/570) para administrar costos operativos y generación de calor (según enunciado)

#### Alimentación de Componentes Críticos
- **Edge Servers**: 
  - CPU de alto rendimiento: 200-300W por nodo
  - GPU para procesamiento IA/ML: 300-500W por nodo
  - Sistemas de red y almacenamiento: 100-150W por nodo
  - **Total por Edge Node**: 600-950W

- **Sistemas de Control LED**:
  - Controladores de alta frecuencia (3840 Hz): 50-100W por controlador
  - Múltiples controladores según resolución y tamaño de cancha

#### Requisitos de Redundancia y Confiabilidad
- **Sistema UPS (Uninterruptible Power Supply)**:
  - Cobertura mínima: Edge servers y sistemas de control críticos
  - Capacidad: 15-30 minutos de autonomía para apagado elegante
  - Protección contra fluctuaciones y cortes de energía

- **Integración con sistemas de emergencia**:
  - Conexión con generadores de emergencia del estadio
  - Sistemas de respaldo automático para eventos en vivo
  - Monitoreo continuo de la calidad de energía

### 1.2 Distribución y Gestión Energética

#### Arquitectura de Distribución
- **Alimentación principal**: Conexión directa a subestación del estadio
- **Distribución secundaria**: Paneles de distribución redundantes
- **Protección**: Sistemas de protección diferencial y sobrecarga
- **Monitoreo**: Medición en tiempo real de consumo por zona

---

## 2. RESTRICCIONES DE TIME-DELAY (Latencia del Sistema)

### 2.1 Latencia de Extremo a Extremo (Percepción del Usuario)

#### Requisitos Críticos (Según enunciado específico)
- **Objetivo principal**: <100 ms para interacciones fluidas e instantáneas (enunciado)
- **Umbral aceptable**: Hasta 150 ms marginalmente aceptable para animaciones en descansos (enunciado)
- **Umbral crítico**: <20 ms ideal para interacciones fluidas (enunciado)
- **Experiencia óptima**: <50 ms generalmente aceptable para aplicaciones interactivas (enunciado)
- **Meta del sistema**: Significativamente inferior a 100 ms para elementos interactivos (enunciado)

#### Casos de Uso Específicos
- **Seguimiento de jugadores en tiempo real**: <100 ms
- **Dibujo de jugadas por entrenador**: <150 ms
- **Animaciones durante descansos**: <200 ms (aceptable)
- **Retroalimentación de entrenamiento**: <50 ms

### 2.2 Latencia del Sistema de Seguimiento

#### Sistemas Ópticos (Cámaras de Alta Velocidad)
- **Rango objetivo**: Pocas decenas de milisegundos, preferiblemente <50 ms (enunciado)
- **Rendimiento documentado**: 15-52 ms para sistemas de seguimiento ocular (enunciado)
- **Frecuencia de captura**: Altas velocidades de fotogramas para seguimiento preciso (enunciado)
- **Procesamiento**: Software de visión artificial para triangulación 3D (enunciado)
- **Impacto**: Latencia alta afecta capacidad de respuesta del suelo LED (enunciado)

#### Sistemas Basados en Sensores (IMU/RFID)
- **Latencia de sensor**: <20 ms para IMU en jugadores
- **Frecuencia de muestreo**: 100-500 Hz para movimientos deportivos
- **Transmisión inalámbrica**: <30 ms para protocolos de baja latencia
- **Fusión de datos**: <10 ms para combinar múltiples sensores

### 2.3 Latencia de Procesamiento (Edge Computing)

#### Edge Server Performance (Especificaciones del enunciado)
- **Objetivo principal**: Milisegundos de un solo dígito bajo, idealmente <10 ms (enunciado)
- **Configuración de CPU**: CPU de alto rendimiento para control del sistema, tráfico de red y procesamiento de datos (enunciado)
- **Configuración de GPU**: GPU de alto rendimiento para acelerar visión artificial, análisis IA/ML y renderizado (enunciado)
- **Memoria y almacenamiento**: Alta velocidad adecuados para alto rendimiento de datos en tiempo real (enunciado)
- **Interfaces de red**: Alta velocidad esenciales para demandas de procesamiento en tiempo real (enunciado)

#### Algoritmos de Procesamiento
- **Detección de objetos**: <5 ms por frame para IA optimizada
- **Seguimiento de trayectorias**: <3 ms para algoritmos de kalman filter
- **Renderizado de gráficos**: <8 ms para contenido visual complejo
- **Fusión de sensores**: <2 ms para combinación de múltiples fuentes

### 2.4 Latencia de Red

#### Red de Área Local (LAN) - Especificaciones del enunciado
- **Latencia objetivo**: Idealmente <5-10 ms dentro de la LAN que conecta Edge server al piso LED (enunciado)
- **Infraestructura requerida**: Rápida y confiable, ejemplo Ethernet (enunciado)
- **Consideración 5G**: Potencialmente 5G para conexiones inalámbricas (enunciado)
- **Impacto**: Latencia alta puede introducir retrasos significativos si se transfieren datos sin procesar (enunciado)
- **Beneficio Edge**: Edge processing mitiga esto reduciendo datos enviados por red (enunciado)

#### Comunicación Inalámbrica
- **WiFi 6/6E**: <10 ms para sensores móviles
- **5G (donde aplicable)**: <1 ms para comunicaciones críticas
- **Protocolo MQTT**: Optimizado para IoT con latencia mínima

### 2.5 Latencia del Sistema de Visualización

#### Controladores LED (Especificaciones exactas del enunciado)
- **Latencia de pantallas profesionales**: 1-2 cuadros de retraso (enunciado)
- **Velocidades de cuadro**: 50-60 fps comunes (o más altas hasta 240 fps para alta velocidad) (enunciado)
- **Latencia equivalente**: ~20-40 ms (1 cuadro a 50 fps = 20 ms, 2 cuadros = 40 ms) (enunciado)
- **Frecuencia de actualización**: 3840 Hz fundamental para imágenes fluidas sin parpadeos (enunciado)
- **Importancia**: Crítico para grabación con cámaras alta velocidad o visualización humana (enunciado)
- **Sincronización**: Retroalimentación visual sincronizada con acciones de atleta (enunciado)

#### Optimizaciones de Rendimiento
- **Buffer de video**: Minimizado para reducir latencia
- **Compresión**: Algoritmos de baja latencia para transmisión
- **Calibración**: Corrección de color y brillo en tiempo real

---

## 3. CONSIDERACIONES DE INTEGRACIÓN

### 3.1 Gestión de Recursos
- **Balanceamiento de carga**: Distribución eficiente entre múltiples Edge nodes
- **Escalabilidad horizontal**: Capacidad de agregar nodos según demanda
- **Failover automático**: Redundancia activa para componentes críticos

### 3.2 Monitoreo y Mantenimiento
- **Telemetría en tiempo real**: Monitoreo de todos los parámetros de latencia
- **Alertas proactivas**: Notificación antes de superar umbrales críticos
- **Mantenimiento predictivo**: Análisis de tendencias para prevenir fallas

### 3.3 Cumplimiento de Estándares
- **Estándares deportivos**: Compatibilidad con regulaciones de ligas profesionales
- **Seguridad eléctrica**: Cumplimiento con normativas IEC y locales
- **Certificaciones**: CE, FCC para componentes electrónicos
