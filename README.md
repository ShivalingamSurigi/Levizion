# Levizion – Modern Real-Time Video Calling Platform

Levizion is a production-oriented, high-assurance real-time video communication platform built with **Next.js App Router**, **TypeScript**, **Tailwind CSS**, **LiveKit WebRTC**, and **Supabase**.

---

## 🌟 Highlights & Key Features

1. **Brand Identity & Ultra-Modern UI**:
   - Distinctive glowing Levizion brand logo with live pulse indicator.
   - Dark & Light mode theme toggle.
   - Premium glassmorphic navigation, cards, and responsive layouts.

2. **Phone Number Verification & Protected Directory**:
   - Register and verify accounts with phone number and SMS OTP.
   - User directory allows searching **only verified, registered users**.
   - Strict privacy safeguards: unverified numbers and blocked users are never exposed.

3. **Live Signaling & Call Invitation Protocol**:
   - Outgoing call overlay with pulsating radar animations and telecom-standard audio ringers.
   - Incoming call prompt with caller identification, avatar, and distinct melodic chime.
   - Full acceptance gating: camera and microphone connections are only established after explicit receiver consent.
   - Instant response signaling: Accept, Decline, Cancel, and Busy states.

4. **Genuine Real-Time Video & Audio (LiveKit + WebRTC)**:
   - Real hardware camera and microphone integration with echo cancellation, noise suppression, and auto gain control.
   - Server-side LiveKit JWT access token minting via `/api/livekit/token` (zero secret keys leaked to frontend).
   - Dynamic video grid, floating Picture-in-Picture local preview tile, active speaker highlight, and audio wave indicators.
   - In-call controls: Microphone mute/unmute, Camera toggle, Screen sharing, and End call.
   - Real-time in-call text messaging / data channel.

5. **Call Analytics, History, Blocks & Reports**:
   - Persistent call logs with duration timing, call status (Completed, Missed, Declined), and timestamps.
   - Quick one-click redial.
   - Comprehensive user blocking and abuse reporting workflows.

---

## 🚀 Quick Start (Local Development)

The application is running and accessible at:
👉 **[http://localhost:3000](http://localhost:3000)**

### 1. Test 2-User Video Calling Across 2 Browser Tabs / Windows
You can immediately test real two-way peer calling on your machine:
1. Open **Tab 1** in standard browser mode: Navigate to `http://localhost:3000/dashboard`.
   - By default, Tab 1 is logged in as **Sarah Connor** (`+1 555-010-1111`).
2. Open **Tab 2** in an **Incognito / Private Window**: Navigate to `http://localhost:3000/auth`.
   - Click the quick profile button for **Alex Vance** (`+1 555-010-2222`) or enter name & phone number with code `123456`.
3. In **Sarah's window (Tab 1)**:
   - Search `+1 555-010-2222` or `Alex Vance`.
   - Click **Video Call**.
4. In **Alex's window (Tab 2)**:
   - Alex's browser immediately chimes with an incoming call from Sarah Connor!
   - Click **Answer**.
5. Both sessions enter the real-time WebRTC room with live camera, mic, screen sharing, timer, and chat!

---

## 🛠️ Tech Stack & Directory Structure

```
Levizion/
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   ├── auth/register-or-verify/route.ts  # Phone verification & profile upsert
│   │   │   ├── users/search/route.ts             # Registered phone lookup
│   │   │   ├── calls/invite/route.ts             # Rate-limited call invitations
│   │   │   ├── calls/respond/route.ts            # Accept/decline/cancel signaling
│   │   │   ├── calls/events/route.ts             # SSE real-time cross-client bus
│   │   │   ├── calls/history/route.ts            # Persistent call history
│   │   │   ├── calls/block/route.ts              # Block / unblock actions
│   │   │   ├── calls/report/route.ts             # Trust & safety report filings
│   │   │   └── livekit/token/route.ts            # Server-side LiveKit JWT generation
│   │   ├── auth/page.tsx                         # Registration & OTP screen
│   │   ├── dashboard/page.tsx                    # User dashboard & device diagnostics
│   │   ├── call/[roomId]/page.tsx                # Real-time WebRTC video room
│   │   ├── layout.tsx                            # App shell, Navbar, Footer, Modals
│   │   ├── page.tsx                              # High-conversion Landing page
│   │   └── globals.css                           # Tailwind base & animations
│   ├── components/
│   │   ├── incoming-call-modal.tsx               # Pulsating incoming call dialog
│   │   ├── outgoing-call-modal.tsx               # Radar ringing calling overlay
│   │   ├── video-room.tsx                        # LiveKit room, tiles & controls
│   │   ├── user-search.tsx                       # Phone directory search component
│   │   ├── call-history-list.tsx                 # Call history with redial & options
│   │   ├── block-report-dialog.tsx               # Safety block & report modal
│   │   ├── navbar.tsx                            # Brand header & identity switcher
│   │   └── footer.tsx                            # Security & compliance footer
│   ├── context/
│   │   └── auth-context.tsx                      # User profile & call signaling state
│   └── lib/
│       ├── audio-service.ts                      # Web Audio API ringtone synthesizer
│       ├── call-signaling.ts                     # Cross-tab signaling & event store
│       ├── livekit.ts                            # LiveKit SDK token minter
│       ├── types.ts                              # TypeScript data contracts
│       ├── utils.ts                              # Formatters & avatar helpers
│       └── supabase/client.ts                    # Supabase client connector
├── supabase/
│   └── migrations/
│       └── 001_initial_schema.sql                # Complete PostgreSQL SQL migration
├── .env.local.example
└── README.md
```

---

## 🗄️ Database Setup (Supabase PostgreSQL)

1. Create a project at [supabase.com](https://supabase.com).
2. Open the **SQL Editor** in your Supabase dashboard.
3. Paste and run the contents of [`supabase/migrations/001_initial_schema.sql`](./supabase/migrations/001_initial_schema.sql).
4. In your Supabase Project Settings, copy:
   - **Project URL** -> `NEXT_PUBLIC_SUPABASE_URL`
   - **Anon Key** -> `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - **Service Role Key** -> `SUPABASE_SERVICE_ROLE_KEY`
5. Enable Phone Auth in **Authentication -> Providers -> Phone** (Twilio, MessageBird, or Supabase Test Phone numbers).

---

## 🎙️ LiveKit WebRTC Setup

1. Create a free account at [cloud.livekit.io](https://cloud.livekit.io).
2. Generate an API Key and Secret in **Settings -> Project Settings -> Keys**.
3. Set your environment variables in `.env.local`:
   ```env
   NEXT_PUBLIC_LIVEKIT_URL=wss://your-project.livekit.cloud
   LIVEKIT_API_KEY=your_livekit_key
   LIVEKIT_API_SECRET=your_livekit_secret
   ```

---

## ☁️ Deployment to Vercel

1. Push this repository to GitHub or GitLab.
2. In the [Vercel Dashboard](https://vercel.com), click **Add New... -> Project** and import the repository.
3. Add the environment variables from `.env.local.example`.
4. Deploy! Next.js App Router and server-side route handlers compile seamlessly.
