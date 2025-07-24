# 🤖 AI Foundry Agent Tutorials

Eine umfassende Sammlung von Tutorials, Beispielen und Best Practices für die Entwicklung von KI-Agenten mit Azure
🎯 Beispiel Anwendungsfälle

- **🛒 Intelligenter Kundenservice** - 24/7 Chatbots für Online-Shop und In-Store KiosksAI Foundry und anderen modernen Frameworks.

## 📋 Überblick

Dieses Repository enthält eine vielfältige Sammlung von Tutorials und Beispielen für die Entwicklung intelligenter Agenten, von grundlegenden Konzepten bis hin zu fortgeschrittenen Multi-Agent-Systemen und Produktionsbereitschaft.

## 🗂️ Repository-Struktur

### 🏗️ Grundlagen & Core Services

- **[Ai-agents-for-beginners/](./Ai-agents-for-beginners/)** - Microsoft's offizieller AI Agents Kurs
  - 11 Lektionen zu AI Agent Grundlagen
  - Agentic Design Patterns, Tool Use, Production
  - Multi-Language Support (Deutsch verfügbar)
  - MCP (Model Context Protocol) Integration

- **[Agent-Service/](./Agent-Service/)** - Azure AI Agent Service Tutorials
  - Einzelne Agenten, Multi-Agent-Systeme
  - File Search, Code Interpreter, Function Calling
  - Bing Integration, Custom Agents, Connected Agents
  - MCP Support, Deep Research Tools

- **[Ai-Foundry-handson-Playground/](./Ai-Foundry-handson-Playground/)** - Azure AI Foundry Playground
  - Hands-on Anleitung für die Azure AI Foundry UI
  - Agent Setup und Konfiguration im Playground
  - Schritt-für-Schritt Guides für UI-basierte Entwicklung
  - **Ideal für alle, die den visuellen Playground bevorzugen**

- **[Agents-and-MCP-handson/](./Agents-and-MCP-handson/)** - Model Context Protocol Hands-on
  - Praktische MCP (Model Context Protocol) Implementierung
  - Client-Server Architektur Beispiele
  - Web Search MCP Integration
  - Event-basierte Agent Workflows

- **[AI-Agents-foundamentals/](./AI-Agents-foundamentals/)** - Fundamentale Konzepte
  - Enterprise Knowledge Agents
  - Medical Diagnostic Agents
  - Automatisierte Evaluationen
  - Multi-Agent Tracing

### 🧠 Agentic Design Patterns

- **[Agent-innovator-lab/](./Agent-innovator-lab/)** - Innovationslabor für Agenten
  - **Basic Agents**: AutoGen, LangGraph, Semantic Kernel, Azure AI Agent
  - **Agentic Design Patterns**: Reflection, Plan-and-Execute, Multi-Agent
  - **Evaluation Patterns**: Human-in-the-Loop, Azure Evaluation SDK
  - **Optimization**: Streaming, Caching, Prompt Optimization, Memory Management

- **[Agentic-RAG/](./Agentic-RAG/)** - Retrieval Augmented Generation
  - Agentic Retrieval mit Azure AI Search
  - RAG-Pattern Implementierungen

### 🔒 Spezialisierte Anwendungen

- **[MultiAgent-CyberSecurity-Lab/](./MultiAgent-CyberSecurity-Lab/)** - Cybersecurity Agenten
  - Single Agent Implementierungen
  - Multi-Agent Orchestrierung
  - AutoGen Integration
  - Sicherheitsanalytik und -bewertung

- **[Dream-team-main/](./Dream-team-main/)** - Dream Team Multi-Agent-System
  - Frontend/Backend Architektur
  - Magentic One Integration
  - MCP (Model Context Protocol) Support
  - Azure Deployment mit Bicep

### ⚙️ Frameworks & Tools

- **[Semantic-Kernel-Agent-Orchestration/](./Semantic-Kernel-Agent-Orchestration/)** - Semantic Kernel
  - Concurrent Agents
  - Group Chat Orchestrierung
  - Sequential Processing
  - Azure Integration

- **[Voic-live-api/](./Voic-live-api/)** - Voice Integration
  - Live Voice API Integration
  - Quickstart Beispiele

## 🚀 Erste Schritte

### Voraussetzungen

- Python 3.8+
- Azure Subscription mit AI Foundry Zugang
- VS Code oder Jupyter Notebook Umgebung

### Installation

```bash
# Repository klonen
git clone https://github.com/LaetitiaMa1410/AI_Foundry_Agent_Tutorials.git
cd AI_Foundry_Agent_Tutorials

# Je nach Projekt spezifische Requirements installieren
pip install -r <project-folder>/requirements.txt
```

### Konfiguration

1. Azure AI Foundry Setup
2. Umgebungsvariablen konfigurieren (siehe .env.sample Dateien)
3. API Keys und Endpoints einrichten

**💡 Tipp**: Wenn du die visuelle Entwicklung bevorzugst, starte mit `Ai-Foundry-handson-Playground/` - dort findest du Anleitungen für die Azure AI Foundry UI anstatt Code-basierter Entwicklung.

## 📚 Lernpfade

### 🔰 Beginner Track

1. **Absoluter Start** → `Ai-agents-for-beginners/` 
2. **UI-basiert (Playground)** → `Ai-Foundry-handson-Playground/` (Für Aigent Entwicklung im Playground ohne Code)
3. **Grundlagen** → `AI-Agents-foundamentals/01-enterprise-knowledge-agent.ipynb`
4. **Erste Schritte** → `Agent-innovator-lab/0_basic-agent/`
5. **Simple RAG** → `Agentic-RAG/`

### 🔥 Intermediate Track

1. **Design Patterns** → `Agent-innovator-lab/1_agentic-design-ptn/`
2. **MCP Hands-on** → `Agents-and-MCP-handson/` (Model Context Protocol)
3. **Multi-Agent** → `Agent-Service/2 Azure AI Agent service - Many agents.ipynb`
4. **Function Calling** → `Agent-Service/5 Azure AI Agent service - Function calling.ipynb`

### 🚀 Advanced Track

1. **Production Systems** → `Dream-team-main/`
2. **Cybersecurity** → `MultiAgent-CyberSecurity-Lab/`
3. **Evaluation & Optimization** → `Agent-innovator-lab/2_eval-design-ptn/`

## 🛠️ Technologie-Stack

- **Azure AI Foundry** - Core AI Platform (Code + UI Playground)
- **AutoGen** - Multi-Agent Framework
- **LangGraph** - Graph-based Agent Orchestration
- **Semantic Kernel** - Microsoft's AI SDK
- **Azure AI Search** - Vector Search & RAG
- **Bing Search API** - Web Integration
- **MCP (Model Context Protocol)** - Standardisierte Tool Integration

## 📊 Verwendete Frameworks im Vergleich

| Framework | Best für | Komplexität | Azure Integration |
|-----------|----------|-------------|-------------------|
| AutoGen | Multi-Agent Konversationen | Mittel | ⭐⭐⭐ |
| LangGraph | Graph-basierte Workflows | Hoch | ⭐⭐ |
| Semantic Kernel | .NET/C# Integration | Niedrig | ⭐⭐⭐⭐⭐ |
| Azure AI Agent | Managed Service | Niedrig | ⭐⭐⭐⭐⭐ |

## 🎯 Beispiel Anwendungsfälle 

- **� Intelligenter Kundenservice** - 24/7 Chatbots für Online-Shop und In-Store Kiosks
- **�📊 Inventory & Demand Analytics** - Bestandsoptimierung basierend auf Verkaufsdaten und Trends
- **🎯 Personalisierte Produktempfehlungen** - KI-gestützte Cross-Selling und Upselling Strategien
- **📱 Omnichannel Customer Journey** - Nahtlose Erfahrung zwischen Online-Shop und Filiale
- **� Intelligente Produktsuche** - Semantische Suche mit Bild- und Texterkennung
- **💰 Dynamic Pricing** - Echtzeitpreisanpassungen basierend auf Markt und Konkurrenz
- **� Supply Chain Optimization** - Automatisierte Bestellungen und Lieferkettenmanagement
- **👥 Customer Insights & Segmentierung** - Verhaltensanalyse für zielgerichtetes Marketing


