# Apple Shortcuts - WhatsApp Photo Capture

A collection of Apple Shortcuts that enable automatic photo capture from the front camera and seamless integration with WhatsApp.

## 🎯 Overview

This project contains a two-part shortcut system that:

1. **WhatsApp Trigger** - Automatically opens a webpage when WhatsApp is accessed
2. **Photo Capture** - Captures a photo from the front camera via the webpage
3. **Photo Processing** - Encodes the photo in base64 and sends it to a Shortcut
4. **Photo Storage** - Decodes the base64 and saves the image to your Photos gallery

## 📁 Project Structure

```
apple-shortcuts/
├── index.html                 # Landing page with shortcut links
├── snap-on-open-wapp.html    # WhatsApp integration webpage
├── wapp.png                   # WhatsApp logo (referenced in snap-on-open)
├── Readme.md                  # This file
```

## 🚀 Quick Start

### Prerequisites
- Apple device (iPhone/iPad) with iOS 14+
- WhatsApp installed
- Apple Shortcuts app installed

### Installation

1. **Download the Shortcuts**
   - Open the [Shortcuts App](shortcuts://) on your Apple device
   - Set up the two main shortcuts: `ReceivePhoto` and `WhatsAppAutoCapture`

2. **Host the Webpage**
   - Deploy `snap-on-open-wapp.html` to a web server or use it locally
   - Update the shortcut with the correct URL to the webpage
   - Or use it as a file:// URL if running locally

3. **Grant Permissions**
   - Allow camera access when prompted
   - Allow Photos library access when prompted

## ⚙️ How It Works

### Part 1: Automation Trigger
When you open WhatsApp, an automation rule triggers and opens a URL that points to `snap-on-open-wapp.html`.

### Part 2: Photo Capture Web Page
The `snap-on-open-wapp.html` file:
- Displays a WhatsApp-themed loading screen
- Requests camera permissions
- Automatically captures a front camera photo after 1.5 seconds
- Encodes the photo to base64 JPEG format
- Passes the base64 data to the `ReceivePhoto` shortcut via the `shortcuts://` URL scheme

### Part 3: Photo Processing Shortcut
The `ReceivePhoto` shortcut:
- Receives the base64-encoded image data
- Decodes the base64 string back to an image
- Saves the image to the Photos library
- Optionally sends it to desired destinations (WhatsApp, iCloud, etc.)

## 🔗 URL Scheme Reference

The key URL scheme used:
```
shortcuts://run-shortcut?name=ReceivePhoto&input=text&text=[BASE64_DATA]
```

This tells the Shortcuts app to:
- Run the shortcut named `ReceivePhoto`
- Pass the base64 data as text input

## 📝 Files Explained

### `snap-on-open-wapp.html`
- **Purpose**: Photo capture interface triggered from WhatsApp
- **Features**:
  - WhatsApp-themed dark UI (#111b21 background)
  - Animated loading spinner
  - Automatic camera access request
  - Photo capture after 1.5 second delay
  - Base64 encoding with 0.6 quality JPEG

### `index.html`
- **Purpose**: Landing page and documentation hub
- **Features**:
  - Quick links to shortcuts
  - Setup instructions
  - Usage guide

## 🎨 Customization

### Modify Capture Delay
In `snap-on-open-wapp.html`, change the timeout value (line with `setTimeout`):
```javascript
setTimeout(() => {
  takePhoto();
}, 1500);  // Change 1500 to your desired milliseconds
```

### Change Image Quality
Adjust the quality parameter in the `toDataURL` call:
```javascript
const base64 = canvas.toDataURL("image/jpeg", 0.6);  // 0.6 = 60% quality
```

### Modify UI Theme
Update the CSS color values in the `<style>` section:
- `background: #111b21` - Main background color
- `border-top: 3px solid #25D366` - Spinner accent color (WhatsApp green)

## ⚠️ Privacy & Security Notes

- **Camera Access**: This shortcut requires camera permissions. Grant access only if you trust the source.
- **Data Encoding**: Photos are encoded as base64 before transmission. Keep sensitive photos in mind.
- **Local Deployment**: For maximum privacy, host the HTML file locally on your device.
- **No Cloud Upload**: By default, captured photos only go to your local Photos library.

## 🐛 Troubleshooting

### Camera not opening?
- Check that camera permissions are granted to Safari/Shortcuts in Settings
- Try running the shortcut directly instead of via automation

### Photo not saving?
- Verify the `ReceivePhoto` shortcut exists and is correctly configured
- Check that Photos app permissions are granted to Shortcuts
- Review the base64 encoding/decoding steps in the shortcut

### Automation not triggering?
- Ensure "Open URLs" is enabled in the shortcut automation settings
- WhatsApp automations work best on iOS 14.5+
- Try running the shortcut manually first to test

## 📱 Compatible Devices

- iPhone 6S and later
- iPad (2nd generation) and later
- iPod touch (6th generation) and later

Requires iOS 14 or later for full automation support.

## 📜 License

This project is provided as-is for personal use.

## 🤝 Contributing

Feel free to enhance this project with:
- Additional automation triggers
- Improved UI themes
- Video recording capability
- Cloud storage integration
- Multi-photo capture

## 📧 Support

For issues or questions:
1. Check the troubleshooting section above
2. Verify all permissions are granted
3. Test each component individually
4. Review the Shortcuts app logs

---

**Version**: 1.0  
**Last Updated**: April 2026
