# Grocery List

A simple web app for managing your shopping list. Build your list on your computer, send it to your phone via QR code or email, and check off items as you shop.

## Features

- Add and remove grocery items
- Check off items as you buy them
- Share your list to your phone via QR code or email link
- Send your list to Telegram for instant phone notifications
- Data persists in your browser between sessions
- Works on any device with a browser

## Live App

Open in your browser: https://liska84.github.io/my_reminder/

## Deploy Your Own Copy

### 1. Fork or clone the repository

```bash
git clone https://github.com/liska84/my_reminder.git
cd my_reminder
```

### 2. Create your own GitHub repository

1. Go to https://github.com/new
2. Name it `my_reminder` (or any name you prefer)
3. Set visibility to **Public** (required for free GitHub Pages)
4. Do not initialize with a README

### 3. Push to your repository

```bash
git remote set-url origin git@github.com:YOUR_USERNAME/my_reminder.git
git push -u origin main
```

### 4. Enable GitHub Pages

1. Go to your repository on GitHub
2. Navigate to **Settings > Pages**
3. Under "Source", select **Deploy from a branch**
4. Set branch to `main` and folder to `/ (root)`
5. Click **Save**

Your app will be live at `https://YOUR_USERNAME.github.io/my_reminder/` within a few minutes.

## Install as a macOS Dock App

You can create a clickable app icon that opens the grocery list in your browser.

### 1. Create the app bundle structure

```bash
mkdir -p GroceryList.app/Contents/MacOS
mkdir -p GroceryList.app/Contents/Resources
```

### 2. Create the launcher script

Create `GroceryList.app/Contents/MacOS/GroceryList` with this content:

```bash
#!/bin/bash
open "https://YOUR_USERNAME.github.io/my_reminder/"
```

Make it executable:

```bash
chmod +x GroceryList.app/Contents/MacOS/GroceryList
```

### 3. Create the Info.plist

Create `GroceryList.app/Contents/Info.plist`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>CFBundleExecutable</key>
    <string>GroceryList</string>
    <key>CFBundleIconFile</key>
    <string>AppIcon</string>
    <key>CFBundleIdentifier</key>
    <string>com.yourname.grocerylist</string>
    <key>CFBundleName</key>
    <string>Grocery List</string>
    <key>CFBundlePackageType</key>
    <string>APPL</string>
    <key>CFBundleVersion</key>
    <string>1.0</string>
</dict>
</plist>
```

### 4. Add an icon (optional)

If you have a 256x256 PNG icon:

```bash
mkdir -p /tmp/AppIcon.iconset
cp your_icon.png /tmp/AppIcon.iconset/icon_256x256.png
sips -z 128 128 your_icon.png --out /tmp/AppIcon.iconset/icon_128x128.png
sips -z 32 32 your_icon.png --out /tmp/AppIcon.iconset/icon_32x32.png
sips -z 16 16 your_icon.png --out /tmp/AppIcon.iconset/icon_16x16.png
iconutil -c icns /tmp/AppIcon.iconset -o GroceryList.app/Contents/Resources/AppIcon.icns
```

### 5. Add to Dock

1. Move `GroceryList.app` to your Desktop or `/Applications`
2. Drag it into your Dock

## Telegram Setup

You can send your grocery list directly to Telegram for instant notifications on your phone.

1. Open Telegram and message [@BotFather](https://t.me/BotFather)
2. Send `/newbot` and follow the prompts to create a bot
3. Copy the bot token BotFather gives you
4. Send `/start` to your new bot
5. Visit `https://api.telegram.org/bot<YOUR_TOKEN>/getUpdates` — find your chat ID in the JSON response under `"chat":{"id":...}`
6. In the app, click the gear icon (⚙), paste your bot token and chat ID, and hit Save

Your credentials are stored only in your browser's localStorage — they never leave your device except when sending a message to Telegram.

## Usage

1. Open the app (click the Dock icon or visit the URL)
2. Type an item name and click **Add** (or press Enter)
3. When ready to shop, click **Show QR code** and scan with your phone, click **Email to phone**, or click **Send to Telegram**
4. On your phone, check off items as you buy them
5. Back on your computer, click **Clear bought** to remove purchased items

## Requirements

- A modern web browser (Chrome, Safari, Firefox, Edge)
- A GitHub account (for hosting)
- macOS (for the Dock app — the web app itself works on any OS)
