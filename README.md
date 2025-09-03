## Murf_ai

## 🤖 About The Project

This project is a hands-on guide to building a voice-based conversational AI using modern web technologies and powerful AI APIs. You can engage in a continuous, voice-to-voice conversation with an AI powered by Google's Gemini LLM. The agent remembers the context of your conversation, allowing for natural follow-up questions and a more human-like interaction.

The repository is structured by day, with each folder representing a significant step in the development process, from setting up the server to implementing a full conversational loop with memory and deploying it to the cloud.

### Key Features

  * **Voice-to-Voice Interaction**: Speak to the agent and receive a spoken response, creating a seamless conversational experience.
  * **Contextual Conversations**: The agent maintains a chat history for each session, enabling it to understand the flow of dialogue and respond to follow-up questions intelligently.
  * **End-to-End AI Pipeline**: It seamlessly integrates multiple AI services for a complete Speech-to-Text → Large Language Model → Text-to-Speech pipeline.
  * **Modern & Intuitive UI**: A clean, user-friendly interface with a single-button control and visual feedback for different states (e.g., ready, recording, thinking).
  * **Robust Error Handling**: Includes a fallback audio response for graceful failure when an API call is unsuccessful, ensuring a smooth user experience.


-----

## 🛠️ Tech Stack

The application is built using a combination of Python for the backend, vanilla JavaScript for the frontend, and a suite of powerful AI APIs for the core functionalities.

  * **Backend**:
      * **FastAPI**: For building the high-performance, asynchronous API server.
      * **Uvicorn**: As the ASGI server to run the FastAPI application.
      * **Python-Dotenv**: To manage environment variables securely.
      * **WebSockets**: For real-time, bidirectional communication between the client and server.
  * **Frontend**:
      * **HTML, CSS, JavaScript**: For the structure, styling, and client-side logic.
      * **Bootstrap**: For creating a responsive and modern user interface.
      * **MediaRecorder API & WebSocket API**: To capture and stream audio directly from the user's microphone in the browser.
  * **AI & Voice APIs**:
      * **Murf AI**: For generating high-quality, natural-sounding Text-to-Speech (TTS), including streaming capabilities.
      * **AssemblyAI**: For providing fast and accurate real-time Speech-to-Text (STT) transcription with turn detection.
      * **Google Gemini**: As the Large Language Model (LLM) for generating intelligent and coherent responses, with streaming and function calling.
      * **SerpAPI**: For real-time Google Search results, giving the agent access to current information.
 
-----

## ⚙️ Architecture

The application follows a client-server architecture. The frontend, running in the user's browser, is responsible for capturing audio and managing the user interface. The FastAPI backend acts as the orchestrator, managing the complex interactions between the various AI services.

Here is the flow for a single turn in a conversation:

1.  The **Client** captures the user's voice using the MediaRecorder API and sends the audio data to the backend.
2.  The **FastAPI Server** receives the audio file.
3.  It first sends the audio to **AssemblyAI** to be transcribed into text (STT).
4.  The server retrieves the chat history for the current session and appends the new transcript. This entire context is then sent to the **Google Gemini LLM**.
5.  Gemini processes the conversation and generates a text response, which is sent back to the server.
6.  The server adds the LLM's response to the chat history and forwards the text to **Murf AI** for speech synthesis (TTS).
7.  The server receives the final audio URL from Murf AI and sends it back to the client.
8.  The **Client** automatically plays the received audio, and the UI updates to indicate it's ready for the user's next turn.

-----

## 🚀 Getting Started

### Try the Live Agent

Our voice agent is now live\! You can access and interact with it here:

**[https://marvis-voice-agent-l7da.onrender.com/](https://marvis-voice-agent-l7da.onrender.com/)**

Simply visit the link, click the settings icon to enter your API keys, grant microphone permissions, and start chatting\!

### Running the App Locally

To get a local copy up and running, follow these simple steps.

#### Prerequisites

  * Python 3.8+
  * API keys for:
      * Murf AI
      * AssemblyAI
      * Google Gemini
      * SerpAPI

#### Installation

1.  **Clone the repository**
    ```sh
    git clone https://github.com/siddbhatt18/30-days-of-voice-agents.git
    ```
2.  **Install the required dependencies** from the `requirements.txt` file.
    ```sh
    pip install -r requirements.txt
    ```
3.  **Create a `.env` file** in the chosen day's directory. Copy the contents of `.env.example` (if available) or create it from scratch.
    ```
    MURF_API_KEY="your_murf_api_key_here"
    ASSEMBLYAI_API_KEY="your_assemblyai_api_key_here"
    GEMINI_API_KEY="your_gemini_api_key_here"
    SERP_API_KEY="your_serp_api_key_here"
    ```
4.  **Run the FastAPI server** with hot-reloading.
    ```sh
    uvicorn main:app --reload
    ```
5.  **Open your browser** and navigate to `http://localhost:8000`. Grant microphone permissions when prompted and start conversing\!

-----

## 📂 Project Structure

The project structure is optimized for deployment.

```
AI Voice Agent/
├── main.py      # Handles WebSocket connections and API key logic
├── services/
│   ├── llm.py   # Handles interactions with the Gemini LLM
│   ├── stt.py   # Manages real-time speech-to-text
│   └── tts.py   # Manages text-to-speech conversion
├── schemas.py
├── templates/
│   └── index.html # Main UI for the voice agent
├── static/
│   ├── script.js  # Frontend logic for recording and settings
│   └── style.css  # UI styles
├── requirements.txt # Lists all project dependencies for deployment
└── .env           # Stores API keys for local development
```


