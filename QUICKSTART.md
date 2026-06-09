# Quick Start Guide

## Your Application is Running! 🎉

Both servers are now live:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:5001

## What You Can Do Now

### 1. Open the Application
Visit http://localhost:3000 in your browser to see the app.

### 2. Try the Features

**Step 1: Add Players**
- Click on "Roster" in the navigation
- Add some players with their jersey numbers and positions
- Examples:
  - Name: "John Smith", Jersey: "23", Position: "Forward"
  - Name: "Jane Doe", Jersey: "10", Position: "Midfielder"

**Step 2: Upload a Video**
- Click on "Upload" in the navigation
- Drag and drop a video file (or click to browse)
- Supported formats: MP4, MOV, AVI, WMV, FLV, MKV
- Max file size: 500MB

**Step 3: Tag Players in Videos**
- After uploading, click "Tag Players" on any video
- The video will play in the main area
- Select a player from the sidebar
- Optionally add an action type (e.g., "pass", "shot", "tackle")
- Optionally add notes (e.g., "Great footwork")
- Click "Tag at [timestamp]" to mark the player at the current time
- Tags appear in the list below the video - click any tag to jump to that moment

**Step 4: Review Player Clips**
- Click on "Review" in the navigation
- Select any player from the sidebar
- The video player will show all their tagged moments
- Use "Next Clip" / "Previous Clip" to navigate through their highlights
- See all clips in a grid view below the player

## File Locations

- **Videos**: Stored in `/server/uploads/`
- **Database**: SQLite file at `/server/database.db`
- **Logs**: Check terminal for server logs

## Stopping the Servers

Press `Ctrl+C` in the terminal to stop both servers.

## Restarting Later

Just run from the root directory:
```bash
npm run dev
```

## API Endpoints (for testing)

The backend API is available at http://localhost:5001/api

- `GET /api/players` - List all players
- `POST /api/players` - Create a player
- `GET /api/videos` - List all videos
- `POST /api/videos` - Upload a video (multipart/form-data)
- `GET /api/tags` - List all tags
- `POST /api/tags` - Create a tag

### Example API Test:
```bash
# Add a player
curl -X POST http://localhost:5001/api/players \
  -H "Content-Type: application/json" \
  -d '{"name":"Test Player","jerseyNumber":"99","position":"Forward"}'

# Get all players
curl http://localhost:5001/api/players
```

## Next Steps

1. **Add Authentication**: Implement user login/signup if needed
2. **Cloud Storage**: Replace local file storage with AWS S3 or similar
3. **PostgreSQL**: Migrate from SQLite to PostgreSQL for production
4. **Video Processing**: Add video compression/optimization
5. **Export Features**: Add ability to export player highlight reels
6. **Search & Filter**: Add search functionality for players and videos
7. **Analytics**: Track player performance metrics over time

## Need Help?

Check the detailed documentation:
- [README.md](./README.md) - Project overview
- [SETUP.md](./SETUP.md) - Detailed setup and troubleshooting

Enjoy your Sports Tryout Video Review application! 🏆
