🤖 Odyssey AI Chatbot

Odyssey is an AI mentor chatbot that helps students and beginner developers understand programming and tech concepts. It explains ideas clearly and concisely, remembers the conversation, and streams replies token by token in a clean web chat interface.

🔗 Live demo: [odyssey-chatbot on Streamlit](https://odyssey-chatbot-mwtw8xnxwg52pt8mrwsd73.streamlit.app/)
---

## ✨ Features

- **Live streaming responses** – tokens appear as they are generated, no waiting for the full reply
- **Conversation memory** – previous turns are passed back to the model so follow-up questions work
- **Fast inference** – powered by Groq's high-speed LPU inference
- **Clean chat UI** – built with Streamlit's native chat components
- **Secure key handling** – supports a local `.env` file and Streamlit Cloud Secrets
- **Composable LangChain pipeline** – prompt → model → parser using LCEL

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|------------|
| UI | [Streamlit](https://streamlit.io/) |
| Orchestration | [LangChain](https://www.langchain.com/) (LCEL) |
| LLM provider | [Groq](https://groq.com/) via `langchain-groq` |
| Model | `openai/gpt-oss-20b` |
| Config | `python-dotenv` |

---

## 🧠 How It Works

The app is split into two layers:

1. **AI brain (LangChain)** – a `ChatPromptTemplate` combines a system instruction, a `chat_history` placeholder and the user's question. This is piped into `ChatGroq` and a `StrOutputParser`:

   ```
   prompt_template | model | parser
   ```

2. **Presentation layer (Streamlit)** – `st.session_state` stores the conversation as `HumanMessage` / `AIMessage` objects, past turns are re-rendered on every rerun, and `st.write_stream` displays the streamed response live.

---

## 📁 Project Structure

```
Odyssey-Chatbot/
├── app.py             # Streamlit web app (main entry point)
├── main.py            # Command-line version of the chatbot
├── requirements.txt   # Python dependencies
├── .gitignore
└── README.md
```

> `main.py` also keeps earlier commented-out versions of the bot (single call → looped chat → manual memory), showing how it evolved into the LangChain version.

---

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- A free [Groq API key](https://console.groq.com/keys)

### 1. Clone the repository

```bash
git clone https://github.com/src-geek07/Odyssey-Chatbot.git
cd Odyssey-Chatbot
```

### 2. (Optional) Create a virtual environment

```bash
python -m venv venv
source venv/bin/activate      # macOS / Linux
venv\Scripts\activate         # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Add your API key

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key_here
```

### 5. Run the app

**Web app (Streamlit):**

```bash
streamlit run app.py
```

**Terminal version:**

```bash
python main.py
```

Type `quit` or `exit` to leave the terminal chat.

---

## ☁️ Deploying on Streamlit Community Cloud

1. Push the repo to GitHub.
2. Create a new app on [Streamlit Community Cloud](https://streamlit.io/cloud) and point it to `app.py`.
3. Open **Settings → Secrets** and add:

   ```toml
   GROQ_API_KEY = "your_groq_api_key_here"
   ```

4. Deploy.

---

## ⚙️ Configuration

You can tweak the bot in `app.py`:

| Setting | Where | Default |
|---------|-------|---------|
| Model | `ChatGroq(model=...)` | `openai/gpt-oss-20b` |
| Creativity | `temperature` | `0.7` |
| Max response length | `max_tokens` | `1024` |
| Personality | system message in `prompt_template` | "Inspiring AI mentor that explains concepts clearly and concisely" |

---

## 🔐 Security Notes

- Never commit your `.env` file or API key. Keep `.env` listed in `.gitignore`.
- On Streamlit Cloud, always use **Secrets** instead of hard-coding keys.

---

## 🗺️ Possible Improvements

- Persistent chat history across sessions
- Model / temperature selector in the sidebar
- "Clear chat" button
- File or document Q&A (RAG)

---

## 🤝 Contributing

Suggestions and pull requests are welcome. Fork the repo, create a branch, and open a PR.

---

## 🙌 Acknowledgements

Built during the **CSI Bootcamp**, using [Streamlit](https://streamlit.io/), [LangChain](https://www.langchain.com/) and [Groq](https://groq.com/).
