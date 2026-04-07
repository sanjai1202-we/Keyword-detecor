# 📖 SDN AR Scanner

An Augmented Reality (AR) scanner for mobile browsers that uses OCR to detect SDN-related keywords from a textbook page and automatically plays an explanatory video — followed by an interactive quiz.

---

## 🚀 Features

- **Camera-based OCR** — Uses [Tesseract.js](https://github.com/naptha/tesseract.js) to read text from your phone's camera in real time.
- **Smart keyword detection** — A 3-layer detection system ensures the video only triggers when the correct textbook page is in view.
- **Auto-play video** — Once the SDN Controllers page is detected, `video.mp4` plays automatically with full player controls.
- **Built-in quiz** — A 5-question multiple-choice quiz launches after the video ends to reinforce learning.
- **No app install needed** — Runs entirely in the browser. No image markers or tracking files required.
- **Works at any angle/lighting** — Pure OCR-based detection, not image-matching.

---

## 📁 Project Structure

```
Keyword-detecor-main/
├── index.html   # Main AR scanner page (all-in-one: HTML, CSS, JS)
├── video.mp4    # SDN Controllers explanatory video (compressed for mobile)
└── README.md    # This file
```

---

## 🔍 How It Works

### Detection Engine — 3-Layer System

To prevent false triggers (e.g. a random page with the word "network"), detection uses three layers that **must all pass** simultaneously:

| Layer | Rule | Threshold |
|---|---|---|
| **Layer 1 — Topic Groups** | Keywords are organized into concept clusters (SDN Controller, OpenFlow, Flow Management, etc.). Must hit distinct groups. | ≥ 3 unique groups |
| **Layer 2 — Raw Count** | Total keyword matches across all groups. | ≥ 4 keyword hits |
| **Layer 3 — Confirmation** | Must pass Layers 1 & 2 in consecutive scans to rule out single-frame noise. | 2 consecutive passes |

**Keyword groups monitored:**
- `SDN Controller`, `Software-Defined Network`, `SDN Architecture`
- `OpenFlow`, `Open Flow Protocol`
- `Flow Management`, `Flow Table`, `Flow Entry`, `Packet Forwarding`
- `Topology Management`, `Network Topology`, `Topology Discovery`
- `Network Discovery`, `Device Discovery`
- `End-User`, `End User Discovery`, `Host Discovery`
- `Northbound Interface`, `Southbound Interface`, `Control Plane`, `Data Plane`

**Anchor keywords** (rare, section-specific terms like `openflow`, `northbound interface`) count as +2 group hits each when matched, making detection even more precise.

---

## 📱 Usage

1. **Host the files** on any web server (or open `index.html` directly on a device that supports camera access via file://).
2. **Open in a mobile browser** (Chrome on Android or Safari on iOS recommended).
3. **Grant camera permission** when prompted.
4. **Point the camera** at the *SDN Controllers* section (Section 2.5) of your textbook.
5. Watch the **keyword pills** at the bottom light up as terms are detected.
6. When enough keywords are confirmed, the **video plays automatically**.
7. After the video ends, the **quiz launches automatically** (or tap the "Take Quiz" button).

---

## 🎮 Video Player Controls

| Control | Action |
|---|---|
| ▶ / ⏸ | Play / Pause |
| ⏪ 10s | Rewind 10 seconds |
| ⏩ 10s | Skip forward 10 seconds |
| Progress bar | Tap or drag to seek |
| Speed (1×▲) | Change playback speed (0.5× – 2×) |
| ✕ | Close video and return to scanner |

---

## 📝 Quiz

- 5 multiple-choice questions on SDN Controller concepts.
- Instant feedback with explanations for each answer.
- Score ring animation and performance message at the end.
- Full answer review after completion.

**Topics covered:**
1. Role of an SDN Controller
2. Purpose of OpenFlow
3. Northbound vs Southbound interfaces
4. Flow Management
5. Network Topology Discovery

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| [Tesseract.js v5](https://cdn.jsdelivr.net/npm/tesseract.js@5/dist/tesseract.min.js) | In-browser OCR engine |
| Vanilla JS / HTML5 | App logic and UI |
| CSS3 | Animations, scanner UI |
| `getUserMedia` API | Camera access |

No backend, no frameworks, no build step required.

---

## ⚙️ Configuration

Key constants at the top of the `<script>` block in `index.html`:

```js
const MIN_GROUPS         = 3;   // Minimum distinct concept groups to match
const MIN_TOTAL_KEYWORDS = 4;   // Minimum total keyword hits
const CONFIRM_SCANS      = 2;   // Consecutive passing scans before trigger
```

Adjust these to make detection stricter (higher values) or more lenient (lower values).

---

## 🌐 Deployment

Since the app uses `getUserMedia`, camera access requires a **secure context**:

- ✅ `https://` — works on any hosting platform (GitHub Pages, Netlify, Vercel, etc.)
- ✅ `localhost` — works for local development
- ❌ `http://` on a remote server — camera will be blocked by the browser


## 📋 Browser Compatibility

| Browser | Support |
|---|---|
| Chrome (Android) | ✅ Full support |
| Safari (iOS 14.3+) | ✅ Full support |
| Firefox (Android) | ✅ Full support |
| Desktop Chrome/Firefox | ✅ Works (uses front camera or webcam) |

---

## 📄 License

This project is for educational use.
