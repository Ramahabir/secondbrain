This project integrates IoT devices, a backend with machine learning & chatbot, and a frontend dashboard to monitor, predict, and interact with solar panel performance in real time.
## 📌 Overview

The system collects real sensor data (power, temperature, humidity) via ESP32, sends it to a FastAPI backend where it is processed, stored, and used for energy prediction (with ML + Open-Meteo API). A Next.js frontend provides a live dashboard and a chatbot interface for user interaction.

```

   [ESP32 + Sensors]  -->  [FastAPI Backend]  -->  [Database + ML + OpenMeteo API]

         |                         |                      |

   INA219 (power)                  |                      |

   DHT22 (temperature)             |                      |

                                   v                      v

                          [Next.js Frontend]   <-->   [Chatbot (LangGraph)]

  

```

  3 Main Concepts:

  

- Frontend (Next.js) → Displays dashboard and chatbot UI.

- IoT (ESP32) → Collects real-world sensor data.

- Backend (FastAPI) → Handles routing, storage, chatbot (LangGraph), and prediction.

  
  

## 💻 Front End ( Next.js )

The frontend is built with Next.js + React, styled with TailwindCSS, and uses Recharts for data visualization. It provides a modern and responsive interface where users can explore live sensor data, predictions, and interact with the chatbot.

  

### 🌐 Routes

  

1. /dashboard

  

    - Displays real-time sensor data (voltage, current, power, temperature).

  

    - Interactive line & bar charts (Recharts) for:

  

        - Power vs Time

  

        - Temperature vs Time

  

        - Daily Energy Summary

  

    - Auto-refreshes data via backend API.

  

2. /insight

  

    - Provides analytics & predictions from the backend.

  

    - Shows historical trends (daily, weekly, monthly).

  

    - Displays ML-powered future energy forecasts.

  

    - Correlation graphs (e.g., temperature vs power efficiency).

  

3. /setting

  

    - User configuration panel.

  

    - Options to adjust:

  

        - IoT Integration

        - Panel Specification

4. /chatbot

  

    - Interactive AI chatbot interface.

  

    - Users can ask questions like:

  

        - “What’s my total energy today?”

  

        - “Show me yesterday’s performance.”

  

        - “Predict my solar output for tomorrow.”

  

    - Connected to LangGraph + FastAPI backend, fetching live data & predictions.

  

## 🔧 Backend

The backend acts as the data hub for the system, providing:

  

 - Data ingestion from IoT devices (ESP32).

  

 - Prediction service for solar panel performance.

  

 - Chatbot service powered by LangGraph + Gemini 2.5 Flash with RAG.

  

 - API endpoints consumed by the Next.js frontend.

  

### 📡 Api Routes

1. __POST /data__

  

Receives JSON data from IoT devices (ESP32)

  

**Payload Example**:

  
```
    {

    "timestamp": "2025-08-19T10:00:00Z",

    "voltage": 12.5,

    "current": 1.2,

    "power": 15.0,

    "ambient_temp": 32.4,

    "module_temp": 35.1,

    "irradiance": 820

    }
```
  

2. __GET /predict__

  

Generates solar power output predictions based on irradiance, ambient temperature, and module temperature.

  

Uses Open-Meteo API for weather forecast data.

  

Applies ML model trained on historical sensor + weather data.

  

**Response Example**:

  
```
    {

    "timestamp": "2025-08-20T10:00:00Z",

    "irradiance": 810,

    "ambient_temp": 30.2,

    "module_temp": 33.5,

    "predicted_power_output": 14.7

    }
```
  

3. __POST /chat__

  

Backend route for LangGraph chatbot.

  

- Powered by Gemini 2.5 Flash.

  

- Uses RAG (Retrieval Augmented Generation) with solar panel condition data (from DB + predictions).

  

- Allows natural language interaction with system insights.

  

**Example Input**:

  
```
    { "message": "What is my predicted power output tomorrow?" }
```
	  
  

**Example Output**:

  

```
    {

    "response": "Based on tomorrow’s forecast, your panels are expected to produce around 15.2W at peak hours, with higher efficiency in the morning due to lower module temperatures."

    }
```

  

⚙️ Key Components

  

- FastAPI → lightweight backend framework.

  

- Database → stores raw + processed sensor data.

  

- Open-Meteo API → external weather forecasts.

  

- Machine Learning → time-series prediction for power output.

  

- LangGraph + Gemini 2.5 Flash → chatbot pipeline with RAG for solar panel data.