# 🚗 AlbaMove — Aparcamiento en Albacete

## 🎯 Objetivo
Ayudar a los ciudadanos de Albacete a encontrar aparcamiento rápido y reducir el tráfico perdido buscando plazas.

---

## 📌 Funcionalidades clave
- 🗺️ **Mapa en tiempo real** con plazas libres/ocupadas.  
- 🔍 Búsqueda por dirección o zona.  
- ℹ️ Detalle de parking: plazas, precio, horario.  
- 🧭 Botón “Navegar hasta aquí”.  
- ➕ Botón “Reportar plaza libre” (gamificación).  
- 🏆 Ranking de usuarios + recompensas (descuentos en zona azul o transporte).  

---

## 🔎 Método de detección — Sensores IoT en superficie
- Cada plaza lleva un **sensor IoT magnético o ultrasónico** en el suelo.  
- Detecta si hay un coche encima → envía estado **ocupado/libre**.  
- Comunicación: **LoRaWAN o NB-IoT** → Gateway IoT → Servidor municipal.  
- La web app consulta la **API municipal** para mostrarlo en tiempo real.  

### 🔧 Tipos de IoT recomendados
- **Sensores magnéticos LoRaWAN** (ej: Bosch, Libelium, Urbiotica).  
- Batería de larga duración (5–10 años).  
- Conexión: **LoRaWAN** o **NB-IoT** según cobertura.  

---

## 💻 Lenguajes y tecnologías
- **IoT Gateway:**  
  - Firmware en **C/C++** (Arduino / STM32).  
  - Protocolos: **LoRaWAN / MQTT**.  

- **Backend (API):**  
  - **Python** (FastAPI o Django REST).  
  - **PostgreSQL + PostGIS** (datos espaciales).  

- **Frontend (Web App):**  
  - **React.js + TailwindCSS**.  
  - Mapas con **Leaflet.js o Mapbox**.  

---

## 🗺️ Flujo de datos
```
+------------------+       +---------------------+
|                  |       |                     |
|   Ciudadano      |<----->|   AlbaMove WebApp   |
|  (Usuario final) | HTTPS |  (Frontend React)   |
|                  |       |                     |
+------------------+       +----------+----------+
                                      |
                                      | API REST
                                      v
                       +--------------+---------------+
                       |                              |
                       |   Servidor Backend           |
                       |   (FastAPI + PostgreSQL)     |
                       |                              |
                       +--------------+---------------+
                                      ^
                                      | MQTT / HTTP
                                      |
                       +--------------+---------------+
                       |                              |
                       |   Gateway IoT                |
                       |   (Raspberry Pi)             |
                       |                              |
                       +--------------+---------------+
                                      ^
                                      | LoRaWAN / NB-IoT
                                      |
                       +--------------+---------------+
                       |                              |
                       |   Sensores en plaza          |
                       |   (Nodos IoT: magnéticos)    |
                       |                              |
                       +------------------------------+ ```
