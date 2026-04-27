# SRT Tools

A multi-tool web application for working with subtitles, audio, and video. Built as a pnpm workspace monorepo with TypeScript.

## Features

- **SRT Note** — Multi-language subtitle editor with side-by-side language columns (Original, Arabic, German, etc.). Auto-saves locally, supports project organization, export, and trash.
- **Ai Audio** — Text-to-speech editor using free Microsoft Edge voices. Supports Bangla, English, and many other languages with chunked synthesis, playback queue, MP3 download, undo, and favorite voices.
- **Audio Splitter** — Split audio files into segments.
- **Video Splitter** — Split video files into segments.

## Tech Stack

- **Monorepo**: pnpm workspaces
- **Runtime**: Node.js 24
- **Language**: TypeScript 5.9
- **Frontend**: React + Vite + Tailwind CSS + shadcn/ui
- **Backend**: Express 5
- **Database**: PostgreSQL + Drizzle ORM
- **Validation**: Zod (`zod/v4`), `drizzle-zod`
- **API codegen**: Orval (from OpenAPI spec)
- **Build**: esbuild
- **TTS**: `msedge-tts` (free Microsoft Edge online voices)

## Project Structure

```
artifacts/
├── api-server/       # Express backend (TTS, etc.)
├── srt-tools/        # React frontend (main app)
└── mockup-sandbox/   # Component preview / design canvas
packages/
├── api-spec/         # OpenAPI spec + generated client hooks
└── db/               # Drizzle schema + migrations
```

## Getting Started

### Prerequisites
- Node.js 24+
- pnpm

### Install
```bash
pnpm install
```

### Run in development
Each artifact has its own dev workflow. To run them all:
```bash
pnpm --filter @workspace/api-server run dev
pnpm --filter @workspace/srt-tools run dev
```

### Build
```bash
pnpm run build
```

### Type-check
```bash
pnpm run typecheck
```

## Key Commands

| Command | Description |
|---------|-------------|
| `pnpm run typecheck` | Full typecheck across all packages |
| `pnpm run build` | Typecheck + build all packages |
| `pnpm --filter @workspace/api-spec run codegen` | Regenerate API hooks and Zod schemas from OpenAPI spec |
| `pnpm --filter @workspace/db run push` | Push DB schema changes (dev only) |
| `pnpm --filter @workspace/api-server run dev` | Run API server locally |

## API Endpoints

### `POST /api/tts`
Synthesizes MP3 audio from text using Microsoft Edge voices (free, no API key required).

**Body:**
```json
{
  "text": "Hello world",
  "voice": "en-US-AriaNeural"
}
```
- `voice` is optional. Auto-detects `bn-BD-NabanitaNeural` for Bangla text and `en-US-AriaNeural` for English when omitted.
- Max 5000 characters per request.

### `GET /api/tts/voices`
Returns the full list of available Edge voices (cached in memory).

## Deployment

This project is configured for Replit Deployments. Use the publish button in the Replit workspace to deploy.

## License

Private project.
