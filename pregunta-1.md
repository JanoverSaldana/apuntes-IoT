# Pregunta 1: Definition of System Requirements (4 puntos)

## Elabore el Definition of system requirements (los requisitos del sistema) en términos de Power Supply (Capacidades de suministro de energía) y restricciones de time-delay.

---

## 1. REQUISITOS DE SUMINISTRO DE ENERGÍA (Power Supply)

### 1.1 Capacidades de Suministro de Energía para el Piso LED

#### Consumo Máximo del Sistema
- **Densidad de energía máxima**: >570 W/m² para tecnología LumiFlex
- **Área de cancha estándar**: 420 m² (baloncesto) - 800 m² (instalaciones grandes)
- **Consumo total máximo**: 239.4 kW (cancha estándar) - 456 kW (instalación grande)
- **Tipo de conexión**: CA trifásica, 400V para instalaciones de 800 m²
- **Factor de demanda**: El sistema debe soportar condiciones de carga máxima (pantalla blanco sólido)

#### Consumo Promedio Operacional
- **Densidad promedio**: 190 W/m² durante operación normal
- **Consumo promedio**: 79.8 kW (cancha estándar) - 152 kW (instalación grande)
- **Eficiencia operacional**: 33.3% del consumo máximo para gestión de costos y generación de calor

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

#### Requisitos Críticos
- **Objetivo principal**: <100 ms para interacciones en tiempo real
- **Umbral aceptable**: <150 ms para aplicaciones no críticas
- **Umbral crítico**: <20 ms para interacciones de entrenamiento fluidas
- **Experiencia óptima**: <50 ms para la mayoría de aplicaciones interactivas

#### Casos de Uso Específicos
- **Seguimiento de jugadores en tiempo real**: <100 ms
- **Dibujo de jugadas por entrenador**: <150 ms
- **Animaciones durante descansos**: <200 ms (aceptable)
- **Retroalimentación de entrenamiento**: <50 ms

### 2.2 Latencia del Sistema de Seguimiento

#### Sistemas Ópticos (Cámaras de Alta Velocidad)
- **Rango objetivo**: <50 ms desde detección hasta datos disponibles
- **Rendimiento óptimo**: 15-52 ms (basado en sistemas de seguimiento ocular)
- **Frecuencia de captura**: 240-1000 fps para deportes de alta velocidad
- **Procesamiento de imagen**: Algoritmos optimizados para detección en tiempo real

#### Sistemas Basados en Sensores (IMU/RFID)
- **Latencia de sensor**: <20 ms para IMU en jugadores
- **Frecuencia de muestreo**: 100-500 Hz para movimientos deportivos
- **Transmisión inalámbrica**: <30 ms para protocolos de baja latencia
- **Fusión de datos**: <10 ms para combinar múltiples sensores

### 2.3 Latencia de Procesamiento (Edge Computing)

#### Edge Server Performance
- **Objetivo principal**: <10 ms para procesamiento local
- **Capacidad de CPU**: Procesamiento de datos de sensores en tiempo real
- **Capacidad de GPU**: Aceleración de algoritmos de visión artificial y IA/ML
- **Memoria RAM**: Buffer suficiente para procesamiento sin bloqueos
- **Almacenamiento NVMe**: Acceso rápido a algoritmos y modelos

#### Algoritmos de Procesamiento
- **Detección de objetos**: <5 ms por frame para IA optimizada
- **Seguimiento de trayectorias**: <3 ms para algoritmos de kalman filter
- **Renderizado de gráficos**: <8 ms para contenido visual complejo
- **Fusión de sensores**: <2 ms para combinación de múltiples fuentes

### 2.4 Latencia de Red

#### Red de Área Local (LAN)
- **Backbone de red**: <5 ms entre Edge servers y controladores LED
- **Protocolo recomendado**: Ethernet Gigabit (1 Gbps) mínimo
- **Infraestructura**: Switches dedicados para tráfico de tiempo real
- **QoS (Quality of Service)**: Priorización de tráfico crítico

#### Comunicación Inalámbrica
- **WiFi 6/6E**: <10 ms para sensores móviles
- **5G (donde aplicable)**: <1 ms para comunicaciones críticas
- **Protocolo MQTT**: Optimizado para IoT con latencia mínima

### 2.5 Latencia del Sistema de Visualización

#### Controladores LED
- **Frecuencia de actualización**: 3840 Hz mínimo para eliminar parpadeo
- **Latencia de frame**: 1-2 frames de retraso (20-40 ms a 50-60 fps)
- **Resolución de color**: Procesamiento en tiempo real sin degradación
- **Sincronización**: Sincronía perfecta entre múltiples paneles LED

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
