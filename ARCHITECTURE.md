## 🏗️ Architecture

The frontend follows a **SCREAM Architecture** (Screaming Architecture), adapted for modern UI frameworks. The guiding principle is that looking at the project structure should instantly communicate **what the application does** (the business domains), rather than the frameworks or technical tools it uses.

Notice how the top-level folders inside `src/features/` yell "User", "Course", "Challenge" — not "Views", "Store", "Controllers".

---

## 📁 Full project structure

```
ai-gamification-elearning-client/
├── public/                      # Static assets not processed by Vite
├── src/                         
│   ├── app/                     # [APP LAYER] Application setup. Bootstraps the app, wires providers.
│   │   ├── main.ts              # Entry point. Initializes Vue, Pinia, Router.
│   │   ├── router/              # Global route definitions combining feature routes.
│   │   └── styles/              # Global CSS, Tailwind layers, theme variables.
│   │
│   ├── shared/                  # [SHARED LAYER] Global cross-cutting UI and utilities.
│   │   │                        # Rule: code here must be domain-agnostic. No business logic.
│   │   │
│   │   ├── components/ui/       # Base UI components (e.g., shadcn-vue buttons, inputs, modals).
│   │   ├── layouts/             # Application layouts (MainLayout, AuthLayout).
│   │   ├── lib/                 # Core utilities (fetch client, formatting, dates).
│   │   ├── stores/              # Global generic state (e.g., theme store, auth session).
│   │   └── types/               # Generic TS types / interfaces.
│   │
│   ├── features/                # [FEATURE LAYER] The core of SCREAM Architecture.
│   │   │                        # Organized strictly by business domain. 
│   │   │
│   │   ├── auth/                # Everything related to Authentication
│   │   ├── users/               # Everything related to User profiles, stats, settings
│   │   ├── courses/             # Everything related to Course browsing, enrollment
│   │   └── challenges/          # Everything related to solving coding challenges
│   │       ├── api/             # Feature-specific API calls (e.g., submitChallenge)
│   │       ├── components/      # UI components used only in this feature (e.g., CodeEditor)
│   │       ├── composables/     # Feature-specific Vue composables (e.g., useChallengeTimer)
│   │       ├── stores/          # Feature-specific Pinia state
│   │       ├── types/           # TS definitions purely for this domain
│   │       └── views/           # Page-level components for this feature (e.g., ChallengeDetail.vue)
│   │
│   ├── App.vue                  # Root Vue component
│   └── vite-env.d.ts            # Vite related types
│
├── tailwind.config.js           # Tailwind & shadcn configuration
├── components.json              # shadcn-vue CLI registry config
├── package.json                 # Dependencies and scripts
└── vite.config.ts               # Vite configuration
```

---
 
## 🔵 Features layer
 
**Location:** `src/features/`
 
The core of our SCREAM architecture. If a developer wants to change how a Challenge is submitted, they go straight to `src/features/challenges/`. They do not need to hunt across a separate global `views/`, `stores/`, or `api/` directory.

### Rules of a Feature:
1. **High Cohesion:** A feature must contain everything it needs to function (its own API calls, types, localized state, specific components).
2. **Encapsulation:** Features should not deeply import from other features' internal folders. If they must communicate, it should be through public boundaries or global state.
3. **Domain Naming:** Folders are named after the business entity (`courses`, `challenges`), not technical roles.

```ts
// SAMPLE: src/features/challenges/api/submit-challenge.ts
import { apiClient } from '@/shared/lib/api-client'
import type { SubmissionResult } from '../types'

export async function submitChallenge(challengeId: string, code: string): Promise<SubmissionResult> {
  const { data } = await apiClient.post(`/challenges/${challengeId}/submit`, { code })
  return data
}
```

```vue
<!-- SAMPLE: src/features/challenges/components/CodeEditor.vue -->
<script setup lang="ts">
import { ref } from 'vue'
import { Button } from '@/shared/components/ui/button'

const content = ref('')
const emit = defineEmits(['run-code'])
</script>

<template>
  <div class="code-editor-wrapper">
    <textarea v-model="content"></textarea>
    <Button @click="emit('run-code', content)">Run</Button>
  </div>
</template>
```
 
---
 
## 🟢 Shared layer
 
**Location:** `src/shared/`
 
Contains generic, reusable parts of the application. It acts as the "Standard Library" for our frontend. 
 
### Rules of the Shared Layer:
1. **Domain-Agnostic:** Code in `shared/` must never know about specific features. `Button.vue` shouldn't know about a "Course".
2. **Shadcn-vue:** All generated `shadcn` components live in `src/shared/components/ui/`.
3. **Global Layouts:** `Navbar`, `Sidebar`, and structural layouts go into `src/shared/layouts/`.

```vue
<!-- SAMPLE: src/shared/layouts/MainLayout.vue -->
<script setup lang="ts">
import { Navbar } from '@/shared/components/layout/Navbar.vue'
</script>

<template>
  <div class="min-h-screen bg-background font-sans antialiased">
    <Navbar />
    <main class="container mx-auto py-6">
       <!-- Feature Views are injected here -->
      <RouterView /> 
    </main>
  </div>
</template>
```
 
---
 
## 🟡 App layer
 
**Location:** `src/app/`
 
Handles the highest-level orchestration such as initializing Vue plugins, routing, and global stylesheets.

### Rules of the App Layer:
1. **No Business Logic:** Only configuration and bootstrapping.
2. **Global Assembly:** The router imports Views from the feature layer and stitches them into defined URLs.

```ts
// SAMPLE: src/app/router/index.ts
import { createRouter, createWebHistory } from 'vue-router'
import MainLayout from '@/shared/layouts/MainLayout.vue'

// Import feature view
import ChallengeDetail from '@/features/challenges/views/ChallengeDetail.vue'

export const router = createRouter({
  history: createWebHistory(),
  routes: [
    {
      path: '/',
      component: MainLayout,
      children: [
        {
          path: 'challenges/:id',
          name: 'challenge-detail',
          component: ChallengeDetail
        }
      ]
    }
  ]
})
```