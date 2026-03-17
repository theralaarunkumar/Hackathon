# CortexFlow AI – Multi-Agent Work Operating System

## Overview

Full-stack AI productivity app that transforms unstructured information (meeting notes, project updates, documents) into structured workflows using AI agents powered by Google Gemini.

## Stack

- **Monorepo tool**: pnpm workspaces
- **Node.js version**: 24
- **Package manager**: pnpm
- **TypeScript version**: 5.9
- **Frontend**: React + Vite + TailwindCSS + Zustand (state)
- **Backend**: Express 5
- **AI**: Google Gemini 2.5 Flash (via Replit AI Integrations)
- **Validation**: Zod (via generated OpenAPI schemas)
- **API codegen**: Orval (from OpenAPI spec)

## Structure

```text
artifacts-monorepo/
├── artifacts/
│   ├── cortexflow/         # React + Vite frontend (served at /)
│   └── api-server/         # Express API server (served at /api)
├── lib/
│   ├── api-spec/           # OpenAPI spec + Orval codegen config
│   ├── api-client-react/   # Generated React Query hooks
│   ├── api-zod/            # Generated Zod schemas from OpenAPI
│   ├── db/                 # Drizzle ORM schema + DB connection
│   └── integrations-gemini-ai/  # Gemini AI client + utilities
└── scripts/                # Utility scripts
```

## Pages

1. **Landing Page** (`/`) — Hero with "Start Workspace" CTA
2. **Workspace Page** (`/workspace`) — Textarea to paste notes, triggers AI analysis
3. **AI Insights Page** (`/insights`) — Shows summary, key insights, extracted tasks with priority
4. **Workflow Visualization** (`/workflow`) — Vertical workflow steps with arrows
5. **Dashboard** (`/dashboard`) — Today's tasks, AI recommendations, workflow progress

## API Endpoints

- `GET /api/healthz` — Health check
- `POST /api/analyze` — Analyze text through 4 AI agents
  - Input: `{ text: string }`
  - Output: `{ summary, insights, tasks, workflowSteps, nextBestAction, priorityRecommendation }`

## AI Agents (run via single Gemini prompt)

1. **Analysis Agent** — Generates summary and insights
2. **Task Extraction Agent** — Extracts tasks with priorities
3. **Workflow Planning Agent** — Creates sequential workflow steps
4. **Productivity Agent** — Recommends next best action and priority

## Environment Variables

- `AI_INTEGRATIONS_GEMINI_BASE_URL` — Auto-set by Replit AI Integrations
- `AI_INTEGRATIONS_GEMINI_API_KEY` — Auto-set by Replit AI Integrations
- `PORT` — Set automatically per service

## Running

- Frontend: `pnpm --filter @workspace/cortexflow run dev`
- Backend: `pnpm --filter @workspace/api-server run dev`
- Codegen: `pnpm --filter @workspace/api-spec run codegen`
