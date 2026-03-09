# Product Requirements Document (PRD)
## Herominutes - AI-Powered Injury Recovery Platform

**Version**: 2.1  
**Last Updated**: December 25, 2024  
**Product Manager**: AI Product Team

---

## 1. Problem Statement

### The Challenge
Millions of people suffer from injuries and lack access to personalized, professional rehabilitation guidance. Traditional physical therapy requires:
- Expensive in-person consultations ($100-300/session)
- Limited appointment availability
- Generic "one-size-fits-all" exercise sheets
- No real-time adaptation to pain levels or progress

### The Opportunity
Leverage AI to democratize access to personalized injury recovery plans, combining the expertise of 7 medical specialists into one affordable, accessible platform.

---

## 2. Goals & Objectives

### Primary Goals
1. **Accessibility**: Provide professional-grade recovery plans to anyone with an internet connection
2. **Personalization**: Tailor plans to individual injuries, pain levels, and constraints
3. **Safety**: Incorporate multi-specialist oversight to prevent harmful progressions
4. **Engagement**: Keep users motivated through progressive achievements

### Success Metrics
| Metric | Target | Measurement |
|--------|--------|-------------|
| Plan Completion Rate | >60% | % of users completing all 5 phases |
| Pain Reduction | >40% | Average pain level reduction |
| User Retention | >40% | 30-day retention rate |
| NPS Score | >50 | Monthly user surveys |

---

## 3. Features

### Core Features (MVP)

#### F1: Onboarding Flow
- **Welcome Screen**: App introduction with 7 AI specialist showcase
- **Profile Selection**: Athlete, Active, or Healing user types
- **Goal Setting**: Return-to-sport, reduce pain, move better, get stronger

#### F2: Injury Assessment
- **Body Region Selection**: 8 body regions supported (shoulder, elbow, wrist/hand, hip, knee, ankle/foot, lower back, neck/upper back)
- **Injury Type Classification**: Sprain/strain, post-surgery, chronic pain, tendinitis, overuse
- **Pain Level Tracking**: 0-3 scale (Zero, Low, Medium, High) with visual color indicators
- **Surgery Details**: Specific surgery types per body region

#### F3: Constraints Configuration
- **Session Frequency**: 3, 4, 5, 6, or 7 sessions per week
- **Session Duration**: 15-20min, 30-40min, 45+min
- **Equipment Availability**: Bodyweight, bands, dumbbells, foam roller, gym
- **Environment**: Home, gym, or mix

#### F4: AI Plan Generation
- **7 Specialist Multi-Agent System**: Each specialist provides specialized expertise
  - Cardiologist: Cardiovascular health & progression
  - Neurologist: Neuromuscular patterns & proprioception
  - Orthopedic Surgeon: Bone & joint structural integrity
  - Kinesiologist: Movement science & biomechanics
  - Physical Therapist: Rehabilitation protocols
  - Sports Coach: Performance & conditioning
  - Care Coordinator: Synthesizes all inputs into cohesive plan
- **5-Phase Structure**: 
  1. Protection & Healing (2 weeks)
  2. Controlled Mobility (2 weeks)
  3. Strength & Stability (2 weeks)
  4. Power & Endurance (2 weeks)
  5. Return to Performance (2 weeks)
- **5 Exercises per Phase**: Specific, detailed exercise prescriptions
- **Safety Notes**: Red flags, precautions, and contraindications

#### F5: Daily Sessions
- **Exercise Cards**: Clear instructions with timing, sets, reps
- **Pain Monitoring**: Pre/post session pain checks (0-3 scale)
- **Flare-up Detection**: Automatic regression if pain increases
- **Progress Tracking**: Session and exercise completion tracking
- **Resume Support**: Pick up where you left off across devices

#### F6: User Authentication
- **Supabase Auth**: Email OTP (one-time passcode) authentication
- **Plan Persistence**: Save and retrieve plans in PostgreSQL
- **Cross-device Sync**: Access plans from any device
- **Guest Preview**: Limited access for unauthenticated users

#### F7: Clinical Credibility Features (NEW - December 2024)
- **Liability Waiver**: Touch signature capture with scroll-to-read requirement
- **Clinical Summary**: Collapsible specialist insights with summary bullets
- **Sources Section**: Evidence-based references with 6-level hierarchy
- **Conflict Resolution**: 4-tier priority system when specialists disagree
- **Age-Specific Guidelines**: 4 age cohort system with tailored modifications

#### F8: AI Safety Features (NEW - December 2024)
- **Conflict Resolution Rules**: Priority hierarchy (Safety > Medical > Performance > Coordination)
- **Age Detection**: Intake form field + regex fallback from notes
- **Conservative Defaults**: When uncertain, default to safer option
- **Red Flag Display**: Prominent safety precautions in Clinical Summary

### Immediate Post-MVP Priorities (January 2025)

#### P1: User Feedback Collection (HIGHEST PRIORITY)
- **In-App Feedback Forms**: Session rating after workout completion
- **NPS Surveys**: Monthly Net Promoter Score collection
- **Feature Request System**: Allow users to suggest improvements
- **Bug Reporting**: Easy way to report issues with screenshots
- **Recovery Outcome Tracking**: Did the plan help? Pain reduction metrics

#### P2: Stripe Payment Integration
- **Subscription Tiers**: Free, Premium ($9.99/mo), Pro ($19.99/mo)
- **Payment Flow**: Secure checkout with Stripe Elements
- **Trial Period**: 7-day free trial for Premium features
- **Billing Management**: Upgrade, downgrade, cancel functionality
- **Paywall Gates**: Restrict Phase 2-5 access for free users

#### P3: Analytics Dashboard
- **User Engagement Metrics**: DAU, WAU, MAU tracking
- **Conversion Funnel**: Free to Premium conversion rates
- **Plan Completion Rates**: Phase-by-phase drop-off analysis
- **Pain Reduction Tracking**: Aggregate recovery outcomes
- **Revenue Metrics**: MRR, churn rate, LTV calculations

### Phase 2 Features (Planned - Q2 2025)
- Exercise video library
- Voice-guided sessions
- Proactive injury prevention flows (morning/evening stretching)
- Pre/post workout mobility routines
- Pre/post sport warm-up/cool-down protocols
- Wearable integration (pain/ROM tracking)

---

## 4. User Flows

### Flow 1: New User Onboarding
```
Welcome → Sign In (Email OTP) → Profile → Injury → Constraints → Plan Generation → Plan Overview → Dashboard
```

### Flow 2: Returning User
```
App Load → Auto-Resume → Dashboard → Select Plan → Continue Session
```

### Flow 3: Session Completion
```
Start Session → Complete Exercises → Pain Check → 
├── Pain Same/Lower → Great Job! → Continue
└── Pain Higher → Flare-up Detected → Suggest Phase Regression
```

### Flow 4: Level Up
```
Complete All Sessions → Pain Consistently Low → 
"Level Up Available" → Create New Plan at Higher Level
```

---

## 5. Acceptance Criteria

### AC1: Plan Generation
- [x] Plans MUST include exactly 5 phases
- [x] Each phase MUST have exactly 5 exercises
- [x] Plans MUST include insights from all 7 specialists
- [x] Generation time MUST be under 60 seconds
- [x] Fallback to algorithmic generation if AI unavailable

### AC2: Security
- [x] GEMINI_API_KEY MUST only exist in Supabase Edge Function secrets
- [x] User data MUST be protected by RLS policies
- [x] JWT tokens validate user identity for all data access

### AC3: Accessibility
- [x] All interactive elements MUST have data-testid attributes
- [ ] Color contrast MUST meet WCAG AA standards
- [x] Touch targets MUST be at least 44x44px on mobile (PWA optimized)

### AC4: Performance
- [ ] First Contentful Paint MUST be under 1.5 seconds
- [ ] Time to Interactive MUST be under 3 seconds
- [x] API responses MUST be under 500ms (except AI generation)

---

## 6. Technical Requirements

### Frontend
- React 18+ with TypeScript
- Vite for build tooling
- Shadcn UI component library
- TanStack Query for data fetching
- Wouter for routing
- PWA optimized for iOS (Add to Home Screen)

### Backend
- Supabase Edge Functions (Deno runtime)
- Drizzle ORM with PostgreSQL
- Supabase Auth integration

### AI/ML
- Google Gemini 2.0 Flash
- 7-Specialist Multi-Agent System
- Algorithmic fallback for high-availability

### Infrastructure
- Replit for development & hosting
- Supabase for database, auth, and edge functions
- No Docker or containerization (Nix environment)

---

## 7. Pain Level System

### Scale: 0-3
| Level | Label | Color | Description |
|-------|-------|-------|-------------|
| 0 | Zero | Green | No pain |
| 1 | Low | Yellow | Mild discomfort |
| 2 | Medium | Orange | Moderate pain |
| 3 | High | Red | Significant pain |

### Usage
- Pre-session pain check
- Post-session pain check
- Pain trend tracking for flare-up detection
- Phase progression recommendations

---

## 8. Timeline & Milestones

| Milestone | Target Date | Status |
|-----------|-------------|--------|
| MVP Launch | Q4 2024 | Complete |
| Supabase Integration | Q4 2024 | Complete |
| 5-Phase Recovery System | Q4 2024 | Complete |
| Progress Persistence | Q4 2024 | Complete |
| Clinical Credibility Features | Dec 2024 | **Complete** |
| Conflict Resolution System | Dec 2024 | **Complete** |
| Age-Specific Guidelines | Dec 2024 | **Complete** |
| Evidence Hierarchy System | Dec 2024 | **Complete** |
| Liability Waiver | Dec 2024 | **Complete** |
| Video Library | Q1 2025 | Planned |
| Proactive Flows | Q1 2025 | Planned |
| Mobile App (Native) | Q2 2025 | Planned |

---

## 9. Appendix

### Specialist Roles (7-Specialist Multi-Agent System)
1. **Cardiologist**: Heart rate zones, cardiovascular progression, exercise tolerance
2. **Neurologist**: Proprioception, neuromuscular control, nerve healing
3. **Orthopedic Surgeon**: Tissue healing timelines, structural integrity, post-surgical protocols
4. **Kinesiologist**: Movement patterns, biomechanics, functional assessment
5. **Physical Therapist**: Rehabilitation protocols, manual therapy alternatives, home exercise programs
6. **Sports Coach**: Performance return, conditioning, sport-specific training
7. **Care Coordinator**: Synthesizes all specialist inputs into cohesive, progressive plan

### Equipment Options
- Bodyweight (no equipment needed)
- Resistance Bands
- Dumbbells
- Foam Roller
- Full Gym Access

### Clinical Credibility Components (NEW - December 2024)

#### Liability Waiver System
- Touch signature capture using canvas-based SignaturePad
- Scroll-to-bottom requirement before checkbox becomes active
- Stored securely in Supabase with timestamp
- Legal disclaimer text displayed prominently

#### Clinical Summary Dashboard
- Collapsible specialist cards with color-coded icons
- Summary bullets in plain language (max 15 words each)
- Red flags and safety precautions highlighted
- Expandable full assessment text
- Key recommendations per specialist

#### Evidence Hierarchy (6 Levels)
| Level | Type | Examples |
|-------|------|----------|
| 1 | Clinical Guidelines | ACSM, AHA, ACC |
| 2 | Meta-Analyses | Cochrane Library |
| 3 | Peer-Reviewed | PubMed, JOSPT, BJSM |
| 4 | Institutional | NIH, Mayo Clinic, Cleveland Clinic |
| 5 | Professional | APTA, NSCA, AAOS |
| 6 | Educational | ExRx.net, Physiopedia |

#### Conflict Resolution Hierarchy (4 Tiers)
| Priority | Specialists | Behavior |
|----------|-------------|----------|
| 1 (Highest) | Orthopedic Surgeon, PT, Cardiologist | Safety overrides all |
| 2 | Neurologist | Healing timelines override performance |
| 3 | Kinesiologist, Sports Coach | Apply within safety limits |
| 4 (Final) | Care Coordinator | Conservative synthesis |

#### Age-Specific Guidelines (4 Cohorts)
| Age Group | Key Modifications |
|-----------|-------------------|
| Young (<30) | Standard progression, higher intensity tolerance |
| Adult (30-50) | Joint-friendly, 5-10 min mobility required |
| Mature (50-65) | Extended warm-ups (10-15 min), lower impact |
| Senior (65+) | Balance priority, chair-supported, fall prevention |

---

## 10. Changelog

### Version 2.1 (December 25, 2024)
**AI Safety & Clinical Credibility MVP**

| Change | Section | Description |
|--------|---------|-------------|
| F7: Clinical Credibility | Features | Added liability waiver, clinical summary, sources section |
| F8: AI Safety | Features | Added conflict resolution, age-specific guidelines |
| Milestones Updated | Timeline | Marked 5 new features as Complete |
| Appendix Expanded | Appendix | Added detailed documentation for all new features |

**Technical Changes:**
- `supabase/functions/gemini-proxy/index.ts`: Added CONFLICT_RESOLUTION_RULES constant and getAgeSpecificGuidelines function
- `client/src/components/screens/LiabilityWaiverScreen.tsx`: Touch signature with scroll requirement
- `client/src/components/ClinicalSummary.tsx`: Specialist insights with summary bullets
- `client/src/components/SourcesSection.tsx`: 6-level evidence hierarchy display

### Version 2.0 (December 2024)
- Initial 7-specialist multi-agent system
- 5-phase recovery structure
- Pain tracking and flare-up detection
- Supabase authentication integration
