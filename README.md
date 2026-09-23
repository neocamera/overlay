# neocamera

**Version 1.5.0** — `neocamera-v1.5.0.html`

A camera app in one HTML file. It looks like the stock iPhone camera app. It takes photos and it records video. It makes no network calls and it loads no libraries, thus it operates fully offline.

---

## Features

- **Photo mode.** Touch the shutter to take a photo. The app saves a JPG file immediately.
- **Video mode.** Touch the shutter to start. Touch it again to stop. The app saves the video file immediately.
- **Audio-only mode.** If the camera is not available, but the microphone is, the app records sound only.
- **Automatic download.** Each capture goes to the download folder of the browser. No preview screen and no extra touch are necessary.
- **Continuous operation.** The camera stays live after each capture. You can capture again immediately.
- **Front and rear cameras.** Touch the flip button to change the camera. The preview of the front camera is a mirror image. The saved file is not a mirror image. This is the same behavior as iOS.
- **Guide photo overlay.** The button at the bottom left adds a photo above the preview. The photo helps you to align a new shot. It is never part of a saved file.
- **Aspect ratio.** A row above the camera view gives 1:1, 4:3, 3:2, and 16:9, in a vertical or a horizontal shape. It applies to photo mode and to video mode alike. The frame on the screen and the saved file agree.
- **Tap to focus.** Touch the preview to set the focus point and the exposure point. Hold to lock them.
- **Recording timer.** A red indicator and a timer are at the top of the screen during a recording.
- **Screen lock prevention.** The screen stays on during a recording, if the browser gives this function.

## Interface

| Control | Position | Function |
|---|---|---|
| Shutter | Bottom center | Takes a photo, or starts and stops a recording |
| Mode labels | Above the shutter | Change between photo and video. A swipe on the preview also changes the mode |
| Flip | Bottom right | Changes between the front and the rear camera |
| Guide | Bottom left | Adds a guide photo, or removes it |
| Opacity slider | Above the preview | Sets how strong the guide photo is |
| Aspect ratio row | Above the preview | Sets the shape and the orientation of the photo or the video |
| Preview | Center | Touch to focus, hold to lock, swipe to change the mode |

Keyboard: the space bar or the enter key operates the shutter.

## Aspect ratio

A row above the camera view gives 1:1, 4:3, 3:2, and 16:9. It applies to photo mode and to video mode alike, thus the width and the height of a saved video file change with it, not only the shape on the screen.

The first button in the row sets the orientation. It shows `Vertical` or `Horizontal`. Touch it to change the orientation, and the labels turn with it. For example, 4:3 becomes 3:4. The app selects the orientation of the screen at the start, thus a phone starts with vertical shapes.

The row locks during a recording, because a change of the shape while the recorder is running is not possible.

A video recording does not always redraw the picture. If the chosen shape is already close to the true shape of the camera, the app records the camera directly, for the best quality and the smallest use of the processor. The app redraws the picture, frame by frame, only when the chosen shape needs an actual crop of the camera image. This is the mechanism that lets a recording swap between a portrait shape and a landscape shape: a crop that is taller than it is wide gives a portrait file, and a crop that is wider than it is tall gives a landscape file, regardless of the true shape of the camera sensor.

The frame on the screen shows the result. The app cuts the sides of the camera image by the same quantity when it writes the JPG file. Thus the file agrees with the screen.

The aspect ratio applies to photo mode only. Video mode always uses the full frame of the camera. The stock app operates in the same manner, because the recorder cannot cut the video without an extra conversion stage.

## Focus and exposure

| Action | Result |
|---|---|
| Touch the preview | A yellow square shows the point. The app sets the focus there and measures the exposure there |
| Hold the preview | The square stays and `AE/AF LOCK` shows at the top. The focus and the exposure do not change again |
| Drag up or down after a touch | Changes the exposure, if the camera gives this control. A sun symbol shows at the side of the square |
| Touch again | Sets a new point and removes the lock |

The yellow square always shows. The control of the hardware is different for each browser. Chrome on Android usually gives focus point, focus mode, and exposure control. Safari on iOS does not make these controls available to a web page, thus the square is an indication only on an iPhone. The app hides the sun symbol if the camera does not give exposure control.

## Guide photo overlay

Use a guide photo to repeat the composition of an earlier shot.

1. Touch the grey plus at the bottom left.
2. Select a photo file.
3. The photo comes above the preview at 50 percent opacity. A slider comes above the preview.
4. Move the slider to change the opacity between 0 and 100 percent.
5. Touch the photo to change between fit and fill. Fit shows the full photo. Fill covers the full frame.
6. Touch the grey X at the bottom left to remove the photo and the slider.

While a guide photo is on screen, a touch on the preview changes fit and fill. Use a hold to set the focus and the lock.

The guide photo is an element of the interface only. The app captures photos from the camera frame, and it records video directly from the camera. Thus the guide photo is not in the JPG file, the video file, or the audio file.

The overlay stays in the frame of the camera. It does not go on the black bars at the sides. It follows a change of the aspect ratio. The overlay does not turn to a mirror image with the front camera, because the saved file is also not a mirror image. The camera and the recorder operate as usual while the overlay is on screen.

## Permissions

The app asks for the camera and the microphone when it starts. If you refuse one permission, the app uses the other one.

| Camera | Microphone | Result |
|---|---|---|
| Allowed | Allowed | Photo mode and video mode with sound |
| Allowed | Refused | Photo mode and video mode without sound |
| Refused | Allowed | Audio-only recording. Photo mode is off |
| Refused | Refused | The app shows a message and a button to try again |

## File names and formats

| Capture | Name | Format |
|---|---|---|
| Photo | `IMG_20260914_142233.jpg` | JPEG, quality 0.92 |
| Video | `VID_20260914_142233.mp4` | MP4 (H.264/AAC) if the browser gives it |
| Audio | `AUD_20260914_142233.m4a` | MP3 if the browser gives it, or M4A |

The name contains the local date and the local time.

**Important:** the browser controls the recording format. The app asks for MP4 first, and MP3 first for audio. Safari and recent versions of Chrome give MP4. Firefox and older browsers give WebM only. In that condition the app writes a `.webm` file, because a change of format needs an external library. Almost no browser can write MP3, thus the audio file is usually `.m4a`. No conversion is possible offline in one file.

## How to use

1. Put `neocamera-v1.5.0.html` on a web server with HTTPS, or on `localhost`.
2. Open the file in the browser.
3. Give permission to the camera and the microphone.

A secure origin is necessary. Browsers refuse camera access on plain HTTP. Chrome also permits a local `file://` page, but Safari does not. For a phone, GitHub Pages is a sufficient host.

The browser can ask for permission before it saves more than one file. Allow this to keep the automatic download.

## Browser support

| Browser | Photo | Video | Format |
|---|---|---|---|
| Safari on iOS 15 or later | Yes | Yes | MP4 |
| Chrome on Android | Yes | Yes | MP4 or WebM |
| Chrome and Edge on desktop | Yes | Yes | MP4 (version 130 or later) |
| Firefox | Yes | Yes | WebM |

## Not in this version

These functions of the stock app are not implemented: flash and torch, zoom, grid, timer, exposure and focus control, portrait mode, panorama, slow motion, time lapse, Live Photos, shutter sound, and a photo library.

## Technical notes

- One file. No external requests, no fonts, no libraries, and no build step.
- The app uses `getUserMedia`, `canvas.toBlob`, and `MediaRecorder` only.
- The preview keeps the full aspect ratio of the camera. Thus the saved image agrees with the image on the screen.
- The app saves the full sensor frame. It does not crop the image.
- The app writes no data to the disk of the browser and it uses no cookies.
- The guide photo stays in the memory of the browser only. The app releases the object URL when you remove the photo.
- The app makes a copy of a large guide photo at 1600 pixels maximum. A file of less than 0.9 MB goes directly to the overlay. The app keeps the PNG format if the source can have transparency.
- The overlay is on an independent compositing layer. Thus a change of the opacity does not draw the photo again.

## Changelog

### 1.5.0
- Changed: the aspect ratio row now applies to video mode. A recorded video file has the chosen shape, including a swap between a portrait shape and a landscape shape.
- New: video recording redraws the picture only when the chosen shape needs a crop of the camera image. A shape that is already close to the true shape of the camera skips this, for a recording of the best quality.
- Changed: the aspect ratio row locks during a recording.

### 1.4.0
- Changed: the aspect ratio row shows above the camera view at all times, in photo mode. The button that opened and closed it is removed.
- Removed: the Full aspect ratio option.
- Changed: the button that changes the camera is 10 percent larger.

### 1.3.1
- Fixed: a button could take the native system look on some mobile browsers, instead of the custom pill shape.

### 1.3.0
- New: a vertical or a horizontal shape for each aspect ratio. A button in the list changes the orientation.
- Fixed: Full now uses the true shape of the camera image. It gave a square frame before.
- Fixed: the frame measures the camera image again when the camera starts and when you change the camera.

### 1.2.1
- Changed: the app has the name neocamera.

### 1.2.0
- New: aspect ratio control with 1:1, 4:3, 3:2, 16:9, and Full. Photo mode only.
- New: touch to focus, hold to lock the focus and the exposure, and drag to change the exposure.
- New: a touch on the guide photo changes between fit and fill.
- Changed: the app prepares a large guide photo at a smaller size. The overlay opens much more quickly.

### 1.1.0
- New: a guide photo overlay with an opacity slider.
- Changed: the button at the bottom left controls the overlay. The last-file function is removed.

### 1.0.0
- First release: photo mode, video mode, audio-only mode, automatic download, camera flip, recording timer, and iOS-style interface.
