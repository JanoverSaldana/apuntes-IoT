# IoT-Specific C4 Examples
# Ejemplos C4 Específicos para IoT

Esta guía presenta ejemplos completos de diagramas C4 aplicados a diferentes tipos de sistemas IoT, mostrando las particularidades y consideraciones especiales para este dominio.

## Características Especiales de Sistemas IoT

### 🌐 **Conectividad Diversa**
- Múltiples protocolos: MQTT, CoAP, LoRaWAN, Sigfox
- Conectividad intermitente y limitada
- Edge computing y procesamiento distribuido

### ⚡ **Restricciones de Recursos**
- Dispositivos con limitaciones de energía
- Ancho de banda limitado
- Capacidad de procesamiento reducida

### 📊 **Manejo de Datos**
- Grandes volúmenes de datos temporales
- Necesidad de procesamiento en tiempo real
- Almacenamiento distribuido

---

## Ejemplo 1: Smart Agriculture System

### Context Diagram (Mermaid)
```mermaid
graph TB
    subgraph "👥 Usuarios"
        U1[👤 Agricultor<br/>Gestiona cultivos]
        U2[👤 Técnico Agrícola<br/>Mantenimiento sensores] 
        U3[👤 Agrónomo<br/>Análisis de datos]
    end
    
    subgraph "🌱 Sistema Principal"
        S1[🏭 Sistema Agricultura Inteligente<br/><br/>• Monitoreo de cultivos<br/>• Automatización de riego<br/>• Optimización de producción]
    end
    
    subgraph "🌐 Sistemas Externos"
        E1[🌤️ Servicio Meteorológico<br/>API datos climáticos]
        E2[🛰️ Imágenes Satelitales<br/>Análisis cultivos]
        E3[💰 Precios de Mercado<br/>Info precios agrícolas]
        E4[💧 Sistema de Riego<br/>Infraestructura existente]
    end
    
    %% Conexiones usuarios
    U1 -->|App móvil<br/>Monitorea cultivos| S1
    U2 -->|Panel web<br/>Mantiene equipos| S1
    U3 -->|Dashboard<br/>Optimiza cultivos| S1
    
    %% Conexiones externas
    S1 -->|API REST<br/>Pronósticos| E1
    S1 -->|API REST<br/>Análisis imágenes| E2
    S1 -->|API REST<br/>Consulta precios| E3
    S1 -->|Modbus/TCP<br/>Control riego| E4
    
    %% Estilos
    classDef userStyle fill:#e1f5fe,stroke:#0277bd,stroke-width:2px
    classDef systemStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:3px
    classDef externalStyle fill:#fff3e0,stroke:#ef6c00,stroke-width:2px
    
    class U1,U2,U3 userStyle
    class S1 systemStyle
    class E1,E2,E3,E4 externalStyle
```

### Container Diagram (Mermaid)
```mermaid
graph TB
    subgraph "👥 Usuarios"
        U1[👤 Agricultor]
        U2[👤 Técnico]
    end
    
    subgraph "🌾 Sistema de Agricultura Inteligente"
        subgraph "📱 Interfaces"
            C1[📱 App Móvil<br/>React Native<br/>Monitoreo en campo]
            C2[💻 Portal Web<br/>Vue.js<br/>Configuración técnica]
            C3[📊 Dashboard<br/>Angular + D3.js<br/>Análisis avanzados]
        end
        
        subgraph "🔧 API Layer"
            C4[🚪 API Gateway<br/>Kong<br/>Autenticación]
        end
        
        subgraph "⚙️ Servicios"
            C5[📡 Servicio Dispositivos<br/>Node.js + TypeScript<br/>Gestión sensores]
            C6[🔄 Procesador Datos<br/>Python + Spark<br/>ETL agrícola]
            C7[🧠 Servicio ML<br/>Python + TensorFlow<br/>Predicciones]
            C8[📢 Notificaciones<br/>Go<br/>Alertas multi-canal]
        end
        
        subgraph "💾 Almacenamiento"
            C9[📈 InfluxDB<br/>Datos sensores]
            C10[🗄️ PostgreSQL<br/>Datos operacionales]
            C11[📊 ClickHouse<br/>Data Warehouse]
            C12[⚡ Redis Cluster<br/>Cache distribuido]
            C13[📬 Apache Kafka<br/>Streaming IoT]
        end
    end
    
    subgraph "🔌 Gateway"
        G1[🎛️ Gateway IoT<br/>Raspberry Pi<br/>Pre-procesamiento]
    end
    
    subgraph "🌐 Dispositivos"
        E1[📟 Sensores Campo<br/>ESP32 ambientales]
        E2[🚁 Drones Agrícolas<br/>Imágenes aéreas]
        E3[🌤️ Estación Meteorológica<br/>Clima local]
    end
    
    %% Conexiones usuarios
    U1 -->|HTTPS| C1
    U2 -->|HTTPS| C2
    
    %% Conexiones API
    C1 -->|REST API| C4
    C2 -->|REST API| C4
    C3 -->|REST API| C4
    
    %% Servicios internos
    C4 -->|HTTP| C5
    C4 -->|HTTP| C7
    C4 -->|HTTP| C8
    
    %% Datos
    C5 -->|SQL| C10
    C5 -->|InfluxQL| C9
    C5 -->|Kafka| C13
    C6 -->|Kafka| C13
    C6 -->|InfluxQL| C9
    C6 -->|SQL| C11
    C7 -->|SQL| C11
    C7 -->|Redis| C12
    
    %% Conexiones IoT
    E1 -->|LoRaWAN| G1
    E2 -->|WiFi| G1
    E3 -->|Modbus| G1
    G1 -->|MQTT/TLS| C5
    
    %% Estilos
    classDef userStyle fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef interfaceStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef apiStyle fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    classDef serviceStyle fill:#e8f5e8,stroke:#388e3c,stroke-width:2px
    classDef storageStyle fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    classDef gatewayStyle fill:#e0f2f1,stroke:#00796b,stroke-width:2px
    classDef deviceStyle fill:#fafafa,stroke:#616161,stroke-width:2px
    
    class U1,U2 userStyle
    class C1,C2,C3 interfaceStyle
    class C4 apiStyle
    class C5,C6,C7,C8 serviceStyle
    class C9,C10,C11,C12,C13 storageStyle
    class G1 gatewayStyle
    class E1,E2,E3 deviceStyle
```

---

## Ejemplo 2: Industrial IoT (IIoT) System

### Context Diagram (Mermaid)
```mermaid
graph TB
    subgraph "👥 Usuarios"
        U1[👤 Operador Planta<br/>Supervisa operaciones]
        U2[👤 Técnico Mantenimiento<br/>Mantiene equipos]
        U3[👤 Gerente Producción<br/>Decisiones estratégicas]
        U4[👤 Ingeniero Calidad<br/>Estándares calidad]
    end
    
    subgraph "🏭 Sistema Principal"
        S1[🏭 Plataforma Industrial IoT<br/><br/>• Monitoreo producción<br/>• Predicción de fallas<br/>• Optimización operaciones]
    end
    
    subgraph "🌐 Sistemas Empresariales"
        E1[📊 Sistema ERP<br/>Planificación recursos]
        E2[⚙️ Sistema MES<br/>Ejecución manufactura]
        E3[🎛️ Sistema SCADA<br/>Control y adquisición]
        E4[🔧 Sistema CMMS<br/>Gestión mantenimiento]
        E5[🚚 Sistemas Proveedores<br/>Cadena suministro]
    end
    
    %% Conexiones usuarios
    U1 -->|HMI/Dashboard<br/>Monitorea producción| S1
    U2 -->|App móvil<br/>Diagnostica fallas| S1
    U3 -->|Executive Dashboard<br/>Analiza KPIs| S1
    U4 -->|Quality Portal<br/>Monitorea calidad| S1
    
    %% Conexiones sistemas
    S1 -->|API REST<br/>Órdenes/Reportes| E1
    S1 -->|OPC UA<br/>Intercambio datos| E2
    S1 -->|OPC UA/Modbus<br/>Datos tiempo real| E3
    S1 -->|API REST<br/>Órdenes trabajo| E4
    S1 -->|EDI/API<br/>Datos inventario| E5
    
    %% Estilos
    classDef userStyle fill:#e8eaf6,stroke:#3f51b5,stroke-width:2px
    classDef systemStyle fill:#fff3e0,stroke:#ff9800,stroke-width:3px
    classDef externalStyle fill:#f3e5f5,stroke:#9c27b0,stroke-width:2px
    
    class U1,U2,U3,U4 userStyle
    class S1 systemStyle
    class E1,E2,E3,E4,E5 externalStyle
```

### Component Diagram - Predictive Maintenance Service (Mermaid)
```mermaid
graph TB
    subgraph "🖥️ Interfaces Externas"
        I1[🖥️ HMI Dashboard<br/>React + WebSocket<br/>Interfaz operador]
        I2[📱 App Mantenimiento<br/>Flutter<br/>App técnicos]
    end
    
    subgraph "💾 Almacenamiento Externo"
        D1[📊 InfluxDB<br/>Datos sensores]
        D2[🧠 MLflow<br/>Modelos entrenados]
        D3[🗄️ PostgreSQL<br/>Datos activos]
    end
    
    subgraph "📢 Servicios Externos"
        S1[📢 Servicio Notificaciones<br/>Python<br/>Alertas]
    end
    
    subgraph "🔧 Servicio Mantenimiento Predictivo"
        subgraph "🔌 API Layer"
            C1[🚪 API Controller<br/>FastAPI<br/>Endpoints REST]
        end
        
        subgraph "🔄 Procesamiento"
            C2[📥 Data Collector<br/>Python<br/>Recolecta sensores]
            C3[⚙️ Feature Engineer<br/>Pandas + NumPy<br/>Extrae características]
            C4[🚨 Anomaly Detector<br/>Scikit-learn<br/>Detecta anomalías]
            C5[🔮 Failure Predictor<br/>TensorFlow<br/>Predice fallas]
            C6[📅 Maintenance Scheduler<br/>Python<br/>Programa mantenimiento]
        end
        
        subgraph "💾 Repositorios"
            C7[🏭 Asset Repository<br/>SQLAlchemy<br/>Acceso activos]
            C8[📊 Sensor Repository<br/>InfluxDB Client<br/>Acceso temporal]
            C9[🧠 Model Manager<br/>MLflow Client<br/>Gestión ML]
        end
    end
    
    subgraph "🏭 Sistemas Industriales"
        E1[📟 Sensores Industriales<br/>Vibración, temperatura]
        E2[🎛️ Sistemas PLC<br/>Controladores lógicos]
    end
    
    %% Conexiones externas
    I1 -->|WebSocket/REST| C1
    I2 -->|HTTPS/REST| C1
    
    %% Flujo interno
    C1 -->|Consulta| C6
    C1 -->|Estado| C4
    
    C2 -->|Datos bruto| C3
    C3 -->|Características| C4
    C3 -->|Características| C5
    C4 -->|Anomalías| C6
    C5 -->|Predicciones| C6
    C6 -->|Alertas| S1
    
    %% Acceso a datos
    C7 -->|SQL| D3
    C8 -->|InfluxQL| D1
    C9 -->|API| D2
    
    %% Ingesta sensores
    E1 -->|Modbus/TCP| C2
    E2 -->|OPC UA| C2
    
    %% Estilos
    classDef interfaceStyle fill:#e8eaf6,stroke:#3f51b5,stroke-width:2px
    classDef storageStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef serviceStyle fill:#e0f2f1,stroke:#00695c,stroke-width:2px
    classDef apiStyle fill:#fff3e0,stroke:#ef6c00,stroke-width:2px
    classDef processStyle fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef repoStyle fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    classDef externalStyle fill:#fafafa,stroke:#616161,stroke-width:2px
    
    class I1,I2 interfaceStyle
    class D1,D2,D3 storageStyle
    class S1 serviceStyle
    class C1 apiStyle
    class C2,C3,C4,C5,C6 processStyle
    class C7,C8,C9 repoStyle
    class E1,E2 externalStyle
```

---

## Ejemplo 3: Smart City Monitoring

### Container Diagram (Mermaid)
```mermaid
graph TB
    subgraph "👥 Usuarios"
        U1[👤 Ciudadano]
        U2[👤 Operador Municipal]
        U3[👤 Servicios Emergencia]
    end
    
    subgraph "🏙️ Plataforma Ciudad Inteligente"
        subgraph "📱 Interfaces"
            C1[📱 App Ciudadana<br/>React Native<br/>Reportes ciudadanos]
            C2[🖥️ Centro Control<br/>Angular + Leaflet<br/>Monitoreo tiempo real]
            C3[🚨 Dashboard Emergencias<br/>React + WebRTC<br/>Respuesta emergencias]
        end
        
        subgraph "🔧 API Layer"
            C4[🚪 API Gateway<br/>AWS API Gateway<br/>Enrutamiento y auth]
        end
        
        subgraph "⚙️ Servicios"
            C5[🚗 Servicio Tráfico<br/>Java Spring Boot<br/>Optimización tráfico]
            C6[🌱 Servicio Ambiental<br/>Python FastAPI<br/>Calidad aire]
            C7[🚨 Servicio Emergencias<br/>Go<br/>Gestión incidentes]
            C8[📊 Servicio Analytics<br/>Scala + Akka<br/>Patrones urbanos]
        end
        
        subgraph "💾 Almacenamiento"
            C9[🚗 MongoDB<br/>Datos tráfico]
            C10[🌿 InfluxDB<br/>Datos ambientales]
            C11[🚨 PostgreSQL<br/>Incidentes]
            C12[🗺️ PostGIS<br/>Datos geoespaciales]
        end
        
        subgraph "🔄 Procesamiento"
            C13[⚡ Apache Flink<br/>Streams tiempo real]
            C14[📬 Apache Pulsar<br/>Mensajería escalable]
        end
    end
    
    subgraph "🌐 Sensores Urbanos"
        E1[🚦 Sensores Tráfico<br/>Cámaras y flujo]
        E2[🌬️ Calidad Aire<br/>PM2.5, NO2, O3]
        E3[🔊 Sensores Ruido<br/>Monitoreo acústico]
        E4[📹 Cámaras Emergencia<br/>CCTV + análisis]
        E5[🌤️ Estaciones Meteorológicas<br/>Clima urbano]
    end

' User interactions
Rel(citizen, citizen_app, "Reporta incidentes", "HTTPS")
Rel(city_operator, control_center, "Monitorea ciudad", "HTTPS")
Rel(emergency_responder, emergency_dashboard, "Gestiona emergencias", "HTTPS")

' API Gateway routing
Rel(citizen_app, api_gateway, "API calls", "HTTPS")
Rel(control_center, api_gateway, "API calls", "HTTPS")
Rel(emergency_dashboard, api_gateway, "API calls", "HTTPS")

Rel(api_gateway, traffic_service, "Traffic APIs", "HTTP")
Rel(api_gateway, environment_service, "Environment APIs", "HTTP")
Rel(api_gateway, emergency_service, "Emergency APIs", "HTTP")
Rel(api_gateway, analytics_service, "Analytics APIs", "HTTP")

' Service interactions
Rel(traffic_service, traffic_db, "Traffic data", "MongoDB")
Rel(environment_service, environmental_db, "Environmental data", "InfluxQL")
Rel(emergency_service, incidents_db, "Incident data", "SQL")
Rel(analytics_service, geospatial_db, "Geospatial queries", "PostGIS")

' Stream processing
Rel(stream_processor, message_hub, "Consumes streams", "Pulsar")
Rel(stream_processor, traffic_service, "Processed data", "HTTP")
Rel(stream_processor, environment_service, "Processed data", "HTTP")

' Sensor data ingestion
Rel(traffic_sensors, message_hub, "Traffic events", "MQTT")
    E2 -->|LoRaWAN| C14
    E3 -->|WiFi| C14
    E4 -->|RTMP| C14
    E5 -->|HTTP| C14
```

---

## Consideraciones Especiales para IoT

### 🔋 **Gestión de Energía** (Mermaid)
```mermaid
graph TB
    subgraph "📱 Dispositivo IoT"
        C1[📊 Sensor Reader<br/>C++<br/>Lee sensores optimizado]
        C2[🔋 Power Manager<br/>C<br/>Modos bajo consumo]
        C3[💾 Data Buffer<br/>EEPROM<br/>Buffer por lotes]
        C4[📡 Comm Scheduler<br/>C++<br/>Transmisiones eficientes]
    end
    
    %% Flujo de control energético
    C1 -->|Interrupt<br/>Request wake-up| C2
    C1 -->|SPI<br/>Store readings| C3
    C4 -->|SPI<br/>Read buffered data| C3
    C2 -->|Timer<br/>Wake for transmission| C4
    
    %% Estilos
    classDef sensorStyle fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef powerStyle fill:#fff3e0,stroke:#ef6c00,stroke-width:2px
    classDef bufferStyle fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    classDef commStyle fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    
    class C1 sensorStyle
    class C2 powerStyle
    class C3 bufferStyle
    class C4 commStyle
```

### 📡 **Conectividad Híbrida** (Mermaid)
```mermaid
graph TB
    subgraph "📟 Dispositivos IoT"
        D1[📡 Dispositivos LoRaWAN<br/>Largo alcance]
        D2[📶 Dispositivos WiFi<br/>Corto alcance]
        D3[🔵 Dispositivos Bluetooth<br/>Proximidad]
    end
    
    subgraph "🔌 Gateway IoT"
        C1[🔄 Protocol Adapter<br/>Python<br/>Multi-protocolo]
        C2[🌐 Connectivity Manager<br/>Python<br/>Gestión conexiones]
        C3[📊 Data Aggregator<br/>Python<br/>Agregación y compresión]
        C4[💾 Offline Buffer<br/>SQLite<br/>Buffer intermitente]
    end
    
    subgraph "🌍 Redes WAN"
        N1[📱 Red Celular<br/>Conectividad WAN]
        N2[🌐 Red Ethernet<br/>Conectividad LAN]
        N3[🛰️ Red Satelital<br/>Conectividad remota]
    end
    
    %% Entrada de datos
    D1 -->|LoRaWAN| C1
    D2 -->|MQTT/WiFi| C1
    D3 -->|Bluetooth LE| C1
    
    %% Procesamiento interno
    C1 -->|API interna<br/>Datos normalizados| C3
    C3 -->|SQLite<br/>Buffer datos| C4
    C2 -->|SQLite<br/>Sync online| C4
    
    %% Conectividad externa
    C2 -->|LTE/5G<br/>Conexión primaria| N1
    C2 -->|Ethernet<br/>Backup| N2
    C2 -->|Satellite<br/>Emergencia| N3
    
    %% Estilos
    classDef deviceStyle fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef gatewayStyle fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef networkStyle fill:#fff3e0,stroke:#ef6c00,stroke-width:2px
    
    class D1,D2,D3 deviceStyle
    class C1,C2,C3,C4 gatewayStyle
    class N1,N2,N3 networkStyle
```

### 🛡️ **Seguridad en IoT** (Mermaid)
```mermaid
graph TB
    subgraph "🛡️ Capa de Seguridad IoT"
        C1[🔐 Device Identity Manager<br/>HSM<br/>Certificados y claves]
        C2[🚀 Secure Boot<br/>Hardware<br/>Arranque seguro]
        C3[🔒 Crypto Engine<br/>mbedTLS<br/>Encriptación comunicaciones]
        C4[🔄 OTA Update Manager<br/>C++<br/>Actualizaciones seguras]
        C5[🚨 Threat Detector<br/>ML<br/>Detección amenazas]
    end
    
    %% Flujo de seguridad
    C2 -->|Hardware<br/>Verify certificates| C1
    C3 -->|Secure API<br/>Load keys| C1
    C4 -->|Digital signature<br/>Verify updates| C1
    C5 -->|Encrypted data<br/>Analyze traffic| C3
    
    %% Estilos
    classDef identityStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef bootStyle fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef cryptoStyle fill:#fff3e0,stroke:#ef6c00,stroke-width:2px
    classDef updateStyle fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef threatStyle fill:#ffebee,stroke:#d32f2f,stroke-width:2px
    
    class C1 identityStyle
    class C2 bootStyle
    class C3 cryptoStyle
    class C4 updateStyle
    class C5 threatStyle
```

---

## Patrones Arquitectónicos para IoT

### 🌊 **Lambda Architecture**
Procesamiento tanto en tiempo real como por lotes para IoT
```
Dispositivos IoT → Stream Processing (Real-time) → Serving Layer
                ↘ Batch Processing (Historical) ↗
```

### 🏗️ **Microservices with Event Sourcing**
```
Device Events → Event Store → Microservices → Read Models
```

### 🔄 **CQRS (Command Query Responsibility Segregation)**
```
Commands (Device Control) → Write Model
Queries (Data Analytics) → Read Model (Optimized)
```

## Métricas y Monitoreo

### 📊 **KPIs Importantes**
- **Device Health**: Uptime, battery level, signal strength
- **Data Quality**: Completeness, accuracy, timeliness
- **Network Performance**: Latency, throughput, packet loss
- **Security**: Failed authentication attempts, anomalies

### 🎯 **SLAs Típicos**
- **Availability**: 99.9% para sistemas críticos
- **Latency**: <100ms para control en tiempo real
- **Data Retention**: 1-7 años según regulaciones
- **Recovery Time**: <15 minutos para servicios críticos

## Visualización de Diagramas en GitHub

---

**� Resultado**: Los sistemas IoT con Mermaid ofrecen documentación arquitectónica viva que se mantiene sincronizada automáticamente en GitHub, facilitando la colaboración y el mantenimiento de proyectos complejos de Internet de las Cosas.