<div align="center">
  <h1>SENSIREN</h1>
  <p><strong>A sensual and renovating split companion</strong></p>
  <p>Dual-persona AI: Sen (caring therapeutic companion with voice & 3D) + Ren (research lab & study tools)</p>
</div>

## Overview

SenSiRen is a Next.js application featuring two complementary AI personas that share a diary:

- **Sen**: Warm, therapeutic, and optionally flirty companion. Supports neural TTS (Gemini), browser speech, 3D character customization, mood tracking, and voice interaction.
- **Ren**: Analytical research workspace with deep research mode, study tools (summarize, flashcards, quiz, simplify), themes, dictation, and structured Markdown outputs.

Both use Google Gemini with search grounding and maintain shared context via a local diary.

## Features

- Split / full Sen / full Ren layout modes
- Shared diary with context passing between personas
- Voice input (dictation) and output (TTS)
- 3D character for Sen with wardrobe, motion, and distortion controls
- Ren study tools and customizable technical level / verbosity
- Offline indicator
- PWA support (manifest + service worker)
- Responsive glassmorphism UI

## Prerequisites

- Node.js 18+
- A Google Gemini API key ([Get one here](https://aistudio.google.com/apikey))

## Local Setup

1. Clone the repository:
   ```bash
   git clone https://github.com/anonrighteousruler-art/SenSiRen.git
   cd SenSiRen
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create environment file:
   ```bash
   cp .env.example .env.local
   ```

4. Edit `.env.local` and set your API key:
   ```
   NEXT_PUBLIC_GEMINI_API_KEY=your_actual_gemini_api_key_here
   ```

   > **Note:** The key must be prefixed with `NEXT_PUBLIC_` because the app runs as a static client-side export and makes Gemini calls from the browser.

5. Run the development server:
   ```bash
   npm run dev
   ```

6. Open [http://localhost:3000](http://localhost:3000)

## Build for Production

```bash
 npm run build
```

This generates a static export in the `out/` directory (due to `output: 'export'` in next.config.ts).

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `NEXT_PUBLIC_GEMINI_API_KEY` | Yes | Gemini API key for AI responses and neural TTS |
| `APP_URL` | No | Base URL (mainly for AI Studio deployments) |

## Project Structure

```
components/
  sen-side.tsx      # Sen companion (voice, 3D, persona)
  ren-side.tsx      # Ren research lab
  sen-character.tsx # 3D orb character (Three.js)
  sensiren-app.tsx  # Main layout & navigation
  diary-panel.tsx   # Shared diary UI
hooks/
  use-diary.ts      # Local diary storage & context
  use-speech.ts     # Dictation + TTS helpers
app/
  page.tsx          # Entry point
```

## Notes

- API calls happen client-side. Be mindful of exposing your key in production deployments.
- Neural TTS uses `gemini-2.5-flash-preview-tts`.
- Text generation uses `gemini-2.0-flash` with Google Search grounding.
- Diary is stored in browser localStorage.

## License

MIT (or as per original AI Studio export — feel free to add a LICENSE file).
