# 🐷 AI Gamification Elearning-Client — Frontend

> Open source frontend for the **AI Gamification Elearning Server** e-learning platform: a gamified, AI-powered environment to learn web and backend development.

---

## 📖 About the project

**AI Gamification Elearning-Client** is an open source, gamified e-learning platform designed to teach software development in a practical and engaging way. The platform's initial focus is **web and backend development**, with a roadmap to expand into mobile development and artificial intelligence.

The platform is built around two core ideas:

- **Learning by doing** — students write real code, solve real challenges, and progress through levels as they build skills.
- **AI-powered feedback** — an integrated AI code reviewer analyses the student's submissions and provides contextual, constructive feedback in real time, acting as a always-available mentor.

This repository is the **Vue 3 frontend** of the platform. It consumes the REST API exposed by the backend and provides an interactive, gamified interface for students, utilizing `shadcn-vue` and Tailwind CSS for rapid and consistent UI development.

This project is **free to use and open to contributions**. See the [license](#license) section for details.

---

## 🗺️ Roadmap highlights

| Phase | Scope |
|---|---|
| v1 | Web & backend development tracks UI |
| v2 | AI code reviewer chat & feedback interface |
| v3 | Mobile-responsive design improvements |
| v4 | AI / ML development track UI features |

---

## ⚙️ Tech stack

| Concern | Technology |
|---|---|
| Framework | Vue 3 (Composition API) |
| UI Library | [shadcn-vue](https://www.shadcn-vue.com/) |
| Styling | Tailwind CSS |
| Build Tool | Vite |
| State Management| Pinia |
| Routing | Vue Router |
| API Client | Axios / Fetch API |
| Language | TypeScript |

---

## 🚀 Getting started

```bash
# Clone the repository
git clone https://github.com/your-org/ai-gamification-elearning-client.git
cd ai-gamification-elearning-client

# Install dependencies
pnpm install

# Copy and configure environment
cp .env.sample .env

# Run the development server
pnpm run dev
```

---

## 🤝 Contributing

AI Gamification Elearning Client is an open source project and contributions are welcome. Please open an issue before submitting a pull request so we can discuss the proposed change first.

When contributing, make sure your code respects the **SCREAM architecture** principles described in `ARCHITECTURE.md`. A PR that scatters feature-specific logic across generic global folders instead of isolating it inside its feature module will not be merged.

---

## 📄 License

This project is released under the [MIT License](LICENSE). You are free to use, modify, and distribute it.
