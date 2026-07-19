<div align="center">

  <img src="https://raw.githubusercontent.com/OneByJorah/ChatForge/main/docs/logo.png" alt="ChatForge Logo" width="120">

  # 🔥 ChatForge

  **AI-Powered Chat Interface & Conversation Management Platform**

  Build, deploy, and manage intelligent chatbots with multi-model support and enterprise features

  [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
  [![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
  [![Cloudflare Workers](https://img.shields.io/badge/Cloudflare_Workers-000?style=flat&logo=cloudflare&logoColor=white)](https://workers.cloudflare.com/)
  [![Workers AI](https://img.shields.io/badge/Workers_AI-F6821F?style=flat&logo=cloudflare&logoColor=white)](https://developers.cloudflare.com/workers-ai/)

  [Features](#-features) • [Quick Start](#-quick-start) • [Architecture](#-architecture) • [API](#-api-reference) • [Contributing](#-contributing)

</div>

---

## 📸 Screenshots

> Captured from `wrangler dev` serving the real `public/index.html` UI.

<div align="center">

![Chat Interface](docs/screenshots/chat-ui.png)

</div>

> 💡 **Tip:** ChatForge streams assistant replies in real time via Server-Sent Events (SSE).

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🤖 **Workers AI Chat** | Powered by Cloudflare Workers AI (`@cf/meta/llama-3.1-8b-instruct-fp8`) |
| 💬 **Real-Time Streaming** | Assistant replies stream token-by-token via Server-Sent Events (SSE) |
| 🔒 **Security Headers** | HSTS, X-Frame-Options, nosniff, referrer-policy, permissions-policy |
| 📦 **Zero-Server Ops** | Runs entirely on Cloudflare Workers + static assets (no VM to manage) |

> This is a focused Cloudflare Workers template. It does **not** include JWT auth, multi-model provider switching, conversation persistence, theming, analytics, or a plugin system — those are not in the code.

---

## 🚀 Quick Start

### Prerequisites

- [Node.js 18+](https://nodejs.org/) and npm
- A Cloudflare account (free tier works) with Workers AI enabled
- `CLOUDFLARE_API_TOKEN` with Workers deploy permissions (for `wrangler dev`/`deploy`)

### Local Development

```bash
git clone https://github.com/OneByJorah/ChatForge.git
cd ChatForge
npm install
npm run dev          # wrangler dev — serves the UI + /api/chat locally
```

Open **http://localhost:8787** in your browser.

> Deploy: `npx wrangler deploy` (publishes the Worker + assets to your Cloudflare account).

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `CLOUDFLARE_API_TOKEN` | — | Token with Workers deploy rights (for `wrangler dev`/`deploy`) |
| `MODEL_ID` | `@cf/meta/llama-3.1-8b-instruct-fp8` | Workers AI model (set in `src/index.ts`) |

> Configuration lives in `wrangler.jsonc` (the `ai` binding) and `src/index.ts` — there is no `.env`/database for this template. |

---

## 🏗️ Architecture

```
Browser ──HTTP/SSE──▶ Cloudflare Worker (src/index.ts)
                        ├── GET  /            → static UI (public/index.html)
                        └── POST /api/chat    → Workers AI (@cf/meta/llama-3.1-8b-instruct-fp8)
                                              → streams reply via Server-Sent Events
```

No database, no auth layer, no separate backend process — everything runs on Cloudflare's Workers runtime.

### Tech Stack

| Component | Technology |
|-----------|------------|
| **Runtime** | Cloudflare Workers |
| **Language** | TypeScript |
| **AI** | Cloudflare Workers AI (`@cf/meta/llama-3.1-8b-instruct-fp8`) |
| **UI** | Static HTML/CSS/JS (`public/`) |
| **Tooling** | Wrangler, Vitest (worker pool) |

---

## 📁 Project Structure

```
ChatForge/
├── src/
│   ├── index.ts             # Worker entry (fetch handler, /api/chat SSE)
│   ├── types.ts             # ChatMessage / Env types
│   └── __tests__/index.test.ts
├── public/
│   ├── index.html           # Chat UI
│   └── chat.js              # Frontend logic
├── docs/                    # Architecture / API docs
├── wrangler.jsonc           # Worker config (AI binding, assets)
├── package.json
└── tsconfig.json
```

---

## 🔌 API Reference

### Chat

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/api/chat` | `POST` | Body `{"messages": [...]}` → streams the assistant reply as SSE (`data: {...}` chunks) |

No authentication, conversation persistence, or model-listing endpoints exist in this template.

### Example Usage

```bash
# Stream a chat reply (SSE)
curl -N -X POST http://localhost:8787/api/chat \
  -H "Content-Type: application/json" \
  -d '{"messages": [{"role": "user", "content": "Hello!"}]}'
```

---

## 🛠️ Development

```bash
git clone https://github.com/OneByJorah/ChatForge.git
cd ChatForge
npm install

npm run dev        # wrangler dev (UI + /api/chat on :8787)
npm run typecheck  # tsc --noEmit
npm test           # vitest (worker integration tests)
```

Deploy to Cloudflare: `npx wrangler deploy`.

---

## 🤝 Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🔒 Security

For security concerns, please see [SECURITY.md](SECURITY.md).

---

## 💬 Support

- 📧 Email: support@jorah.one
- 🐛 Issues: [GitHub Issues](https://github.com/OneByJorah/ChatForge/issues)
- 📖 Docs: [Documentation](docs/)

---

<div align="center">

  **Built with ❤️ by [Jhonattan L. Jimenez](https://github.com/OneByJorah)**

  [⬆ Back to Top](#-chatforge)

</div>
