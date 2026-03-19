# Quick Start Guide - SessionLog Mod

## Building the Mod

### Windows
```bash
gradlew.bat build
```

### Mac/Linux
```bash
./gradlew build
```

The compiled JAR will be in: `build/libs/sessionlog-1.0.0.jar`

## Installation Steps

1. **Install Fabric Loader** (if not already installed)
   - Download from https://fabricmc.net/use/installer/
   - Run the installer and select your Minecraft version (1.21.1)

2. **Copy the mod JAR**
   ```
   Copy: build/libs/sessionlog-1.0.0.jar
   To: .minecraft/mods/
   ```

3. **Add your Session ID**
   - Launch Minecraft once (it will fail if your session isn't configured, that's OK)
   - Find the config file: `.minecraft/config/sessionlog/sessionlog.json`
   - Edit it with your session ID:

   ```json
   {
     "sessionId": "your-session-id-here",
     "usernameOverride": "YourUsername",
     "enabled": true
   }
   ```

4. **Restart Minecraft** - You should now be logged in!

## Getting Your Session ID

### Method 1: From launcher_profiles.json
1. Press `Win + R` and type `%APPDATA%`
2. Navigate to `.minecraft/launcher_profiles.json`
3. Open with a text editor
4. Find the "accessToken" field for your profile - this is your session ID

### Method 2: Using a Session Grabber Tool
- Search for "Minecraft session grabber" (use caution with third-party tools)

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Mod doesn't load | Ensure Fabric Loader is installed correctly |
| Config file not created | Launch game, then check `.minecraft/config/sessionlog/` |
| Session ID invalid | Verify the accessToken from launcher_profiles.json |
| Login fails | Session ID may have expired; get a new one |

## Notes

- ✅ Works in offline mode
- ✅ Uses session-based authentication
- ✅ Compatible with Fabric mods
- ⚠️ Keep your session ID private - it's like a password
