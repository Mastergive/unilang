# 🚀 UniLang Client
A custom ClassiCube client with Full Cyrillic support for chat and UI.

---

## 📊 Development Progress

### ✅ Completed
- **UTF-8 String Bypass:** Modified `String_.c` to allow bytes in the `0x0400` (Cyrillic) range.
- **Clipboard Unlock:** Updated `String_AppendUtf8` to allow pasting Russian text.
- **Input Filter Fix:** Removed the "bouncer" logic that deleted non-English characters.

### ⚠️ In Progress / Buggy
- **Bitmapped Drawing:** - *Status:* **GLITCHY**. 
  - *Issue:* Currently shows "►" and "0" because it defaults to `default.png`.
- **Texture Loading:** - *Status:* **CRASHING**. 
  - *Issue:* `ACCESS_VIOLATION` in `Context2D_MakeTexture` when `russian.png` is missing.

### ❌ Remaining Tasks
- [ ] **Width Calculation:** Fix chat bubbles being twice the length of the text.
- [ ] **Word Wrap Safety:** Prevent the game from splitting 2-byte characters at line breaks.
- [ ] **Final Font Atlas:** Align `russian.png` with the new character indices.

---

## 🛠 Troubleshooting the Crash
The client currently crashes if `russian.png` isn't found in the textures folder. To prevent this, ensure the drawing loop has a NULL check:

```c
struct Bitmap* atlas = (isRussianChar[i] && russianBitmap.scan0) ? &russianBitmap : &fontBitmap;
