# Sports Tryout Video Review SaaS

A full-stack application for coaches to upload tryout videos, tag players at specific timestamps, and review player performance.

## Tech Stack

**Backend:**
- Node.js + Express
- SQLite + Drizzle ORM
- Multer for video uploads
- Local file storage

**Frontend:**
- React + React Router
- Vite
- Tailwind CSS
- react-player for video playback
- react-dropzone for uploads

## Quick Start

### Prerequisites
- Node.js 18+ installed
- npm or yarn

### Installation

1. Install all dependencies:
```bash
npm run install:all
```

2. Set up the database:
```bash
npm run db:push
```

3. Start the development servers:
```bash
npm run dev
```

This will start:
- Backend server on http://localhost:5001
- Frontend client on http://localhost:3000

## Project Structure

```
/client          - React frontend application
/server          - Express backend API
  /uploads       - Video file storage
  /src
    /db          - Database schema and connection
    /routes      - API endpoints
```

## Features

- **Roster Management**: Add, edit, and delete players
- **Video Upload**: Drag-and-drop video uploads with library view
- **Video Tagging**: Tag players at specific timestamps in videos
- **Review Mode**: Auto-play tagged clips for individual players
