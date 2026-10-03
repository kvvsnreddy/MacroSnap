# 🥗 MacroSnap

A Streamlit chat app where you enter your name and WhatsApp number once, then
chat with an AI nutrition buddy - type a question or attach a photo of your
meal - and get an instant calorie/macro estimate. One button sends a full
summary of the conversation to your WhatsApp.

Built with **Gemini** (chat + vision) and **Twilio** (WhatsApp). No OpenCV,
no MediaPipe, no model training.

## Features
- One-time onboarding (name + WhatsApp number)
- Chat by text or by attaching a meal photo (jpg / jpeg / png)
- Persistent conversation memory, so follow-ups like "how much protein was that?" work
- System prompt keeps the bot strictly on food, nutrition and fitness
- "Send to WhatsApp" button texts you a combined summary of every meal

## Project structure
```
macrosnap/
├── app.py                         # the app
├── prompts.py                     # the AI's personality
├── requirements.txt
├── .gitignore
└── .streamlit/secrets.toml.example
```

## Run locally
1. Python 3.9+ required.
2. Create and activate a virtual environment
   - `python -m venv venv`
   - macOS/Linux: `source venv/bin/activate`
   - Windows PowerShell: `.\venv\Scripts\Activate.ps1`
3. `pip install -r requirements.txt`
4. Copy `.streamlit/secrets.toml.example` to `.streamlit/secrets.toml` and fill in:
   - `GEMINI_API_KEY` from [Google AI Studio](https://aistudio.google.com)
   - `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN` from the Twilio Console
   - `TWILIO_WHATSAPP_FROM` (sandbox default is already filled in)
   - `TWILIO_CONTENT_SID` from Twilio's Content Template Builder
     (template text: `Hi {{1}}, here's your MacroSnap summary:\n\n{{2}}`)
5. From your WhatsApp, send the sandbox join message (e.g. `join happy-tiger`)
   to the Twilio sandbox number. This expires after ~72 hours of inactivity.
6. `streamlit run app.py` and open http://localhost:8501

## Deploy (Streamlit Community Cloud)
1. Push to GitHub (never commit `.streamlit/secrets.toml`).
2. On [share.streamlit.io](https://share.streamlit.io), click **New app**, pick the repo and `app.py`.
3. Paste your secrets into **Settings → Secrets**.
4. Deploy.
