# StyleSet — Photo-based Style Recommender (Single File)

A minimal, client‑only web app that lets users upload a picture and get a suggested **style set**.  
It supports **optional API integration** (multipart upload). If no API is configured, it uses a simple, deterministic on‑device analyzer so it works out‑of‑the‑box on GitHub Pages (no installs).

## ✅ Features
- Upload image (kept in the browser).
- **API mode**: POSTs `image` (multipart/form-data) to your endpoint; expects JSON.
- **Local mode**: Fallback analyzer infers warm/cool tone and seasonal palette from average colors.
- Single `index.html` file: drop it in a repo and enable GitHub Pages.
- Persist API settings in `localStorage`, or pass via URL query params.

## 🧪 Expected API Response (example)
Your endpoint should accept `multipart/form-data` with an `image` field and respond like:
```json
{
  "styles": ["Casual Minimalist", "Warm Autumn Palette"],
  "palette": ["#c58a6a","#3b4d61","#e9c46a"],
  "notes": "Detected warm undertone; earth tones recommended."
}
```
- Auth: if you require a key, set the **Authorization: Bearer &lt;key&gt;** header.  
- In the UI, paste your API URL and Key, set **Mode = Use API**, then **Analyze**.

## 🔧 Configure via URL
You can prefill settings using query parameters:
```
?apiUrl=https://your-endpoint.example.com/infer&apiKey=YOUR_TOKEN&mode=api
```

## 🚀 Deploy to GitHub Pages
1. Create a new public repo, e.g., `styleset-web`.
2. Add `index.html` (from this project root) and commit.
3. In **Settings → Pages**, choose:
   - **Source**: `Deploy from a branch`
   - **Branch**: `main` / `/ (root)` → **Save**  
4. Open the provided Pages URL to use the app.

## 🔐 Security Notes
- Do **not** commit secrets to your repo. Enter API keys in the UI or via URL only.
- Ensure your endpoint supports **CORS** for your GitHub Pages origin.
- Consider rate limiting and content restrictions server-side.

## 🧭 How the Local Analyzer Works
- Downscales the image, computes average color + top buckets.
- Heuristic for warm/cool and a seasonal palette: Spring/Summer/Autumn/Winter.
- Generates style set suggestions per season. No personal data leaves the browser.

## 📁 Project Structure
```
index.html    # Single self-contained app file
README.md     # Quick start and API contract
```

## 🐛 Troubleshooting
- **API failed. Check URL/key and CORS.** → Enable CORS on your API; verify the route and method (POST).
- Blank preview? → Ensure you uploaded a PNG/JPG and the browser has permission.
- Colors odd? → Provide a well-lit photo; avoid heavy filters.

---

Happy shipping! ✨
