# Pricing Strategy Document
## Herominutes - AI-Powered Injury Recovery Platform

**Version**: 1.0  
**Last Updated**: December 2024

---

## 1. Executive Summary

Herominutes follows a **freemium model** with value-based pricing. The strategy focuses on demonstrating immediate value through a free preview, then converting engaged users to premium subscriptions for full access to the 5-phase recovery journey.

### Key Pricing Principles
1. **Value First**: Free tier demonstrates clear value before asking for payment
2. **Fair Pricing**: Positioned at 1/10th the cost of traditional physical therapy
3. **Simple Tiers**: Clear differentiation between free, premium, and pro
4. **Annual Incentive**: Significant discount for annual commitment

---

## 2. Subscription Tiers

### Free Tier - "Recovery Preview"
**Price**: $0/month

**Includes**:
- Phase 1 access only (Protection & Healing)
- 1 recovery plan per month
- Basic 7-specialist plan generation
- 5 exercises in Phase 1
- Pain tracking (current session only)
- Guest access without account required

**Limitations**:
- Cannot progress beyond Phase 1
- No session history
- No progress persistence across devices
- No clinical summary reports
- Standard AI processing speed

**Purpose**: Hook users with immediate value, demonstrate the quality of AI-generated plans

---

### Premium Tier - "Full Recovery"
**Price**: $9.99/month | $79.99/year (33% savings)

**Includes**:
- All 5 phases unlocked
- Unlimited plan generation
- Full session tracking & history
- Progress persistence across devices
- Pain trend analytics
- Clinical summary reports (PDF export)
- Resume from any device
- Priority support

**Target User**: Active individuals who want complete recovery guidance

**Value Proposition**: 
- Traditional PT: $150-300/session x 8 sessions = $1,200-2,400
- Herominutes Premium: $80/year = **95% cost savings**

---

### Pro Tier - "Performance Recovery"
**Price**: $19.99/month | $159.99/year (33% savings)

**Includes**:
- Everything in Premium
- Exercise video library (HD demonstrations)
- Proactive injury prevention flows
  - Morning mobility routines
  - Evening recovery stretches
  - Pre-workout warm-ups
  - Post-workout cool-downs
  - Sport-specific protocols
- AI specialist chat (powered by Gemini)
- Wearable integrations (Apple Watch, Fitbit)
- Family sharing (up to 4 members)
- Personalized session scheduling
- Advanced analytics dashboard

**Target User**: Athletes and fitness enthusiasts who want comprehensive injury management

---

### Enterprise Tier - "Clinical Solutions"
**Price**: Custom (starting at $500/month)

**Includes**:
- Everything in Pro
- Bulk user licensing
- Custom branding (white-label)
- Admin dashboard with analytics
- Patient outcome tracking
- Integration APIs
- HIPAA compliance features
- Dedicated account manager
- Custom exercise protocols
- Telehealth integration options

**Target User**: Physical therapy clinics, gyms, sports teams, insurance providers

---

## 3. Pricing Psychology

### Anchoring Strategy
Position Premium ($9.99/mo) against:
1. **Physical Therapy**: $150-300/session
2. **Personal Training**: $50-100/session
3. **Gym Memberships**: $30-100/month

Herominutes costs less than a single PT session while providing ongoing support.

### Annual Discount Rationale
- **33% discount** for annual commitment
- Monthly: $9.99 x 12 = $119.88/year
- Annual: $79.99/year (saves $39.89)
- Encourages commitment through recovery journey (10-week minimum)

### Free Trial Strategy
- **No credit card required** for Free tier
- **7-day Premium trial** for new signups
- Trial includes full Phase 1-3 access
- Automatic reminder before trial ends

---

## 4. Conversion Funnel

### Stage 1: Awareness
- Free onboarding flow
- 7-specialist showcase
- Plan preview generation

### Stage 2: Activation
- Complete Phase 1 exercises
- Experience pain tracking
- See progress indicators

### Stage 3: Conversion Trigger
- "Unlock Phase 2" prompt after Phase 1 completion
- Show Phase 2-5 exercises (locked preview)
- Display expected recovery timeline
- Offer 7-day Premium trial

### Stage 4: Retention
- Daily session reminders (push notifications)
- Streak tracking and achievements
- Progress milestones celebration
- Phase completion rewards

### Stage 5: Expansion
- "Level Up" to higher activity level
- Proactive prevention flows (Pro upgrade)
- Family sharing recommendations

---

## 5. Competitive Pricing Analysis

| Competitor | Monthly Price | Annual Price | Key Difference |
|------------|---------------|--------------|----------------|
| RecoverMe | $14.99 | $99.99 | No AI, generic plans |
| Physio.co | $29.99 | $249.99 | Video-only, no personalization |
| PT Hub | $49.99 | $399.99 | For practitioners only |
| YouTube Premium | $13.99 | $139.99 | No structure, conflicting advice |
| **Herominutes** | **$9.99** | **$79.99** | **7 AI specialists, 5-phase structure** |

### Price Positioning
- **Lower than competitors** while offering superior personalization
- **Premium positioning** through AI specialist branding
- **Value-based** rather than cost-based pricing

---

## 6. Revenue Projections

### Year 1 Assumptions
- 10,000 MAU target
- 5% free-to-premium conversion
- 1% premium-to-pro upsell
- 80% annual subscription ratio

### Revenue Model

| Metric | Month 6 | Month 12 |
|--------|---------|----------|
| Free Users | 8,000 | 80,000 |
| Premium Users | 400 | 4,000 |
| Pro Users | 40 | 400 |
| Monthly Revenue | $5,596 | $55,960 |
| Annual Run Rate | $67,152 | $671,520 |

### Unit Economics
- **Customer Acquisition Cost (CAC)**: Target $10
- **Lifetime Value (LTV)**: $120 (12-month avg)
- **LTV:CAC Ratio**: 12:1 (healthy)
- **Payback Period**: 1 month

---

## 7. Monetization Timeline

### Phase 1: Foundation (Current)
- Free tier with Phase 1 access
- No payment processing yet
- Focus on user acquisition and engagement

### Phase 2: Soft Launch (Q1 2025)
- Introduce Premium tier
- 7-day free trial
- Stripe integration for payments
- Annual subscription option

### Phase 3: Optimization (Q2 2025)
- A/B test pricing points ($7.99 vs $9.99 vs $12.99)
- Introduce Pro tier
- Add family sharing
- Launch referral program

### Phase 4: Enterprise (Q3-Q4 2025)
- Custom enterprise pricing
- Volume discounts for clinics
- Insurance partnership pilot
- White-label solution

---

## 8. Payment Processing

### Recommended: Stripe
- Industry standard for SaaS
- Handles subscriptions natively
- Global payment methods
- Easy Supabase integration

### Billing Features
- Monthly and annual billing cycles
- Automatic renewal
- Proration for mid-cycle upgrades
- Dunning management for failed payments
- Invoice generation for enterprise

### Payment Methods
- Credit/debit cards
- Apple Pay / Google Pay
- Bank transfers (Enterprise)
- Regional payment methods (future)

---

## 9. Discount & Promotion Strategy

### Launch Promotions
- **Founding Member**: First 1,000 users get 50% off first year
- **Early Bird**: 25% off annual during beta period

### Ongoing Promotions
- **Referral Program**: Give $10, get $10 credit
- **Student Discount**: 50% off with .edu email
- **Military/First Responder**: 25% off
- **Corporate Wellness**: Volume pricing for employers

### Seasonal Campaigns
- **New Year Resolution** (January): 30% off annual
- **Summer Sports** (June): Free Pro trial for athletes
- **Back to School** (September): Student promotion

---

## 10. Pricing FAQ

### Why is there a free tier?
The free tier allows users to experience the value of our 7-specialist AI system before committing financially. Phase 1 demonstrates immediate relief and builds trust.

### Why is Premium so affordable compared to PT?
Our AI-powered approach allows us to deliver personalized guidance at scale, dramatically reducing the cost per user while maintaining quality.

### Can I downgrade from Pro to Premium?
Yes, you can downgrade at any time. Your pro features will remain active until the end of your billing period.

### Do you offer refunds?
We offer a 30-day money-back guarantee for annual subscriptions. Monthly subscriptions can be cancelled anytime with no refund for the current period.

### Is there a family plan?
Pro tier includes family sharing for up to 4 members, making it cost-effective for households with multiple active individuals.

---

## 11. Success Metrics

| Metric | Target | Measurement |
|--------|--------|-------------|
| Free-to-Trial Conversion | 15% | % of free users starting trial |
| Trial-to-Paid Conversion | 40% | % of trial users converting |
| Annual Subscription Rate | 70% | % choosing annual vs monthly |
| Churn Rate | <5%/month | Monthly cancellation rate |
| ARPU | $12/month | Average revenue per user |
| LTV | $120 | Lifetime value per user |

---

## 12. Future Pricing Considerations

### Potential Add-ons (à la carte)
- Single plan generation: $2.99
- Clinical summary report: $4.99
- Video library access: $4.99/month
- Specialist chat session: $1.99/session

### Geographic Pricing
- Regional pricing for emerging markets
- Purchasing power parity adjustments
- Local currency support

### B2B Expansion
- Per-seat licensing for clinics
- Usage-based pricing for high-volume
- Custom API access pricing
