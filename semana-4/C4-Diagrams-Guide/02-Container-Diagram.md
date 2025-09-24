# IoT Container Diagram (Nivel 2)
# Diagrama de Contenedores IoT (Nivel 2)

El diagrama de contenedores IoT muestra la arquitectura técnica del ecosist### 🔌 **Dispositivos IoT (Edge Layer)**
- **Microcontroladores**: ESP32, Arduino, STM32 (C/C++)
- **Single Board Computers**: Raspberry Pi, BeagleBone (Python, Node.js)
- **Edge Computing**: NVIDIA Jetson, Intel NUC (Python, Docker)
- **Industrial PLCs**: Siemens, Allen-Bradley (Ladder Logic)

### 🌐 **Gateways y Conectividad**
- **Protocol Gateways**: Node-RED, Eclipse Kura
- **Edge Gateways**: AWS IoT Greengrass, Azure IoT Edge
- **Message Brokers**: Eclipse Mosquitto (MQTT), Apache Kafka
- **Network Infrastructure**: LoRaWAN servers, Cellular modules

### ☁️ **Servicios Cloud IoT**
- **IoT Platforms**: AWS IoT Core, Azure IoT Hub, Google Cloud IoT
- **Time-series Storage**: InfluxDB, Amazon TimeStream, Azure Data Explorer
- **Stream Processing**: Apache Kafka, AWS Kinesis, Azure Stream Analytics
- **Analytics**: Apache Spark, AWS Lambda, Azure Functions

### 📱 **Interfaces de Usuario IoT**
- **Mobile Apps**: React Native, Flutter (con MQTT/WebSocket)
- **Web Dashboards**: React + D3.js, Grafana, Node-RED Dashboard
- **Notification Services**: Firebase, AWS SNS, Twilio dispositivos, gateways, servicios cloud y aplicaciones de usuario.

## Propósito para IoT
## Purpose for IoT

- **Arquitectura distribuida**: Dispositivos, edge computing, cloud, aplicaciones
- **Tecnologías IoT**: Protocolos (MQTT, LoRa), plataformas (AWS IoT), firmware
- **Conectividad**: Redes inalámbricas, gateways, APIs
- **Procesamiento**: Edge computing vs cloud computing
- **Restricciones**: Energía, ancho de banda, latencia

## Audiencia y Enfoque IoT

- **Audiencia**: Arquitectos IoT, ingenieros de firmware, desarrolladores backend
- **Nivel de detalle**: Arquitectura técnica con protocolos específicos
- **Pregunta clave**: "¿Cómo están distribuidos los componentes desde dispositivos hasta la nube?"

## ¿Qué es un Contenedor IoT?

Un contenedor IoT representa una **unidad ejecutable** en el ecosistema:
- **Dispositivos**: Sensores, actuadores, gateways
- **Servicios cloud**: Plataformas IoT, APIs, procesamiento
- **Aplicaciones**: Móviles, web, dashboards
- **Almacenamiento**: Bases de datos time-series, operational data
- **Comunicación**: Message brokers, API gateways

## Elementos del Diagrama

### 📦 **Contenedores**
- Aplicaciones, servicios, bases de datos
- Tecnología específica (Node.js, PostgreSQL, etc.)
- Responsabilidades claras

### 👥 **Personas/Sistemas Externos**
- Mismos actores del diagrama de contexto
- Sistemas externos que interactúan

### ↔️ **Relaciones**
- Protocolos de comunicación específicos
- Puertos y tecnologías
- Flujo de datos

## Diagrama con Mermaid

```mermaid
graph TB
    subgraph "👥 Usuarios"
        U1[👤 Agricultor]
        U2[👤 Técnico]
    end
    
    subgraph "📱 Frontend Layer"
        F1[📱 App Móvil<br/>React Native<br/>Monitoreo en tiempo real]
        F2[🌐 Dashboard Web<br/>React.js<br/>Panel de control técnico]
    end
    
    subgraph "🔗 API Gateway"
        A1[🚪 API Gateway<br/>Node.js + Express<br/>Punto de entrada unificado]
    end
    
    subgraph "⚙️ Business Services"
        B1[🔧 Servicio Dispositivos<br/>Python + FastAPI<br/>Gestión sensores IoT]
        B2[📊 Procesador Datos<br/>Python + Celery<br/>Análisis de sensores]
        B3[🔔 Servicio Notificaciones<br/>Node.js<br/>Alertas multi-canal]
    end
    
    subgraph "💾 Data Layer"
        D1[📈 InfluxDB<br/>Time Series<br/>Datos históricos sensores]
        D2[🗄️ PostgreSQL<br/>Operational DB<br/>Config, usuarios, dispositivos]
        D3[📨 Redis/RabbitMQ<br/>Message Broker<br/>Cola mensajes asíncrona]
    end
    
    subgraph "🌐 External Systems"
        E1[📡 Sensores IoT<br/>ESP32<br/>Sensores ambientales]
        E2[🌤️ API Meteorológica<br/>Datos climáticos externos]
        E3[📧 Servicio Email<br/>SendGrid/AWS SES<br/>Notificaciones]
    end
    
    %% User interactions
    U1 -->|HTTPS| F1
    U2 -->|HTTPS| F2
    
    %% Frontend to API
    F1 -->|HTTPS/REST| A1
    F2 -->|HTTPS/REST| A1
    
    %% API to Services
    A1 -->|HTTP/REST| B1
    A1 -->|HTTP/REST| B3
    
    %% Service interactions
    B1 -->|SQL| D2
    B1 -->|InfluxQL| D1
    B1 -->|AMQP| D3
    
    B2 -->|AMQP| D3
    B2 -->|InfluxQL| D1
    B2 -->|HTTP/REST| B3
    
    B3 -->|HTTPS/API| E3
    
    %% External connections
    E1 -->|MQTT| B1
    B2 -->|HTTPS/REST| E2
    
    %% Estilos
    classDef userStyle fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef frontendStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef apiStyle fill:#fff3e0,stroke:#f57c00,stroke-width:3px
    classDef serviceStyle fill:#e8f5e8,stroke:#388e3c,stroke-width:2px
    classDef dataStyle fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    classDef externalStyle fill:#fff8e1,stroke:#fbc02d,stroke-width:2px
    
    class U1,U2 userStyle
    class F1,F2 frontendStyle
    class A1 apiStyle
    class B1,B2,B3 serviceStyle
    class D1,D2,D3 dataStyle
    class E1,E2,E3 externalStyle
```

## Ejemplo Visual (Texto)

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                          DIAGRAMA DE CONTENEDORES                              │
├─────────────────────────────────────────────────────────────────────────────────┤
│                                                                                 │
│ 👤 Agricultor                    👤 Técnico                                    │
│     │                               │                                           │
│     │ HTTPS                        │ HTTPS                                    │
│     ▼                               ▼                                           │
│ ┌─────────────┐                 ┌─────────────┐                               │
│ │  App Móvil  │                 │ Dashboard   │                               │
│ │ React Native│                 │ React.js    │                               │
│ └─────────────┘                 └─────────────┘                               │
│     │                               │                                           │
│     │ HTTPS/REST                   │ HTTPS/REST                               │
│     ▼                               ▼                                           │
│ ┌─────────────────────────────────────────────────────────────┐               │
│ │                  API Gateway                                │               │
│ │                Node.js + Express                            │               │
│ └─────────────────────────────────────────────────────────────┘               │
│     │                               │                                           │
│     │ HTTP/REST                    │ HTTP/REST                                │
│     ▼                               ▼                                           │
│ ┌─────────────┐  Redis/AMQP   ┌─────────────┐      HTTP/REST  ┌─────────────┐ │
│ │ Servicio de │◄─────────────►│ Procesador  │◄───────────────►│ Servicio de │ │
│ │ Dispositivos│               │ de Datos    │                 │Notificaciones│ │
│ │Python+FastAPI│              │Python+Celery│                 │   Node.js   │ │
│ └─────────────┘               └─────────────┘                 └─────────────┘ │
│     │                               │                               │           │
│     │ SQL                          │ InfluxQL                      │ HTTPS/API │
│     ▼                               ▼                               ▼           │
│ ┌─────────────┐               ┌─────────────┐                 📧 Email        │
│ │PostgreSQL   │               │  InfluxDB   │                   Service       │
│ │(Operacional)│               │(Temporal)   │                                 │
│ └─────────────┘               └─────────────┘                                 │
│                                                                                 │
│ 📡 Sensores IoT ──MQTT/HTTP──► Servicio de Dispositivos                       │
│                                                                                 │
└─────────────────────────────────────────────────────────────────────────────────┘
```

## Tipos de Contenedores en IoT

### 🖥️ **Aplicaciones Web**
- **Dashboard administrativo**: React, Angular, Vue
- **Panel de monitoreo**: Grafana, custom dashboards
- **Portal de configuración**: Django, Rails

### 📱 **Aplicaciones Móviles**
- **Apps nativas**: Swift (iOS), Kotlin (Android)
- **Apps híbridas**: React Native, Flutter, Ionic
- **PWAs**: Progressive Web Apps

### 🔧 **APIs y Microservicios**
- **API Gateway**: Kong, AWS API Gateway, Nginx
- **Servicios de dominio**: Node.js, Python, Java, Go
- **Procesamiento de datos**: Apache Kafka, Apache Storm

### 💾 **Almacenamiento**
- **Bases de datos relacionales**: PostgreSQL, MySQL
- **Bases de datos de series temporales**: InfluxDB, TimescaleDB
- **Bases de datos NoSQL**: MongoDB, Cassandra
- **Cache**: Redis, Memcached

### 🔄 **Mensajería**
- **Message brokers**: RabbitMQ, Apache Kafka
- **Colas**: Redis, AWS SQS
- **Pub/Sub**: MQTT broker (Mosquitto, HiveMQ)

## Checklist para Diagramas IoT

### ✅ **Identificación de dispositivos y edge:**
- [ ] ¿Qué tipos de sensores/actuadores necesitamos?
- [ ] ¿Necesitamos gateways o edge computing?
- [ ] ¿Qué protocolos de comunicación (MQTT, LoRa, WiFi)?
- [ ] ¿Hay procesamiento local en dispositivos?

### ✅ **Arquitectura cloud y servicios:**
- [ ] ¿Qué plataforma IoT cloud (AWS IoT, Azure IoT)?
- [ ] ¿Necesitamos time-series database?
- [ ] ¿Qué servicios de analytics en tiempo real?
- [ ] ¿Cómo manejamos escalabilidad de dispositivos?

### ✅ **Interfaces y usuarios:**
- [ ] ¿Apps móviles para usuarios finales?
- [ ] ¿Dashboards web para operadores?
- [ ] ¿Sistemas de alertas y notificaciones?
- [ ] ¿Integración con sistemas empresariales?

### ✅ **Conectividad y protocolos:**
- [ ] MQTT brokers y topics structure
- [ ] APIs REST para configuración
- [ ] WebSockets para real-time updates
- [ ] Protocolos de red específicos (LoRaWAN, Sigfox)

## Patrones Comunes en IoT

### 🏗️ **Arquitectura por Capas**
```
Frontend (App/Web) → API Gateway → Servicios → Base de Datos
```

### 🔄 **Event-Driven Architecture**
```
Dispositivos → Message Broker → Procesadores → Notificaciones
```

### 🌐 **Microservicios**
```
- Servicio de Dispositivos
- Servicio de Usuarios  
- Servicio de Datos
- Servicio de Notificaciones
```

## Consideraciones Especiales para IoT

### 📡 **Conectividad de Dispositivos**
- MQTT brokers para comunicación eficiente
- Protocolos específicos (LoRaWAN, Sigfox)
- Gateways para agregación de datos

### ⚡ **Procesamiento en Tiempo Real**
- Stream processing (Apache Kafka, Apache Storm)
- Edge computing containers
- Time-series databases optimizadas

### 🔒 **Seguridad**
- Certificate management services
- API authentication/authorization
- Device identity management

## Errores Comunes

### ❌ **Evitar:**
- Incluir componentes internos de un contenedor
- Mostrar múltiples instancias del mismo contenedor
- Omitir tecnologías específicas
- No especificar protocolos de comunicación

### ✅ **Mejor práctica:**
- Un contenedor = una aplicación ejecutable
- Incluir tecnología específica en cada contenedor
- Mostrar dependencias claras
- Documentar decisiones arquitectónicas

## Siguientes Pasos

1. **Validar** la arquitectura con el equipo técnico
2. **Continuar** con [Diagrama de Componentes](./03-Component-Diagram.md) para contenedores complejos
3. **Planificar** la infraestructura y despliegue
4. **Documentar** APIs y interfaces entre contenedores

### Ventajas del diagrama Mermaid para IoT

#### ✅ **Arquitectura en capas claramente definida:**
- **Frontend Layer**: Interfaces de usuario (móvil y web)
- **API Gateway**: Punto único de entrada y gestión de APIs
- **Business Services**: Lógica específica de IoT (dispositivos, datos, notificaciones)
- **Data Layer**: Almacenamiento especializado (time-series, operational, messaging)
- **External Systems**: Integración con ecosistema IoT

#### 🎨 **Personalización visual:**
- **Colores diferenciados** por tipo de componente
- **Iconos descriptivos** para mejor comprensión
- **Protocolos específicos** en las conexiones
- **Agrupación lógica** por responsabilidades

#### � **Variantes para diferentes vistas:**

**Vista simplificada para ejecutivos:**
```mermaid
graph LR
    A[� Apps] --> B[🚪 API] --> C[⚙️ Servicios] --> D[💾 Datos]
    E[📡 Dispositivos IoT] --> C
```

**Vista de flujo de datos:**
```mermaid
graph TD
    A[📡 Sensores] --> B[📨 Message Queue]
    B --> C[📊 Data Processor]
    C --> D[📈 Time Series DB]
    C --> E[� Notifications]
```

---

**💡 Tip**: Este diagrama debe ser la base para definir el stack tecnológico y planificar el desarrollo de cada contenedor por separado.