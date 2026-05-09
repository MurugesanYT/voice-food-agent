# 🎙️ VoiceOrder — AI-Powered Food Ordering Agent

> Talk to order. No tapping. No scrolling. Just speak.

**VoiceOrder** is a hands-free food ordering agent powered by **NVIDIA Nemotron 3** — a native live conversation model via NVIDIA NIM — and the **Swiggy MCP API**. Users simply speak what they want — Nemotron 3 listens, understands, responds in natural speech, and places the order on Swiggy on their behalf. No separate STT or TTS services needed.

---

## 🧠 How It Works

```
User speaks → Web Speech API (mic capture) → Nemotron 3 (live conversation) → Swiggy MCP API → Order Placed → Nemotron 3 speaks back
```

1. **Voice Input** — Captured via browser mic using the **Web Speech API**
2. **Live Conversation (Nemotron 3)** — NVIDIA's native live conversation model handles everything in one place:
   - Listens and understands user speech in real-time
   - Parses intent ("I want biryani from a good place nearby")
   - Manages multi-turn conversation (clarifying restaurant, quantity, address)
   - Calls Swiggy MCP tools to search, select, and order
   - Responds back in **natural spoken voice natively** — no TTS service needed
3. **Swiggy MCP API** — Used to:
   - Search nearby restaurants
   - Browse menus
   - Add items to cart
   - Place and track orders

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────┐
│                     User Interface                       │
│         (Web / Mobile — mic input + audio output)        │
└────────────────────────┬────────────────────────────────┘
                         │ mic audio (Web Speech API)
                         ▼
┌─────────────────────────────────────────────────────────┐
│         NVIDIA NIM — Nemotron 3                          │
│         Native Live Conversation Model                   │
│                                                          │
│   • Listens & understands speech in real-time            │
│   • Parses user intent                                   │
│   • Manages conversation state                           │
│   • Calls Swiggy MCP tools                              │
│   • Responds in natural spoken voice natively            │
│   (No separate STT or TTS needed)                        │
└────────────────────────┬────────────────────────────────┘
                         │ MCP tool calls
                         ▼
┌─────────────────────────────────────────────────────────┐
│                  Swiggy MCP Server                       │
│                                                          │
│   Tools used:                                            │
│   • search_restaurants(location, query)                  │
│   • get_menu(restaurant_id)                              │
│   • add_to_cart(item_id, quantity)                       │
│   • place_order(cart_id, address)                        │
│   • track_order(order_id)                                │
└─────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Live Voice Agent | [NVIDIA Nemotron 3](https://build.nvidia.com) — native live conversation model via NVIDIA NIM |
| Mic Capture | Browser-native [Web Speech API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Speech_API) |
| Food Ordering API | Swiggy MCP API (Food) |
| Backend | Python (FastAPI) |
| Frontend | React + Web Speech API |
| Auth | OAuth 2.0 (Swiggy redirect flow) |

---

## 🗣️ Example Conversation

```
User:    "Order me some chicken biryani"

Agent:   "Sure! I found 3 restaurants near you with chicken biryani.
          Paradise Biryani — ₹320, Behrouz Biryani — ₹480,
          or Bawarchi — ₹280. Which one do you prefer?"

User:    "Go with Paradise"

Agent:   "Got it — 1 Chicken Dum Biryani from Paradise Biryani for ₹320.
          Delivering to your saved address on Anna Salai. Shall I place the order?"

User:    "Yes, go ahead"

Agent:   "Order placed! Your biryani will arrive in about 35 minutes.
          Order ID: SWG-8821934. Anything else?"
```

---

## 📁 Project Structure

```
voice-food-agent/
├── backend/
│   ├── main.py               # FastAPI server
│   ├── agent.py              # Nemotron 3 live conversation agent
│   └── swiggy_tools.py       # Swiggy MCP tool definitions
├── frontend/
│   ├── src/
│   │   ├── App.jsx
│   │   ├── VoiceCapture.jsx  # Mic input component
│   │   └── AgentChat.jsx     # Conversation UI
│   └── package.json
├── .env.example
├── requirements.txt
└── README.md
```

---

## ⚙️ Environment Variables

```env
# NVIDIA NIM
NVIDIA_API_KEY=your_nvidia_nim_api_key

# Swiggy MCP
SWIGGY_CLIENT_ID=your_swiggy_client_id
SWIGGY_CLIENT_SECRET=your_swiggy_client_secret
SWIGGY_REDIRECT_URI=http://localhost:3000/auth/callback
```

---

## 🚀 Getting Started

```bash
# 1. Clone the repo
git clone https://github.com/yourusername/voice-food-agent
cd voice-food-agent

# 2. Install backend dependencies
pip install -r requirements.txt

# 3. Set up environment variables
cp .env.example .env
# Edit .env with your keys

# 4. Start the backend
uvicorn backend.main:app --reload

# 5. Start the frontend
cd frontend && npm install && npm run dev
```

---

## 📌 Current Status

> 🚧 Project is in the **planning phase**. Development will begin once Swiggy MCP API access is granted.

- [ ] Swiggy MCP API access — applied via Builders Club
- [ ] NVIDIA NIM account setup & Nemotron API key
- [ ] Backend scaffolding (FastAPI)
- [ ] Nemotron agent integration
- [ ] Swiggy MCP tool wrappers
- [ ] Frontend voice UI with Web Speech API
- [ ] End-to-end order flow testing

---

## 🔮 Roadmap

- **v1.0** — Order food via voice, single user, web app
- **v1.1** — Saved preferences ("my usual order")
- **v1.2** — WhatsApp / Telegram bot interface
- **v1.3** — Multi-language support (Tamil, Hindi, Telugu)
- **v2.0** — Swiggy Instamart grocery orders via voice

---

## 📄 License

MIT License — see [LICENSE](./LICENSE)

---

> Built with ❤️ using NVIDIA Nemotron + Swiggy MCP API
