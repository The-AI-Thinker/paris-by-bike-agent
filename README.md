# 🚴‍♀️ Paris by Bike

An intelligent, interactive assistant designed to help users explore Paris by bicycle – combining real-time information, contextual understanding, and document-based knowledge retrieval.

![Paris by Bike Screenshot](docs/images/home_interface.png)

---

## 🌍 Overview

**Paris by Bike** is a conversational AI assistant built to demonstrate how modern AI systems can integrate *retrieval-augmented generation (RAG)* with intelligent *agent tools*. The application allows users to:

* Retrieve relevant information from local documents (e.g., guides or manuals)
* Plan bike routes and visualize them using Google Maps
* Access live weather forecasts to optimize trip planning
* Perform contextual reasoning to decide when to search, calculate, or respond directly

Through these features, the project showcases the potential of a multi-capability assistant that unifies local knowledge retrieval and external API interactions in a single conversational interface.

---

## 🎯 Features

* 🧭 **RAG-Powered Document Search** – Answers context-based questions from local files using FAISS vector indexing.
* 🌤️ **Weather Forecasts** – Integrates with the OpenWeatherMap API to provide current and hourly forecasts.
* 🧮 **Biking Time & Distance Calculator** – Estimates travel time or distance based on the user's available duration.
* 🔎 **Web Search Tool** – Uses Tavily to find up-to-date events, shops, or bike meetups in Paris.
* 🗺️ **Google Maps Route Generator** – Creates cycling routes between landmarks or neighborhoods.
* 💬 **Conversational Context Memory** – Keeps track of recent exchanges for a natural, human-like flow.
* 💻 **User Interface via Chainlit** – Offers an interactive chat-based interface for testing and exploration.

---

## 🧠 Architecture

The system follows a modular design:

```
project_root/
│
├── app.py              # Chainlit interface and chat orchestration
├── agent_logic.py      # Definition of tools, LLM setup, and agent rules
├── rag_pipeline.py     # Retrieval-Augmented Generation pipeline
├── chainlit.md         # Onboarding text for the UI
├── requirements.txt    # Key dependencies
└── data/               # Local knowledge base (guides, PDFs, markdown files)
```

### Core Components

1. **RAG Pipeline** (`rag_pipeline.py`)

   * Loads and indexes local text/PDF/Markdown files using FAISS.
   * Splits documents with `RecursiveCharacterTextSplitter`.
   * Generates answers using a local or cloud-hosted LLM (e.g., Llama3 or Groq).

2. **Agent Tools** (`agent_logic.py`)

   * Defines structured tools for weather, web search, route generation, and calculations.
   * Uses LangChain's tool framework to enable autonomous reasoning and tool selection.

3. **Chat Interface** (`app.py`)

   * Handles multi-turn conversation and memory management.
   * Displays intermediate reasoning and tool execution steps.

---

## 🧩 Technology Stack

| Component    | Technology                                                                                       |
| ------------ | ------------------------------------------------------------------------------------------------ |
| Interface    | [Chainlit](https://www.chainlit.io/)                                                             |
| Framework    | [LangChain](https://www.langchain.com/) & [LangGraph](https://github.com/langchain-ai/langgraph) |
| Vector Store | FAISS                                                                                            |
| LLMs         | Groq Cloud or Ollama (Llama3 local model)                                                        |
| Tools        | Tavily Search, OpenWeatherMap API                                                                |
| Language     | Python 3.10+                                                                                     |

---

## ⚙️ Installation

1. **Clone the repository:**

   ```bash
   git clone https://github.com/AFA-Teaching/paris-by-bike-agent.git
   cd paris-by-bike
   ```

2. **Install dependencies:**

   ```bash
   pip install -r requirements.txt
   ```

3. **Add environment variables:**
   Create a `.env` file in the project root with your API keys:

   ```bash
   GROQ_API_KEY=your_groq_api_key
   OPENWEATHERMAP_API_KEY=your_openweather_key
   TAVILY_API_KEY=your_tavily_key
   ```

4. **Add your local data:**
   Place `.pdf`, `.md`, or `.txt` files inside the `data/` folder for RAG indexing.

5. **Run the app:**

   ```bash
   chainlit run app.py -w
   ```

6. **Open the interface:**
   Visit [http://localhost:8000](http://localhost:8000) in your browser.

---

## 🧭 Usage Examples

Try interacting with the assistant by asking:

* *"What's a good scenic route for beginners in Paris?"*
* *"Plan a 1-hour bike ride from the 17th arrondissement."*
* *"What's the weather like this afternoon?"*
* *"Find upcoming cycling events near the Seine."*

The agent will decide whether to answer directly, use the RAG pipeline, or call a tool.

---

## 🧰 Future Improvements

* Add persistent memory and user preferences
* Support multi-language interaction (English/French)
* Enhance UI with route visualization (e.g., Folium or Mapbox)
* Containerize the project with Docker for deployment