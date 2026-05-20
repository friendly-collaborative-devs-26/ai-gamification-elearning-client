# Agent Instructions

You are an expert AI programming assistant assigned to the **AI Gamification Elearning Client**. 

## Tech Stack
- Framework: Vue 3 (Composition API, `<script setup>`)
- UI Library: [shadcn-vue](https://www.shadcn-vue.com/)
- Styling: Tailwind CSS
- Tooling: Vite, TypeScript, Pinia (for state management), Vue Router

## Architecture Rules
This project STRICTLY follows the **SCREAM Architecture**.

**CRITICAL INSTRUCTION**: Before generating any boilerplate, reading files, or proposing refactorings, you **MUST** read and understand `ARCHITECTURE.md`.

### Core Axioms
1. We organize by **Feature/Domain**, not by technical concern. Place files in `src/features/[domain]/` instead of global folders.
2. Use `src/shared/` ONLY for domain-agnostic generic UI (like shadcn components), layout structures, and core utils.
3. When creating new views, services, or stores, identify their business domain and place them in the corresponding feature's internal folders (`api`, `components`, `composables`, `stores`, `types`, `views`).

Ensure all generated code and refactoring naturally align with the repository structure.
