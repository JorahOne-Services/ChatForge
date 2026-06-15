# 💬 LLM Chat Application Template

[![Cloudflare Workers](https://img.shields.io/badge/Cloudflare-Workers-F38020?logo=cloudflare)](https://workers.cloudflare.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript)](https://www.typescriptlang.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Maintained by OneByJorah](https://img.shields.io/badge/Maintained%20by-OneByJorah-1E90FF?logo=github)](https://github.com/OneByJorah)

---

## 📋 Overview

**LLM Chat Application Template** is a simple, ready-to-deploy chat application powered by Cloudflare Workers AI. Features real-time streaming responses, a clean responsive UI, and easy customization — perfect as a starting point for AI chat applications.

> **Maintained by [OneByJorah](https://github.com/OneByJorah)**

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 💬 **Chat Interface** | Clean, responsive UI for AI conversations |
| ⚡ **Streaming Responses** | Real-time streaming via Server-Sent Events (SSE) |
| 🧠 **Workers AI** | Powered by Cloudflare's LLM platform |
| 📱 **Mobile-Friendly** | Responsive design for all screen sizes |
| 🔄 **Chat History** | Maintains conversation history client-side |
| 🔍 **Observability** | Built-in logging and monitoring |
| 🛠️ **TypeScript** | Full TypeScript support for type safety |

---

## 📁 Project Structure

```
llm-chat-app-template/
├── public/                     # Static assets
│   ├── index.html             # Chat UI HTML
│   └── chat.js                # Chat UI frontend script
├── src/
│   ├── index.ts               # Main Worker entry point
│   └── types.ts               # TypeScript type definitions
├── test/                      # Test files
├── wrangler.jsonc             # Cloudflare Worker configuration
├── tsconfig.json              # TypeScript configuration
├── package.json               # Node.js dependencies
└── README.md                  # This documentation
```

---

## 📋 Prerequisites

| Requirement | Details |
|-------------|---------|
| **Node.js** | v18 or newer |
| **Wrangler CLI** | [Installation guide](https://developers.cloudflare.com/workers/wrangler/install-and-update/) |
| **Cloudflare** | Account with Workers AI access |

---

## ⚡ Quick Start

### 1. Clone & Install

```bash
git clone https://github.com/OneByJorah/llm-chat-app-template.git
cd llm-chat-app-template
npm install
```

### 2. Generate Type Definitions

```bash
npm run cf-typegen
```

### 3. Start Development Server

```bash
npm run dev
```

The app will be available at `http://localhost:8787`

### 4. Deploy to Cloudflare

```bash
npm run deploy
```

### 5. Monitor Logs

```bash
npm wrangler tail
```

---

## 🔧 Customization

### Changing the Model

Update the `MODEL_ID` constant in `src/index.ts`:

```typescript
const MODEL_ID = "@cf/meta/llama-3.1-8b-instruct";
```

See [available models](https://developers.cloudflare.com/workers-ai/models/) in the Cloudflare docs.

### AI Gateway Integration

The template includes commented code for AI Gateway integration:

1. [Create an AI Gateway](https://dash.cloudflare.com/?to=/:account/ai/ai-gateway) in your Cloudflare dashboard
2. Uncomment the gateway configuration in `src/index.ts`
3. Replace `YOUR_GATEWAY_ID` with your actual gateway ID

### System Prompt

Modify the `SYSTEM_PROMPT` constant in `src/index.ts` to change the AI's behavior.

### Styling

Edit the CSS variables in `public/index.html` to customize the color scheme:

```css
:root {
  --primary: #6366f1;
  --bg: #0f172a;
  --surface: #1e293b;
}
```

---

## 🏗️ How It Works

### Backend

1. **API Endpoint** (`/api/chat`): Accepts POST requests with chat messages
2. **Streaming**: Uses Server-Sent Events (SSE) for real-time response streaming
3. **Workers AI Binding**: Connects to Cloudflare's AI service via Workers AI binding

### Frontend

1. Presents a clean chat interface
2. Sends user messages to the API endpoint
3. Processes streaming responses in real-time
4. Maintains chat history on the client side

---

## 🐛 Troubleshooting

| Problem | Solution |
|---------|----------|
| Worker won't deploy | Check `wrangler.jsonc` configuration |
| AI not responding | Verify Workers AI is enabled in your Cloudflare account |
| Type errors | Run `npm run cf-typegen` to regenerate types |
| Local dev issues | Ensure Node.js v18+ is installed |

---

## 🔄 Updates

```bash
cd /path/to/llm-chat-app-template
git pull origin main
npm install
npm run deploy
```

---

## 📚 Resources

- [Cloudflare Workers Documentation](https://developers.cloudflare.com/workers/)
- [Cloudflare Workers AI Documentation](https://developers.cloudflare.com/workers-ai/)
- [Workers AI Models](https://developers.cloudflare.com/workers-ai/models/)
- [AI Gateway Documentation](https://developers.cloudflare.com/ai-gateway/)

---

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

MIT License — free to use, modify, and distribute.

---

## 📞 Support

For issues or questions, please open an issue on GitHub:

https://github.com/OneByJorah/llm-chat-app-template/issues

---

**Made with ❤️ by [OneByJorah](https://github.com/OneByJorah)**
