# Herominutes - AI-Powered Injury Recovery Platform

A personalized injury recovery application powered by 7 AI medical specialists, built with React, Express, and Supabase.

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                              FRONTEND (React/Vite)                          │
│                         Hosted on Replit (Port 5000)                        │
│                                                                             │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐│
│  │  Welcome    │  │  Profile &  │  │   Plan      │  │   Dashboard &       ││
│  │  Screen     │→ │  Injury     │→ │  Generation │→ │   Sessions          ││
│  │             │  │  Forms      │  │  & Overview │  │                     ││
│  └─────────────┘  └─────────────┘  └──────┬──────┘  └─────────────────────┘│
│                                           │                                 │
└───────────────────────────────────────────┼─────────────────────────────────┘
                                            │
                    ┌───────────────────────┼───────────────────────┐
                    │                       │                       │
                    ▼                       ▼                       ▼
    ┌───────────────────────┐  ┌───────────────────────┐  ┌───────────────────┐
    │   Supabase Edge Fn    │  │   Supabase Auth       │  │  Supabase DB      │
    │   (gemini-proxy)      │  │   (Authentication)    │  │  (PostgreSQL)     │
    │                       │  │                       │  │                   │
    │   GEMINI_API_KEY      │  │   User Management     │  │  Plans, Sessions  │
    │   stored here ONLY    │  │   JWT Tokens          │  │  User Data        │
    └───────────────────────┘  └───────────────────────┘  └───────────────────┘
              │
              ▼
    ┌───────────────────────┐
    │   Google Gemini API   │
    │   (AI Plan Generation)│
    └───────────────────────┘
```

## Security Model

### API Key Security
- **GEMINI_API_KEY**: Stored ONLY in Supabase Edge Function secrets
  - Never stored in Replit environment
  - Never exposed to frontend
  - Never committed to version control

- **SUPABASE_URL / SUPABASE_ANON_KEY**: Safe to expose (Supabase anon key is designed for frontend use with RLS)

### Authentication Flow
1. User authenticates via Supabase Auth
2. JWT token issued and stored client-side
3. Token passed to Edge Functions for validation
4. Protected routes require valid JWT

## Setup Instructions

### 1. Supabase Configuration

1. Create a Supabase project at [supabase.com](https://supabase.com)

2. Add the following secrets to your Supabase Edge Function:
   ```bash
   # In Supabase Dashboard > Settings > Edge Functions
   GEMINI_API_KEY=your_google_gemini_api_key
   ```

3. Deploy the Edge Function:
   ```bash
   cd supabase
   supabase functions deploy gemini-proxy
   ```

4. Add environment variables to Replit:
   - `SUPABASE_URL` - Your Supabase project URL
   - `SUPABASE_ANON_KEY` - Your Supabase anon/public key

### 2. Google Gemini API Key

1. Get your API key from [Google AI Studio](https://aistudio.google.com/)
2. Add it ONLY to Supabase Edge Function secrets (never to Replit)

### 3. Database Setup

The app uses Supabase PostgreSQL. Tables are auto-created via Drizzle migrations.

Run migrations:
```bash
npm run db:push
```

## Development

```bash
# Install dependencies
npm install

# Run development server
npm run dev
```

The app runs on port 5000.

## Project Structure

```
├── client/                    # React frontend
│   ├── src/
│   │   ├── components/        # UI components
│   │   │   ├── screens/       # Full-page screens
│   │   │   └── ui/            # Shadcn UI components
│   │   ├── hooks/             # Custom React hooks
│   │   ├── lib/               # Utilities
│   │   │   ├── geminiProxy.ts # Supabase Edge Function client
│   │   │   ├── supabase.ts    # Supabase client
│   │   │   └── queryClient.ts # React Query setup
│   │   └── App.tsx            # Main app component
│   └── public/                # Static assets
├── server/                    # Express backend (for DB operations)
│   ├── routes.ts              # API routes
│   ├── storage.ts             # Database interface
│   └── gemini.ts              # Constants & types only
├── supabase/
│   └── functions/
│       └── gemini-proxy/      # Supabase Edge Function
│           └── index.ts       # Gemini API proxy
├── shared/
│   └── schema.ts              # Database schema & types
└── docs/
    ├── PRD.md                 # Product Requirements
    └── PRODUCT_STRATEGY.md    # Product Strategy
```

## Features

- **7 AI Specialists**: Cardiologist, Neurologist, Orthopedic Surgeon, Kinesiologist, Physical Therapist, Sports Coach, Care Coordinator
- **5-Phase Recovery Plans**: 10-week progressive rehabilitation programs (Protection & Healing → Controlled Mobility → Strength & Stability → Power & Endurance → Return to Performance)
- **Pain Tracking**: 0-3 scale (Zero/Low/Medium/High) with automatic flare-up detection
- **Activity Level Progression**: Level up from beginner to elite
- **Progress Persistence**: Resume your plan from any device
- **Secure Authentication**: Supabase Auth with Email OTP

## Cost Considerations

- **Supabase**: Free tier includes 500MB database, 2GB file storage, 50,000 monthly active users
- **Gemini API**: Pay-per-use, approximately $0.001 per plan generation
- **Replit**: Free for development, deployment may require paid plan

## Deployment

The app is designed to work with Replit's deployment:

```bash
npm run build
npm start
```

For production, ensure all environment variables are set in Replit Secrets.
