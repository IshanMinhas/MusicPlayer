# MusicPlayer — MusicKiDuniya

A full-stack music streaming application where users can sign in, search and play songs, filter by artist/album/language/category, and minimize the player. Admins can upload songs, artists, and albums, and manage user roles.

## 🚀 Live Demo

- **Frontend (Vercel):** https://music-player-three-blush-66.vercel.app
- **Backend (Render):** https://musicplayer-api-92s1.onrender.com

> **Note:** The backend runs on Render's free tier and spins down after 15 minutes of inactivity. The first request after idle may take ~30–50 seconds to wake up.

## 🛠 Tech Stack

| Layer           | Technology                                       |
| --------------- | ------------------------------------------------ |
| **Frontend**    | React 17, Tailwind CSS, Framer Motion            |
| **Backend**     | Node.js, Express                                 |
| **Database**    | MongoDB Atlas (Mongoose)                         |
| **Auth**        | Firebase Authentication (Google Sign-In)         |
| **Storage**     | Firebase Cloud Storage (for audio & images)      |
| **Hosting**     | Vercel (client), Render (server)                 |

## 📐 Architecture

```
┌─────────────────┐        ┌──────────────────┐        ┌─────────────────┐
│  React Client   │  ───▶  │  Express Server  │  ───▶  │  MongoDB Atlas  │
│    (Vercel)     │        │     (Render)     │        │                 │
└────────┬────────┘        └──────────────────┘        └─────────────────┘
         │
         ▼
┌─────────────────────────┐
│  Firebase (Auth + File  │
│        Storage)         │
└─────────────────────────┘
```

## ✨ Features

- **Google Sign-In** via Firebase Auth
- **Search** songs by name, artist, or language
- **Filter** by artist, album, language, and category (Jazz, Rock, Melody, Karaoke)
- **Music player** with autoplay, next/previous track controls, and minimize
- **Admin dashboard** for managing users, songs, artists, and albums
- **Role-based access** (member / admin)
- **Responsive UI** with smooth animations (Framer Motion)

## 🏃 Running Locally

### Prerequisites

- Node.js 16+
- A MongoDB Atlas cluster (free M0 tier works)
- A Firebase project with Authentication + Cloud Storage enabled
- A Firebase Admin service account key

### 1. Clone and install

```bash
git clone https://github.com/IshanMinhas/MusicPlayer.git
cd MusicPlayer

# Install client deps
cd client && npm install && cd ..

# Install server deps
cd server && npm install && cd ..
```

### 2. Environment variables

Create `client/.env`:

```env
REACT_APP_API_URL=http://localhost:4000/
REACT_APP_FIREBASE_API_KEY=your_api_key
REACT_APP_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
REACT_APP_FIREBASE_PROJECT_ID=your_project_id
REACT_APP_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
REACT_APP_FIREBASE_MESSAGING_ID=your_messaging_sender_id
REACT_APP_FIREBASE_APP_ID=your_app_id
```

Create `server/.env`:

```env
DB_STRING=mongodb+srv://<user>:<password>@<cluster>.mongodb.net/musicplayer?retryWrites=true&w=majority
```

Place your Firebase Admin service account key at:
```
server/config/serviceAccountKey.json
```

### 3. Run

```bash
# Terminal 1 - Server (http://localhost:4000)
cd server && npm run dev

# Terminal 2 - Client (http://localhost:3000)
cd client && npm start
```

## 👑 Making a User an Admin

New users sign up with the `member` role by default. To promote to admin:

1. Open MongoDB Atlas → your cluster → **Browse Collections**
2. In the `musicplayer` database → `users` collection, find your user document
3. Change `role` from `"member"` to `"admin"`
4. Log out and log back in on the app

Admins will see additional dashboard tabs: **Users**, **Songs**, **Artist**, **Albums**, plus the song/artist/album upload forms.

## 📦 Deployment

### Client → Vercel
- Root directory: `client`
- Framework preset: Create React App
- Env vars: all `REACT_APP_*` values plus `CI=false` (to treat ESLint warnings as warnings, not errors)

### Server → Render
- Root directory: `server`
- Build command: `npm install`
- Start command: `node app.js`
- Env vars:
  - `DB_STRING` — MongoDB connection string
  - `FIREBASE_SERVICE_ACCOUNT` — full contents of `serviceAccountKey.json` as a single-line JSON string

### Firebase setup
- Enable **Google** provider in **Authentication → Sign-in method**
- Add your Vercel domain to **Authentication → Settings → Authorized domains**

## ⚠️ Notes & Limitations

- MongoDB Atlas free M0 pauses after ~60 days of inactivity. Visit the app occasionally to keep it warm.
- Render free tier has cold starts (~30–50s). Upgrade to paid ($7/mo) for always-on.
- Firebase Storage free tier is 5 GB, which is plenty for testing.
- Auto-deploys are wired up: every push to `master` redeploys both Vercel and Render.

## 📸 Screenshots

### UI
![UI](https://user-images.githubusercontent.com/84188309/187147327-c2feff8e-f3a2-4e55-9068-405da104af12.jpg)

### Users Dashboard
![Users Dashboard](https://user-images.githubusercontent.com/84188309/187147145-df8a291f-efbb-41c9-a372-fd633d27097f.jpg)

### Playlists
![Playlists](https://user-images.githubusercontent.com/84188309/187147239-97648f69-4cb8-42e3-8658-a1cbcd61a877.jpg)

### Minimized Music Player
![Minimized Player](https://user-images.githubusercontent.com/84188309/187146844-b58955b8-d099-43d6-972f-609cf87cc451.jpg)

## 📝 License

ISC

## 👤 Author

[Ishan Minhas](https://github.com/IshanMinhas)
