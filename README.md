# Amar-Krishi-Final
# আমার কৃষি (Amarkrishi) - Food Loss Reduction Platform

A technology-powered web app to help Bangladesh farmers reduce food loss and protect their harvest through smart monitoring, weather alerts, pest detection, and community risk awareness.

---

## Quick Overview

*What it does:*
- Track crop batches (register harvested crops with weight, date, location, storage type)
- Get weather forecasts and alerts for your region
- Identify pests and diseases using AI (upload photos)
- Monitor crop freshness (health scanner)
- View community risk map (see other farmers' risk levels nearby)
- Voice assistant to ask questions in Bengali
- Earn badges for farming actions
- Export your data as CSV or JSON

*Languages:* English & Bengali (toggle anytime)

---

## Key Pages

### 1. *Landing Page*
- Hero section with statistics about food loss in Bangladesh
- Call-to-action: "Start Protecting Your Harvest"
- Links to Register or Login
- Language toggle (English ↔ Bengali)

### 2. *Dashboard*
- Quick stats: active batches, at-risk batches, interventions, badges earned
- List of your crop batches with risk levels
- High-risk alerts (if any)

### 3. *Add Crop Batch*
- Form to register a new harvest
- Fields: crop type (20 options), weight, harvest date, storage location (5 cities), storage type
- All fields translate to Bengali

### 4. *Weather Forecast*
- 5-day weather for your region
- Humidity & rain % for each day
- Smart alerts (high rain/temp warnings)
- Respects language setting

### 5. *Crop Health Scanner*
- Upload crop photo to check freshness
- Returns: Fresh/Rotten status + confidence %

### 6. *Pest Identification*
- Upload pest/damage photo
- AI identifies pest and suggests treatment (in Bengali)
- Uses Google Gemini API

### 7. *Local Risk Map*
- Interactive map showing your location + neighboring farmers
- Color-coded risk levels (Low=green, Medium=yellow, High=red)
- Supports all major Bangladesh districts

### 8. *Voice Assistant*
- Click microphone → speak in Bengali
- App responds to: weather, rice, warehouse, harvest questions
- Responses are audio + text

### 9. *Profile*
- View your info (name, email, phone, language)
- Achievements: unlocked badges
- Export data as CSV or JSON

---

## Technical Stack

| Component | Technology |
|-----------|-----------|
| Frontend | HTML5 + CSS3 + Vanilla JavaScript |
| Auth | Firebase Authentication |
| Maps | Leaflet.js + OpenStreetMap |
| Weather API | OpenWeatherMap |
| AI/Image | Google Gemini 1.5 Flash |
| Speech | Web Speech API (browser native) |
| Storage | localStorage (browser) + Firebase |

---

## How It Works

### Registration & Login
1. User registers with email, password, name, phone, language preference
2. Firebase creates the account
3. User profile stored in browser localStorage (so login persists across page reloads)
4. On login, Firebase validates email/password, then app loads dashboard

### Adding a Crop Batch
1. Form inputs: crop type, weight (kg), harvest date, location, storage type
2. App calculates risk level (random: Low/Medium/High)
3. Smart alert shown (e.g., "rain expected, turn on fan")
4. Badge check: if first harvest → "First Harvest Logged" badge unlocked
5. Data saved to in-memory store

### Weather & Alerts
1. App fetches 5-day forecast from OpenWeatherMap based on district coordinates
2. Shows humidity + rain % for each day
3. Auto-generates advisory:
   - High rain (>70%) → "Cut rice or cover it"
   - High temp (>35°C) → "Irrigate in afternoon"
   - Favorable → "Good time for storage"

### Pest Detection
1. User uploads crop photo
2. Photo sent to Google Gemini API (base64 encoded)
3. Gemini identifies pest + risk level + Bengali treatment steps
4. Fallback: mock response if API fails

### Voice Assistant
1. Clicks microphone → browser records speech (Bengali)
2. Speech Recognition API transcribes text
3. App matches keywords: আবহাওয়া (weather), ধান (rice), গুদাম (warehouse), কাট (cut/harvest)
4. Returns relevant response + speaks back in Bengali

---

## File Structure


c:\Users\acer\OneDrive\Desktop\newfinal\
├── Amarkrishi.html          (entire app in one file)
└── README.md                (this file)


*Why one file?*
- Simple deployment (just open in browser)
- No backend needed
- Firebase handles auth + data sync

---

## Key Features Explained

### 1. *Bilingual (English & Bengali)*
- Toggle button in header (landing) and sidebar (app)
- All UI text translates instantly
- Storage location & type options have Bengali names
- Weather alerts in selected language

### 2. *Persistent Login*
- User profile saved to localStorage as amarkrishi_appData
- Survives page reload
- Cleared on logout

### 3. *Smart Alerts*
- High-risk batches trigger warnings in dashboard
- Weather-based recommendations
- SMS-style notifications in console (for testing)

### 4. *Badges System*
- First Harvest Logged
- Risk Mitigated Expert (5+ interventions)
- Weather Watcher
- Pest Finder
- Shown on profile; unlock on actions

### 5. *Data Export*
- CSV: export all batches (crop, weight, location, risk, status)
- JSON: export full user data (profile, batches, badges, interventions)

---

## How to Use

### Setup
1. Open Amarkrishi.html in a modern browser (Chrome, Firefox, Edge)
2. Allow location access if browser asks (for map)
3. Allow microphone access for voice assistant

### Workflow
1. *Register* with Gmail and password
2. *Add batches* (your harvested crops)
3. *Check weather* to plan next actions
4. *Upload crop photo* to scan freshness
5. *Use voice* to ask farming questions
6. *View map* to see community risk levels
7. *Export data* when needed
8. *Logout* when done (clears local session)

### Tips
- Use Bengali language for better regional experience
- Voice assistant works best with clear Bengali speech
- Weather alerts appear automatically when you add a batch
- Badges unlock on specific actions (encourage farmers to monitor regularly)

---

## Data Storage

| Data | Where | When Cleared |
|------|-------|--------------|
| User profile | localStorage + Firebase | On logout |
| Crop batches | In-memory (session) | On page reload |
| Badges/interventions | In-memory (session) | On page reload |
| Settings (language) | localStorage | On logout |

*Note:* Batches & badges are NOT persisted yet (session-only). To make them permanent, store in Firebase Firestore.

---

## API Keys & Limits

| Service | Key Status | Rate Limit |
|---------|-----------|-----------|
| Firebase | Active | Included in free tier |
| OpenWeatherMap | Active | 60 calls/min free tier |
| Google Gemini | Active | 60 req/min free tier |
| Leaflet/OSM | Free/Open | No key needed |
| Web Speech API | Browser native | No limits |

---

## Future Enhancements

- [ ] Persist batches to Firestore (permanent storage)
- [ ] Add Google Sign-In button
- [ ] Send SMS alerts (integrate Twilio)
- [ ] Mobile app (React Native)
- [ ] Community forum for farmers
- [ ] Multi-language support (Urdu, Hindi, etc.)
- [ ] Video tutorials in Bengali
- [ ] Offline support (Progressive Web App)

---

## Troubleshooting

| Issue | Cause | Solution |
|-------|-------|----------|
| Login not working after logout | Session data cleared | Register again or use localStorage check in console |
| Weather not loading | API key invalid or offline | Check OpenWeatherMap API key in code (line ~1200) |
| Pest detection fails | Gemini API error or bad image | Try again; check image format (JPG/PNG) |
| Voice not working | Microphone not allowed | Check browser permissions for microphone |
| Language not switching | Cache issue | Hard refresh (Ctrl+Shift+R) or clear localStorage |

---

## Team Members

- Maruf Al Karim
- Muntasir Naser
- Md Saman Hossein

---

## Contact & Support

- *Framework:* Firebase + Leaflet
- *Designed for:* Bangladesh farmers
- *Language:* Bengali & English
- *License:* Open source

---

*Last Updated:* November 29, 2025

Enjoy using আমার কৃষি! 🌾
