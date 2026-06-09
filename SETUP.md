# Setup Instructions

Follow these steps to get the Sports Tryout Video Review SaaS application running on your machine.

## Prerequisites

- Node.js 18 or higher
- npm (comes with Node.js)

## Installation Steps

### 1. Install All Dependencies

From the root directory, run:

```bash
npm run install:all
```

This will install dependencies for:
- Root project (concurrently for running both servers)
- Server (Express, Drizzle ORM, SQLite, etc.)
- Client (React, Vite, Tailwind, etc.)

### 2. Set Up the Database

Navigate to the server directory and push the database schema:

```bash
cd server
npm run db:push
```

This creates the SQLite database file (`database.db`) with all necessary tables:
- `players` - Stores player roster information
- `videos` - Stores video metadata and file references
- `tags` - Stores player tags at specific video timestamps

### 3. Start the Development Servers

Return to the root directory and start both servers:

```bash
cd ..
npm run dev
```

This will start:
- **Backend API** on http://localhost:5001
- **Frontend App** on http://localhost:3000

## Verify Installation

1. Open your browser and navigate to http://localhost:3000
2. You should see the Sports Tryout Video Review application
3. Start by adding players in the Roster page
4. Upload a video in the Upload page
5. Tag players in videos using the Tag page
6. Review tagged clips in the Review page

## Folder Structure

```
/SaaS
├── client/              # React frontend
│   ├── src/
│   │   ├── api/        # API client
│   │   ├── components/ # Reusable components
│   │   ├── pages/      # Page components
│   │   └── App.tsx     # Main app with routing
│   └── package.json
├── server/              # Express backend
│   ├── src/
│   │   ├── db/         # Database schema and connection
│   │   ├── routes/     # API endpoints
│   │   └── index.ts    # Server entry point
│   ├── uploads/        # Video file storage
│   └── package.json
└── package.json         # Root scripts
```

## Troubleshooting

### Port Already in Use

If you get an error that port 3000 or 5001 is already in use:

1. Find and kill the process using the port:
   ```bash
   # macOS/Linux
   lsof -ti:3000 | xargs kill -9
   lsof -ti:5001 | xargs kill -9
   ```

2. Or change the ports in:
   - Server: `server/.env` (PORT variable, default: 5001)
   - Client: `client/vite.config.ts` (server.port, default: 3000)
   - Client API: `client/src/api/client.ts` (API_BASE_URL)

Note: Port 5000 is often used by macOS AirPlay Receiver, so we use 5001 by default.

### Database Issues

If you encounter database errors:

1. Delete the database file:
   ```bash
   rm server/database.db
   ```

2. Re-run the database push:
   ```bash
   cd server && npm run db:push
   ```

### Module Not Found Errors

If you get TypeScript or module errors:

1. Ensure all dependencies are installed:
   ```bash
   npm run install:all
   ```

2. Try clearing caches:
   ```bash
   cd client && rm -rf node_modules && npm install
   cd ../server && rm -rf node_modules && npm install
   ```

## Additional Commands

- `npm run dev:server` - Run only the backend server
- `npm run dev:client` - Run only the frontend client
- `npm run db:studio` - Open Drizzle Studio to view/edit database (requires Drizzle Kit)

## Next Steps

1. Add players to your roster
2. Upload tryout videos
3. Tag players at key moments
4. Review player performance clips

Enjoy using the Sports Tryout Video Review application!
