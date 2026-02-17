# 🤖 Livestream Robot Cohost

A Windows desktop application for livestream automation with an interactive robot cohost. Designed for TradingView chart rotation with text-to-speech script reading.

## Features

- **12 Tab Configuration**: Set up 12 TradingView chart URLs with corresponding scripts
- **Automatic Tab Rotation**: Rotates through tabs every 45 seconds (configurable)
- **3D Robot Character**: Wall-E inspired robot with smooth animations
- **Text-to-Speech**: Reads scripts aloud with customizable voice settings
- **SuperChat Simulation**: Manually trigger tab + script reading (simulates YouTube SuperChat)
- **OBS Ready**: Clean, dark-themed UI optimized for streaming capture
- **Control Panel**: Separate window for managing the stream

## Installation

### Prerequisites
- Node.js 18+ and npm
- Windows 10/11 (for executable build)

### Setup

1. Clone or download this repository
2. Install dependencies:
```bash
cd livestream_robot_cohost
npm install
```

3. Run in development mode:
```bash
npm start
```

### Building for Windows

To create a Windows executable:
```bash
npm run build
```

The executable will be created in the `dist` folder.

## Usage Guide

### Setup Window

1. **Launch the app** - The setup window opens first
2. **Enter TradingView URLs** - Paste your chart URLs in the Tab 1-12 fields
3. **Add Scripts** - Write or paste the scripts the robot will read for each chart
4. **Configure Settings**:
   - **Rotation Interval**: How long each tab displays (default: 45 seconds)
   - **Speech Rate**: How fast the robot speaks (0.5x - 2x)
   - **Volume**: Audio volume level
5. **Save Configuration** - Click to persist your settings
6. **Start Stream View** - Launch the main streaming window

### Main Stream View

- **Tab Indicator** (top-right): Shows current tab number and countdown timer
- **Mini Controls** (bottom-right, hover to show):
  - ⏸️ Pause/Resume rotation
  - 🎛️ Open control panel
  - ⚙️ Back to setup
  - 🛑 Emergency stop

### Triggering the Robot (SuperChat Simulation)

**Method 1: Keyboard Shortcuts**
- `Ctrl+1` through `Ctrl+9` → Trigger Tabs 1-9
- `Ctrl+0` → Trigger Tab 10
- `Ctrl+-` → Trigger Tab 11
- `Ctrl+=` → Trigger Tab 12
- `Ctrl+Escape` → Emergency stop

**Method 2: Control Panel**
1. Click 🎛️ to open the control panel
2. Click any tab button to trigger that tab's script
3. Use playback controls to pause/resume/stop

### When Triggered:
1. Tab rotation pauses
2. Switches to the selected tab
3. Robot fades in (lower-left corner)
4. Robot reads the script using TTS
5. Robot fades out when done
6. Rotation resumes

## Customizing the Robot

### Colors

Edit `src/renderer/scripts/robot.js` and modify the `colors` object:

```javascript
this.colors = {
  bodyDark: 0x2a2e39,     // Main body color
  bodyMid: 0x363a45,      // Secondary body color
  bodyLight: 0x4a4e59,    // Accent body color
  accent: 0x00bcd4,       // Glow/highlight color (cyan)
  accentGlow: 0x00e5ff,   // Bright glow color
  eyeColor: 0x00bcd4,     // Eye color
  mouthColor: 0x00bcd4    // Mouth color
};
```

### Accent Color Options
- Cyan (default): `0x00bcd4`
- Blue: `0x2962ff`
- Green: `0x26a69a`
- Purple: `0x9c27b0`
- Orange: `0xff9800`

### Robot Size

Modify the robot group position in `robot.js`:
```javascript
this.robot.position.y = -0.3; // Adjust vertical position
```

Or adjust camera distance:
```javascript
this.camera.position.set(0, 0.5, 3); // Closer = larger robot
```

## File Structure

```
livestream_robot_cohost/
├── src/
│   ├── main.js                 # Electron main process
│   ├── preload/
│   │   ├── setup-preload.js    # Setup window IPC bridge
│   │   ├── main-preload.js     # Main window IPC bridge
│   │   └── control-preload.js  # Control panel IPC bridge
│   ├── renderer/
│   │   ├── setup.html          # Setup window
│   │   ├── main.html           # Main stream view
│   │   ├── control.html        # Control panel
│   │   ├── styles/
│   │   │   ├── setup.css
│   │   │   ├── main.css
│   │   │   └── control.css
│   │   └── scripts/
│   │       ├── setup.js
│   │       ├── main.js
│   │       ├── robot.js        # 3D robot character
│   │       └── control.js
│   └── assets/
│       └── icon.png
├── build/
│   └── icon.ico               # Windows icon
├── sample-config.json         # Example configuration
├── package.json
└── README.md
```

## Configuration File

Configuration is saved to your app data folder:
- Windows: `%APPDATA%/livestream-robot-cohost/config.json`

### Sample Configuration

```json
{
  "tabs": [
    {
      "url": "https://s3.tradingview.com/d/DnlkZnpw_mid.webp",
      "script": "Welcome to our analysis of Bitcoin..."
    }
  ],
  "rotationInterval": 45,
  "speechRate": 1.0,
  "volume": 1.0
}
```

## OBS Setup

1. Add a **Window Capture** source
2. Select "Livestream Robot Cohost - Stream View"
3. Optionally crop to remove window borders
4. The dark theme blends well with TradingView's dark mode

## Troubleshooting

### TradingView Charts Not Loading
- Ensure URLs are valid TradingView chart links
- Some TradingView features may require login - use public charts when possible

### Robot Not Appearing
- Check if the tab has a script configured
- Try the "Test Robot" button in the control panel

### No Audio
- Check system volume and audio output device
- Adjust volume in the control panel
- Some browsers require user interaction before audio can play

### Performance Issues
- Close unnecessary applications
- Reduce the number of tabs with complex charts
- Lower the animation quality by simplifying the robot mesh

## Future Enhancements (Roadmap)

- [ ] YouTube API integration for real SuperChat monitoring
- [ ] Dynamic robot positioning per tab
- [ ] Breaking news integration from trusted sources
- [ ] Voice customization options
- [ ] More robot character designs
- [ ] Stream overlays and alerts

## License

MIT License - Feel free to modify and use for your streams!

## Support

For issues or feature requests, please open an issue on the project repository.
