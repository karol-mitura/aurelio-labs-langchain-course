# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Structure

This is a LangChain-based AI agent application with a FastAPI backend and Next.js frontend that demonstrates streaming agent responses.

### Core Components

- **`/api`** - Python FastAPI backend with streaming agent executor
  - `main.py` - FastAPI server with streaming endpoints and CORS setup
  - `agent.py` - Custom agent executor using LangChain with async tools (SerpAPI search, math operations)
  - Uses OpenAI GPT-4o-mini with tool binding and streaming callbacks
  
- **`/app`** - Next.js 15 frontend with TypeScript and Tailwind CSS
  - `src/app/page.tsx` - Main chat interface
  - `src/components/` - React components for markdown rendering, text input, and output display
  - Uses Turbopack for development builds

### Key Architecture Patterns

- **Streaming Architecture**: Custom `QueueCallbackHandler` manages real-time token streaming from LangChain to frontend
- **Agent Loop**: `CustomAgentExecutor` iteratively invokes tools until reaching `final_answer` tool
- **Tool System**: Async tools including SerpAPI web search and math operations with structured output
- **Message Protocol**: Custom streaming protocol with step markers (`<step>`, `</step>`, `<<STEP_END>>`)

## Development Commands

### API Server
```bash
cd api
uv run uvicorn main:app --reload
```
- API docs available at `http://localhost:8000/docs`
- Test streaming with `streaming-test.ipynb` notebook

### Frontend App
```bash
cd app
npm install
npm run dev          # Development server with Turbopack
npm run build        # Production build
npm run start        # Production server
npm run lint         # Next.js linting
```
- App runs at `http://localhost:3000`

## Environment Setup

Requires `.env` file in project root with:
- `OPENAI_API_KEY` - OpenAI API key for LLM
- `SERPAPI_API_KEY` - SerpAPI key for web search functionality

## Testing

- Use `streaming-test.ipynb` to test API streaming functionality
- Use `serapi-tool.ipynb` for SerpAPI tool testing