# Herominutes - Mobile Injury Recovery Application

## Overview
Herominutes is a mobile-first Progressive Web Application (PWA) designed to provide personalized injury rehabilitation and proactive wellness plans. It leverages AI (Google Gemini) to generate tailored, multi-phase recovery programs based on user-specific injury data and preferences. The application aims to deliver an athlete-focused experience, guiding users through a structured 5-phase recovery journey, with a core focus on enhancing engagement and recovery outcomes. It also supports proactive wellness programs like "Stretch & Flow" and "Posture," emphasizing comprehensive, AI-driven health management.

## User Preferences
Preferred communication style: Simple, everyday language.

## System Architecture

### UI/UX Decisions
The frontend is built with React 18, TypeScript, and Vite, adhering to a mobile-first responsive design. It uses `shadcn/ui` (based on Radix UI) and TailwindCSS for a consistent design system. The application features distinct view modes for onboarding, dashboard, plan viewing, and guided workout sessions for both injury recovery and proactive wellness. UI/UX is inspired by Apple's minimalistic design principles, featuring clear typography, subtle dividers, generous spacing, and simplified color schemes.

### Technical Implementations
- **Frontend**: React 18, TypeScript, Vite, React Query for server state management. Custom iOS PWA fixes are implemented for optimal mobile experience.
- **Backend**: Serverless architecture using Supabase Edge Functions (Deno runtime) for AI plan generation and CRUD operations.
- **Data Storage**: PostgreSQL database via Supabase, with Drizzle ORM for schema definition. Extensive Row Level Security (RLS) is used for data protection.
- **Authentication**: Supabase Auth provides JWT-based user authentication via Email OTP, with a unified sign-in experience. Guest users can access limited features.
- **Plan and Progress Persistence**: Session, round, and plan progress for both injury recovery and proactive wellness are persisted in Supabase PostgreSQL tables, with RLS ensuring data isolation.

### Feature Specifications
- **AI Plan Generation**: A 7-specialist multi-agent AI system (Google Gemini 2.0 Flash), with an algorithmic fallback, generates personalized 5-phase recovery and wellness plans. It incorporates a 4-tier conflict resolution hierarchy and age-specific guidelines. A 4-phase generation architecture ensures comprehensive exercise details including `executionSteps`, `formCues`, `breathingCues`, `purpose`, `equipmentSetup`, and `detailedModifications`.
- **Proactive Wellness Programs**: Supports "Stretch & Flow" and "Posture" programs with a streamlined 12-step intake wizard (age captured in main flow, routine defaults to AM+PM), generating 5-phase plans with 7 days/week commitment (14 total sessions with AM/PM) and integrating recovery tools.
- **Recovery Flow Optimization**: Streamlined 11-step intake wizard (frequency removed - defaults to 6 days/week for committed recovery, automatically reduced to 5 for high pain or post-surgery cases).
- **Phase Progression System**: Gated advancement through 5 phases with strict eligibility criteria:
  - **14-day consecutive requirement**: Users must complete required sessions for 14 consecutive days before advancing
  - **Pain thresholds**: Standard recovery 0-1 pain level, Post-surgery 0-2, Proactive 0-1
  - **Session requirements**: Recovery 6 days/week (5 for high pain/post-surgery), Proactive 7 days/week
  - **Celebration screens**: Full-screen animations with fitness-themed effects (blood flow particles, kinetic chain visualization, pulse ripples) when advancing phases
  - **Backend validation**: Supabase Edge Function (`phase-advancement`) validates eligibility and logs transitions
  - **Analytics tracking**: `phase_transitions` table logs all advancements with metrics snapshots for recalibration analysis
- **Active & Fit Pain Tracking**: Tracks pain/discomfort levels for "heart_recovery" programs, triggering "rest-advised" flows and logging pain events for analysis.
- **Exercise Library**: A separate `exercise_library` schema collects all AI-generated plans for future analysis, including intake data, exercise templates, and modifications, stored without user identification.
- **Injury-Specific Exercise Fallback System**: Comprehensive exercise library with activity-level progression:
  - **Activity Levels**: 4 tiers (beginner, intermediate, advanced, elite) with normalized mapping from all intake values
  - **Fallback Cascade**: injury-type + activity-level → injury-only → generic → hardcoded defaults
  - **Body Regions Covered**: Neck (~128 exercises), Lower Back (~100 exercises), Knee (~100 exercises)
  - **Injury Types**: Herniated disc, muscle strain, sciatica, stenosis (flexion-biased), degenerative disc, whiplash, radiculopathy
  - **Clinical Safety**: Stenosis exercises strictly flexion-biased, no extension drills
  - **Supported Body Regions**: Only neck, lower back, and knee are currently enabled. Other regions (shoulder, ankle, hip, wrist, head) show "Coming Soon" with lock icons.

### Exercise Library Migrations (Supabase)
**IMPORTANT**: These seed files are located in `supabase_migrations/exercises/` which is outside the Supabase CLI's managed migration directory (`supabase/migrations/`). **Do NOT use `supabase db push`** - it will not apply these files.

**Manual Execution Required**: Run these SQL files via Supabase SQL Editor or `psql`:

1. **Column Migration** (run first):
   ```bash
   # Via psql (replace with your connection string)
   psql "$DATABASE_URL" -f supabase_migrations/exercises/add_activity_level_column.sql
   ```
   Or copy contents into Supabase SQL Editor: `supabase_migrations/exercises/add_activity_level_column.sql`

2. **Seed Data Files** (run after column migration):
   - `supabase_migrations/exercises/lower_back_injury_specific_seed.sql` (~100 exercises)
   - `supabase_migrations/exercises/neck_injury_specific_seed.sql` (~128 exercises)
   - `supabase_migrations/exercises/knee_injury_specific_seed.sql` (~100 exercises)

**Verification Query**: After migration, verify data is loaded:
```sql
SELECT body_region, injury_type, activity_level, COUNT(*) 
FROM exercise_library 
WHERE activity_level IS NOT NULL 
GROUP BY body_region, injury_type, activity_level 
ORDER BY body_region, injury_type, activity_level;
```

Expected result: ~100+ rows per body region with activity_level values (beginner, intermediate, advanced, elite).

### System Design Choices
- **Mobile-First PWA**: Optimized for mobile devices, offering an installable, app-like experience.
- **Serverless Backend**: Utilizes Supabase Edge Functions for scalability and cost-efficiency.
- **Robust Data Model**: Comprehensive PostgreSQL schema with Drizzle ORM and RLS for secure and efficient data management.
- **Tiered AI Architecture**: Primary use of Gemini 2.0 Flash, with DeepSeek Chat as a fallback, and an algorithmic local generation as a final safeguard. All API keys are securely stored in Supabase Edge Function secrets.

### Recent Bug Fixes
- **Within-Phase Exercise Deduplication (Jan 2026)**: Fixed issue where DB query returning multiple rows with the same exercise name would cause 5 copies of the same exercise per phase. Added `seenNamesThisPhase` Set-based deduplication at lines 4421-4435 in `gemini-proxy/index.ts` to filter duplicates before cross-phase uniqueness processing. Tier selection now properly supplements phases with <5 exercises using hardcoded tier pools.

### AI Optimization Modules (Additive)
The following optimization modules are available in `gemini-proxy/index.ts` as optional alternatives to existing code paths:

- **Canonical Context Module**: Packages all intake data into reusable context objects with pre-computed rules
  - `buildRecoveryCanonicalContext()` / `buildProactiveCanonicalContext()`: Create structured context from intake
  - Pre-computed rules: Pain intensity, surgery timeline, age tier, equipment progression
  - Compact prompts: `getCompactContextPrompt()` reduces token usage by ~35%
  - Hash generation: `buildIntakeHash()` enables request caching

- **3-Core Generator Architecture**: Parallel specialist generation reducing latency by 50-70%
  - Recovery: Clinical/Movement/Performance domains → 7 specialists in 3 parallel calls
  - Proactive: Flexibility/Wellness domains → 5 specialists in 2 parallel calls
  - Deterministic fallbacks: `createFallbackSpecialistAnalysis()` guarantees all specialists present

- **Batch Exercise Detail Generation**: All exercises per phase in one call
  - `batchGenerateExerciseDetails()`: Recovery exercises with complete field population
  - `batchGenerateProactiveExerciseDetails()`: Proactive exercises with wellness focus
  - Contract-based prompts: Strict JSON schemas ensure no missing fields

- **QA Validators**: Completeness enforcement for generated content
  - `validateExerciseCompleteness()`: Checks all required fields including `equipmentSetup`
  - `validatePhaseExercises()`: Validates entire phase exercise arrays
  - Required fields: executionSteps, formCues, breathingCues, purpose, equipmentSetup, detailedModifications

- **Bulletproof Auto-Save System**: Server-side plan persistence with retry logic
  - `autoSaveRecoveryPlan()`: Saves recovery plans to `recovery_plans` table BEFORE returning to frontend
  - `autoSaveProactivePlan()`: Saves proactive plans to `proactive_plans` table BEFORE returning to frontend
  - 3-retry logic with exponential backoff (500ms, 1000ms, 2000ms)
  - Auto-enforces 4-plan limit by deleting oldest plan when at capacity
  - Returns `savedPlanId` and `autoSaved: true` flag in API response
  - Frontend should check `autoSaved` flag and skip redundant save if true
  - Integrated across ALL generation paths: multi-phase, Groq, Mistral, DeepSeek, and fallback
  - Exercise library backup happens non-blocking after primary save

## External Dependencies

### UI/Styling
- `@radix-ui/* packages`
- `shadcn/ui`
- `tailwindcss`
- `lucide-react`
- `framer-motion`

### State Management & Data Handling
- `@tanstack/react-query`
- `react-hook-form`
- `zod`

### Backend & Database
- `drizzle-orm`
- `@google/genai`
- `PostgreSQL` (via Supabase)

### Supabase Integration
- `Supabase Auth`
- `Supabase Database`
- `Supabase Edge Functions`

### AI Services
- Google Gemini 2.0 Flash
- DeepSeek Chat (fallback)