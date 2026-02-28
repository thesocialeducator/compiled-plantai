# PlantAI — Compiled Intelligence Platform

> **Know your land before you plant a single seed.**

Farm.ai is a precision agriculture platform that analyzes soil composition, climate history, vegetation health, and crop compatibility for any property using USDA data, satellite imagery, and AI-powered recommendations.

## 🌾 Features

### Core Analysis
- **Soil Intelligence** — USDA SSURGO soil classification, pH levels, organic matter, drainage
- **Climate Profiling** — 30-year historical normals, growing season length, hardiness zones, frost dates
- **Vegetation Health** — Sentinel-2 NDVI (Normalized Difference Vegetation Index) analysis
- **Crop Compatibility Matrix** — Suitability scores for 15+ crops with yield projections
- **Economic Projections** — 3 revenue scenarios (Max Yield, Low Maintenance, Pest Resistant)

### Advanced Features (v2.0)
✨ **All NEW in this release:**

#### 1. **Perplexity-Style Dynamic Citations**
- Inline glowing citation pills `[1]` [2] [3] next to every data point
- Expandable "Sources & Factuality" footer revealing all 7 government/scientific databases
- Transparency: See exactly which agencies powered each analysis

#### 2. **High-Yield Property Recommendations**
- MapLibre integration showing 3-4 nearby parcels with similar soil/yield profiles
- AI-recommended parcels displayed as warm orange polygons with yield match %, soil match %
- Click popup for quick comparison, "Run Full Analysis" button for deep dives
- Auto-fetches recommendations when map loads

#### 3. **AI Agronomist Chat Interface**
- Floating glassmorphism chat button (bottom-right, always accessible)
- Context-aware AI responses powered by Gemini 2.5 Flash
- Full property analysis bundled into every query for hyper-personalized answers
- Typing indicator, suggestion chips, message history persistence
- Framer Motion animations: spring drawer, slide-up messages, smooth transitions

#### 4. **AAA-Grade 3D Farm Visualization**
- Real-time sky dome with sun position tracking (SunCalc integration)
- Volumetric cloud systems (clear: 3 clouds, rain/snow: 8 clouds)
- Dynamic particle systems: rain (3000 instances), snow (800 sparkles)
- Procedurally-generated grass-blade normal maps & roughness textures
- Weather-responsive materials (clear→wet→snowy)
- Cinematic post-processing: Depth of Field, Bloom, Vignette, Hue-Saturation boost
- Interactive OrbitControls with responsive terrain

---

## 🏗️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | Next.js 16.1 (Turbopack), React 18, TypeScript, Tailwind CSS |
| **3D Rendering** | React Three Fiber, Three.js, @react-three/drei, @react-three/postprocessing |
| **State Management** | Zustand (lightweight, performant) |
| **UI Animations** | Framer Motion (spring, AnimatePresence) |
| **Map** | MapLibre GL (open-source, privacy-first) |
| **Backend** | FastAPI (Python), Google Gemini API |
| **Data Sources** | USDA SSURGO, Open-Meteo, Copernicus Sentinel-2, NWS, NOAA |

---

## 📁 Repository Structure

```
farm-ai/
├── plantai/                          # Next.js frontend
│   ├── src/
│   │   ├── app/
│   │   │   ├── layout.tsx           # Root layout
│   │   │   ├── page.tsx             # Landing page
│   │   │   ├── map/page.tsx         # Drawing interface
│   │   │   ├── analysis/[id]/       # Main dashboard (7 tabs)
│   │   │   └── farm/[id]/           # 3D visualization
│   │   ├── components/
│   │   │   ├── chat/
│   │   │   │   └── AgronomistChat.tsx     # AI chat drawer
│   │   │   ├── farm/
│   │   │   │   ├── Atmosphere.tsx         # Sky, sun, fog
│   │   │   │   ├── WeatherSystem.tsx      # Rain/snow
│   │   │   │   ├── PostProcessing.tsx     # Effects
│   │   │   │   ├── TerrainMesh.tsx        # Textures
│   │   │   │   └── FarmScene.tsx          # 3D orchestrator
│   │   │   ├── map/
│   │   │   │   └── MapCanvas.tsx          # MapLibre + recommendations
│   │   │   └── ui/
│   │   │       ├── CitationPill.tsx       # Citation pills
│   │   │       └── SourcesFooter.tsx      # Sources footer
│   │   └── lib/
│   │       ├── store.ts              # Zustand state
│   │       └── apiClient.ts          # API calls
│   └── package.json
│
└── plantai-backend/                  # FastAPI backend
    ├── main.py                       # API endpoints
    ├── services.py                   # Data fetching
    └── requirements.txt              # Dependencies
```

---

## 🚀 Quick Start

### Prerequisites
- **Node.js 18+**
- **Python 3.9+**
- **Git**

### Installation

```bash
# Clone
git clone https://github.com/thesocialeducator/compiled-plantai.git
cd compiled-plantai

# Frontend
cd plantai
npm install

# Backend
cd ../plantai-backend
pip install -r requirements.txt
```

### Environment Setup

**Frontend** (`.env.local` in `plantai/`)
```env
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_MAPTILER_KEY=YOUR_MAPTILER_KEY  # Optional
```

**Backend** (`.env` in `plantai-backend/`)
```env
GOOGLE_API_KEY=YOUR_GEMINI_API_KEY
```

### Run Locally

**Terminal 1:**
```bash
cd plantai
npm run dev
# http://localhost:3000
```

**Terminal 2:**
```bash
cd plantai-backend
python main.py
# http://localhost:8000/docs
```

---

## 📊 User Workflow

1. **Enter Address** — Search bar with Nominatim geocoding
2. **Draw Property** — Click points on map to outline field
3. **Analyze** — Backend fetches USDA, Open-Meteo, Sentinel-2 data in parallel
4. **Explore Dashboard** — 7 tabs: Overview, Soil, Climate, Crops, Economics, Agents, Plan
5. **View Citations** — Click pill `[1]` to see sources in expandable footer
6. **Chat with AI** — Click green button, ask context-aware questions
7. **3D Visualization** — Click "3D View" for interactive farm scene

---

## 🔄 NEW API Endpoints

### Chat (Context-Aware AI)
```
POST /api/chat
{
  "message": "Why tomatoes?",
  "history": [...],
  "context": { "soilData": {...}, "cropMatrix": [...] }
}
→ {"reply": "Your Cecil sandy loam with 6.2 pH..."}
```

### Recommendations (High-Yield Parcels)
```
POST /api/recommendations
{ "lat": 40.79, "lng": -77.86 }
→ GeoJSON FeatureCollection with 4 nearby parcels
```

---

## 🎨 Design Highlights

- **Glassmorphism** — Blur, semi-transparency, subtle borders
- **Dark Mode** — `#0a0d0a` background, `#4ade80` accent green
- **Responsive** — Mobile-first Tailwind CSS
- **Smooth Animations** — Framer Motion spring easing
- **Accessibility** — ARIA labels, semantic HTML

---

## 📦 Key Dependencies

**Frontend:**
- `@react-three/fiber` — R3F for 3D
- `@react-three/postprocessing` — Post-process effects
- `maplibre-gl` — Interactive maps
- `framer-motion` — Smooth animations
- `zustand` — Lightweight state

**Backend:**
- `fastapi` — Modern Python API
- `google-genai` — Gemini AI integration
- `pydantic` — Data validation
- `shapely` — Geospatial math

---

## 🧪 Testing

```bash
# Build verification
cd plantai && npm run build

# API test
curl -X POST http://localhost:8000/api/chat \
  -H "Content-Type: application/json" \
  -d '{"message":"Crops?","history":[],"context":{"soilData":{"name":"Loam","ph":6.5}}}'
```

---

## 🔐 Security Notes

⚠️ **Demo API key in repo** — Rotate before production!

**Pre-deployment:**
- [ ] Rotate all API keys
- [ ] Enable HTTPS
- [ ] Add authentication (OAuth2)
- [ ] Configure CORS origins
- [ ] Enable rate limiting
- [ ] Audit Gemini prompts

---

## 📈 Roadmap

- **Phase 2:** IoT soil sensors, subscription tiers, mobile app
- **Phase 3:** Drone imagery, real-time alerts, insurance optimization

---

## 📄 License

MIT License — See LICENSE file

---

## 👥 Contributing

1. Fork the repo
2. Create feature branch (`git checkout -b feature/amazing`)
3. Commit (`git commit -m 'Add feature'`)
4. Push (`git push origin feature/amazing`)
5. Open PR

---

## 📧 Support

- **Issues:** GitHub Issues
- **Email:** contact@farm.ai

---

## 🛠️ Maintenance & Mirroring

To push updates from the local repository to the new GitHub origin:

1. **Set the Remote (if not already set):**
   ```bash
   git remote set-url origin https://github.com/thesocialeducator/compiled-plantai.git
   ```

2. **Stage and Commit Changes:**
   ```bash
   git add .
   git commit -m "Update message"
   ```

3. **Push to GitHub:**
   ```bash
   git push origin main
   ```

---

**Made with 🌾 for farmers who think ahead.**
