# SessionLog Mod - Project Structure & Developer Guide

## Project Layout

```
SessionLog/
├── build.gradle              # Gradle build configuration
├── gradle.properties         # Gradle version properties
├── settings.gradle           # Gradle settings
├── gradlew                   # Unix/Linux build script
├── gradlew.bat              # Windows build script
├── README.md                # Main documentation
├── QUICKSTART.md            # Quick start guide
├── LICENSE                  # MIT License
├── .gitignore              # Git ignore rules
│
├── config/                  # Example config directory
│   └── sessionlog.json      # Example session config file
│
├── src/main/java/com/sessionlog/
│   ├── SessionLogMod.java                    # Main mod class
│   ├── client/
│   │   ├── SessionLogClient.java             # Client initializer
│   │   └── SessionIdAuthenticator.java       # Session authentication logic
│   ├── config/
│   │   └── ConfigManager.java                # Configuration file handling
│   └── mixin/
│       └── MinecraftMixin.java               # Mixin hook for Minecraft
│
└── src/main/resources/
    ├── fabric.mod.json                       # Fabric mod metadata
    ├── sessionlog.mixins.json                # Mixin configuration
    └── assets/sessionlog/
        └── textures/                         # Texture assets (for future GUI)
```

## File Descriptions

### Core Configuration Files

| File | Purpose |
|------|---------|
| `build.gradle` | Maven/Gradle build configuration for Fabric |
| `gradle.properties` | Version numbers and project metadata |
| `fabric.mod.json` | Fabric mod loader metadata |
| `sessionlog.mixins.json` | Mixin hook definitions |

### Java Source Files

| File | Purpose |
|------|---------|
| `SessionLogMod.java` | Entry point, logger initialization |
| `SessionLogClient.java` | Client-side initialization hook |
| `SessionIdAuthenticator.java` | Handles session ID authentication logic |
| `ConfigManager.java` | Manages JSON config file I/O |
| `MinecraftMixin.java` | Mixin hooks into Minecraft client |

### Configuration

| File | Purpose |
|------|---------|
| `config/sessionlog.json` | Example config with session ID, username, enabled flag |

## How It Works

1. **Mod Initialization**
   - Fabric loads `SessionLogMod` on startup
   - `SessionLogClient` is called for client-side setup

2. **Configuration Loading**
   - `ConfigManager.init()` reads from `config/sessionlog/sessionlog.json`
   - Creates file with defaults if it doesn't exist

3. **Authentication**
   - `SessionIdAuthenticator.attemptSessionIdLogin()` runs on client startup
   - Reads session ID from config
   - Creates a `User` object with the session credentials
   - Injects the user into Minecraft's client via reflection

4. **Session Management**
   - User remains logged in as long as session ID is valid
   - Restart Minecraft to apply config changes

## Building & Deployment

### Development Build
```bash
./gradlew clean build
```

### Output
- JAR: `build/libs/sessionlog-1.0.0.jar`
- Sources: `build/libs/sessionlog-1.0.0-sources.jar`

### Installation
1. Install Fabric Loader for 1.21.1
2. Copy JAR to `.minecraft/mods/`
3. Configure `config/sessionlog/sessionlog.json`

## Key Classes Explained

### ConfigManager
Handles persistent configuration storage/retrieval:
- Reads/writes JSON config file
- Manages enabled state
- Stores session ID and username

### SessionIdAuthenticator  
Core authentication logic:
- Creates `User` object from session ID
- Uses reflection to inject user into Minecraft client
- Handles authentication failures gracefully

### SessionLogClient
Fabric client initializer:
- Runs on game client startup
- Triggers config loading and authentication
- Provides entry point for client-side code

## Extending the Mod

### Adding GUI Login Screen
1. Create a custom screen extending `Screen`
2. Add to client init in `SessionLogClient.java`
3. Call `SessionIdAuthenticator.setSessionAndLogin()`

### Adding Commands
1. Implement Fabric API commands
2. Register in `SessionLogClient.java`
3. Examples: `/sessionlog set <id>`, `/sessionlog info`

### Adding Multiplayer Support
1. Extend `SessionIdAuthenticator` for server validation
2. Use mixins to intercept `MultiplayerScreen` 
3. Inject session credentials in server handshake

## Dependencies

- **Minecraft**: 1.21.1
- **Fabric Loader**: 0.16.9+
- **Fabric API**: 0.102.1+
- **Java**: 21+

## Logging

The mod uses SLF4J for logging:
```
[SessionLog] - Main messages
Check logs/debug.log for detailed output
```

## Security Considerations

⚠️ **Important**:
- Session IDs are sensitive credentials
- Never commit `config/sessionlog/sessionlog.json` to version control
- Keep session IDs secure and isolated
- Consider encrypting config file for production use

## Version Compatibility

Currently supports Minecraft 1.21.1. To update to a new version:

1. Update `minecraft_version` in `gradle.properties`
2. Update `fabric_version` to compatible release
3. Rebuild: `./gradlew clean build`
4. Test thoroughly before distribution
