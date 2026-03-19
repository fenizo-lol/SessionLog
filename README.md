# SessionLog - Minecraft Session ID Login Mod

A Fabric mod for Minecraft 1.21.1 that allows you to login using a session ID from a configuration file.

## Features

- ✅ Login using session ID only (no password needed)
- ✅ Config file based setup
- ✅ Alternative login method (works alongside standard authentication)
- ✅ Easy configuration

## Installation

### Prerequisites
- Minecraft 1.21.1
- Fabric Loader
- Fabric API

### Setup

1. **Build the mod:**
   ```bash
   ./gradlew build
   ```
   The compiled JAR will be in `build/libs/sessionlog-1.0.0.jar`

2. **Install to Minecraft:**
   - Place the JAR in your `.minecraft/mods` folder
   - Ensure Fabric Loader is installed

3. **Configure Session ID:**
   - Launch Minecraft once with the mod installed
   - Navigate to `.minecraft/config/sessionlog/sessionlog.json`
   - Edit the file with the following format:

   ```json
   {
     "sessionId": "your-minecraft-session-id-here",
     "usernameOverride": "YourUsername",
     "enabled": true
   }
   ```

4. **Restart Minecraft** - The mod will automatically authenticate using your session ID

## Configuration

Edit `.minecraft/config/sessionlog/sessionlog.json`:

| Field | Type | Description |
|-------|------|-------------|
| `sessionId` | String | Your Minecraft session ID (obtain via launcher debug or from another client) |
| `usernameOverride` | String | The username to appear as in-game |
| `enabled` | Boolean | Set to `true` to enable session ID login |

## How to Get Your Session ID

### Option 1: Extract from Launcher (Windows)
1. Find your launcher's session file
2. Look in `%APPDATA%/.minecraft/launcher_profiles.json`
3. Find the `accessToken` field - this is your session ID

### Option 2: From Another Client
Use a tool to capture the session ID from your existing Minecraft installation.

## Security Notes

⚠️ **Warning:** Session IDs are sensitive credentials. Keep your `sessionlog.json` file secure and never share it.

## Building from Source

```bash
./gradlew build
```

Output: `build/libs/sessionlog-1.0.0.jar`

## License

MIT License - See LICENSE file for details

## Troubleshooting

- **Config not found**: The mod creates `config/sessionlog/sessionlog.json` on first run
- **Login fails**: Verify your session ID is valid and hasn't expired
- **Mod not loading**: Ensure Fabric Loader and Fabric API are installed
