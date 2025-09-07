# 🌱 AI Agronomy Agent – n8n Workflow (100% Mistral AI 🇫🇷)

![Workflow](screenshots/workflow.png)

## Overview

This project implements a **multi-agent decision-support system for agronomy**, fully powered by **Mistral AI** (state-of-the-art French LLM).  
The workflow is built in **n8n** and connects several specialized agents to:  

- 📊 **Analyze agronomic data** (soil analyses, soil tension, phenological stage).  
- 🌦️ **Integrate weather and ETP** to refine irrigation recommendations.  
- 📩 **Notify the user in real time** (Discord, Gmail).  
- 🗓️ **Archive reports** into Google Calendar for traceability.  
- 💬 **Enable conversational interaction**: ask the agent questions and trigger an analysis or alert automatically.  

👉 100% powered by **Mistral AI**, ensuring sovereignty and performance.  

---

## 🧩 Agent Architecture

### **Mistral Agent 1 – Conversational**
- Triggered by a message (`When chat message received`).  
- Connected to **Google Sheets**:  
  - `analyses_sol` (soil physico-chemical properties).  
  - `configuration_parcelle` (crop and sensor parameters).  
- Dynamically generates a **structured JSON** (session_id, tension, rooting depth, stage, etc.).  
- Triggers the **second workflow via HTTP Request**.  

### **Mistral Agent 2 – Irrigation Analysis**
- Receives field data through `Webhook Station Mesures`.  
- Performs hydric analysis with:  
  - 🌡️ Real-time weather (WeatherAPI).  
  - 💧 Hourly ETP (Open-Meteo).  
- Triggers:  
  - **Discord** → notification / hydric stress alert.  
  - **Gmail** → detailed report to the user.  

### **Mistral Agent 3 – Archiving**
- Cleans and reformulates messages.  
- Creates a **Google Calendar event** named *“Agricultural report”*.  
- Stores a clear and dated summary of the field status.  

---

## 🚀 Use cases

- **Hydric monitoring**: soil tension + weather → irrigation recommendations.  
- **Hydric stress alerts**: if dendrometer indicates stress → automatic Discord + mail alert.  
- **Agronomic reporting**: store daily summaries in Google Calendar.  
- **Conversational interface**: direct dialogue with the agent to obtain diagnostics or trigger workflows.  

---

## ⚙️ Installation & usage

1. Import the file `Agent_IA_Agronomie_Final.json` into n8n.  
2. Configure credentials:  
   - Mistral Cloud account (API key).  
   - Google Sheets (analyses_sol, configuration_parcelle).  
   - Gmail, Discord, Google Calendar.  
3. Launch the workflow and interact via the conversational agent.  

---

## 💾 Repository structure

```
Agent_IA_Agronomie/                       
├── README_fr.md                        # Complete project overview (French version)  
├── README_en.md                        # Project overview (this file, English version)  
│
├── screenshots/                        # Visual demos and captures  
│   ├── calendar.png                    # Example of archiving in Google Calendar  
│   ├── message_Discord.png             # Real-time alert sent to Discord  
│   ├── workflow.png                    # Global view of the n8n multi-agent workflow  
│   ├── Workflow_in_Action.gif          # Animated workflow in action  
│   └── selecteur_parcelle.gif          # Demo of parcel configuration (data selector)  
│
├── files/                              # Fictive agronomic datasets and examples  
│   ├── analyses_sol.xlsx               # Soil analyses (texture, MO, CEC, pH, etc.)  
│   ├── configuration_parcelle.xlsx     # Hydric monitoring data (tension, dendrometer, phenological stage)  
│   ├── fertilisation.xlsx              # Nitrogen fertilization history (dates, doses, type)  
│   └── ChatBot_conversation.md         # Example of a conversational dialogue with the agent  
│
├── code/                               # Scripts and orchestration blueprints  
│   ├── Agent_IA_Agronomie_Final.md     # Full n8n multi-agent workflow blueprint  
│   └── datas.txt                       # Example JSON exchanged between workflows (API interoperability)  
```
---

👉 This project is a **showcase of agentic workflows applied to agronomy**: sovereign, modular, and directly usable for decision support.
