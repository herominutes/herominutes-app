# Herominutes System Architecture

Herominutes is built as a mobile-first Progressive Web Application designed to deliver AI-assisted injury recovery and mobility guidance for athletes.

The system is structured around a modern full-stack architecture combining a web client, backend services, and AI decision support.

---

# Architecture Overview

User (Athlete)
      │
      ▼
PWA Web App (React / TypeScript)
      │
      ▼
API Layer (Node / Express)
      │
      ▼
Supabase Backend
 ├ Database (Postgres)
 ├ Authentication
 └ Storage
      │
      ▼
AI Services
 ├ Recovery Plan Generation
 ├ Exercise Recommendation
 └ Specialist Agent System

---

# Core Components

## Frontend

The frontend is a mobile-first Progressive Web Application (PWA).

Responsibilities:

• user onboarding  
• injury assessment flow  
• recovery plan display  
• session tracking  
• progress dashboards  

Technologies:

- React
- TypeScript
- TailwindCSS
- PWA Service Workers

---

## Backend API

The backend handles application logic and orchestrates AI services.

Responsibilities:

• user session management  
• recovery plan generation  
• session tracking  
• data validation  

Technologies:

- Node.js
- Express
- TypeScript

---

## Database & Authentication

Herominutes uses Supabase for backend infrastructure.

Capabilities include:

• PostgreSQL database  
• user authentication  
• secure API access  
• file storage  

---

## AI Specialist System

Herominutes explores a **multi-agent AI approach** to recovery guidance.

Example specialists:

• injury recovery specialist  
• mobility specialist  
• sports performance specialist  
• rehabilitation protocol specialist  

These specialists analyze user injury data and generate structured recovery workflows.

---

# Key Product Capabilities

The architecture enables:

• structured injury recovery programs  
• stretching and mobility routines  
• progress tracking  
• recovery analytics  
• adaptive recommendations  

---

# Deployment Model

Herominutes is currently deployed as a Progressive Web Application allowing users to access the platform directly from their mobile browser.

Future versions may include:

• native mobile applications  
• wearable integrations  
• AI-driven recovery analytics
