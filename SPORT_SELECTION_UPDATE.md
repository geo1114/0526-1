# Sport Selection Feature - Implementation Summary

## Overview
The app is now sport-agnostic! Users can select a sport when uploading videos, and the UI dynamically adapts based on the sport selected (positions for roster, action types for tagging).

## Database Changes

### New `sports` Table
- **id**: Primary key
- **name**: Sport name (e.g., "Basketball", "Volleyball")
- **positions**: JSON array of position names
- **actionTypes**: JSON array of action type names
- **createdAt**: Timestamp

### Updated `videos` Table
- Added **sportId**: Foreign key reference to sports table

### Default Sports Data
Two sports are pre-seeded in the database:

**Basketball:**
- Positions: Guard, Forward, Center
- Action Types: Shot, Assist, Rebound, Block, Steal, Turnover

**Volleyball:**
- Positions: Libero, Setter, Outside Hitter, Middle Blocker, Opposite
- Action Types: Serve, Attack, Block, Dig, Set, Ace

## Backend Changes

### New API Endpoint
- **GET /api/sports** - Returns all sports with positions and action types
- **GET /api/sports/:id** - Returns a specific sport

### Updated Endpoints
- **POST /api/videos** - Now requires `sportId` in the request body

### Migration Script
- `server/src/migrate.ts` - Handles database migration, including:
  - Creating sports table
  - Seeding default sports (Basketball & Volleyball)
  - Migrating existing videos to add sportId (defaults to Basketball)
  - Preserving existing data during migration

## Frontend Changes

### 1. Upload Page (`client/src/pages/Upload.tsx`)
**Added:**
- Sport selector dropdown before video upload area
- Default sport is pre-selected (Basketball)
- Sport badge displayed on each video card in the library
- Validation to ensure a sport is selected before upload

**Usage:**
1. Select a sport from the dropdown
2. Upload video (drag-drop or click to browse)
3. Video is associated with the selected sport

### 2. Tag Page (`client/src/pages/Tag.tsx`)
**Added:**
- Dynamic action type buttons based on video's sport
- Loads sport data when video is loaded
- Action type buttons replace the text input field
- Clear button to deselect action type

**Usage:**
1. Select a player
2. Click on action type buttons (e.g., "Shot", "Assist" for Basketball)
3. Optionally add notes
4. Tag at current timestamp

### 3. Review Page (`client/src/pages/Review.tsx`)
**Added:**
- Action type filter dropdown above video player
- Shows count of clips for each action type
- Filters clips dynamically based on selected action
- Resets to "All Actions" when changing players

**Usage:**
1. Select a player
2. Use filter dropdown to view only specific actions (e.g., only "Shots")
3. Navigate through filtered clips

### 4. Roster Page (No Changes)
- Positions are still free text input
- Future enhancement: Could add sport-specific position dropdowns

## API Client Updates

### New Interface
```typescript
interface Sport {
  id: number;
  name: string;
  positions: string[];
  actionTypes: string[];
  createdAt: Date;
}
```

### Updated Video Interface
```typescript
interface Video {
  id: number;
  filename: string;
  originalName: string;
  sportId: number;  // NEW
  uploadedAt: Date;
}
```

### New API Methods
```typescript
sportsApi.getAll()  // Get all sports
sportsApi.getById(id)  // Get sport by ID
```

### Updated Methods
```typescript
videosApi.upload(file, sportId)  // Now requires sportId
```

## Running the Application

### Fresh Install
```bash
npm run install:all
npm run db:push
npm run dev
```

### Existing Installation
The migration script handles updating existing databases automatically:
```bash
npm run db:push  # Updates schema and seeds sports
npm run dev
```

## Testing the Features

1. **Upload with Sport Selection:**
   - Go to Upload page
   - Select "Basketball" or "Volleyball"
   - Upload a video
   - Verify sport badge appears on video card

2. **Tagging with Action Types:**
   - Click "Tag Players" on a Basketball video
   - Verify action buttons show: Shot, Assist, Rebound, Block, Steal, Turnover
   - Click "Tag Players" on a Volleyball video
   - Verify action buttons show: Serve, Attack, Block, Dig, Set, Ace

3. **Review with Filters:**
   - Go to Review page
   - Select a player with multiple tagged clips
   - Use action filter dropdown
   - Verify clips are filtered correctly

## Future Enhancements

1. **Add More Sports:** Easily add new sports via the database
2. **Admin UI:** Create sports management interface
3. **Position Validation:** Make roster positions sport-specific dropdowns
4. **Custom Actions:** Allow users to add custom action types per sport
5. **Sport Icons:** Add visual icons for each sport
6. **Multi-Sport Analysis:** Compare player performance across different sports

## Database Commands

```bash
npm run db:push    # Run migration (creates tables + seeds sports)
npm run db:seed    # Only seed sports data (if already migrated)
npm run db:reset   # Run migration + seed in one command
```

## API Testing

```bash
# Get all sports
curl http://localhost:5001/api/sports

# Get specific sport
curl http://localhost:5001/api/sports/1

# Upload video with sport
curl -X POST http://localhost:5001/api/videos \
  -F "video=@video.mp4" \
  -F "sportId=1"
```

## Notes

- Existing videos are automatically migrated to Basketball (sportId=1)
- Tags without action types still work (action type is optional)
- The migration preserves all existing player and tag data
- SQLite JSON handling uses TEXT fields with JSON.parse/stringify
