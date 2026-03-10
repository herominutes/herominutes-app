# Herominutes Mobile App - Design Guidelines

## Design Approach
**Reference-Based Design**: Draw inspiration from health/wellness apps like MyFitnessPal, Headspace, and Nike Training Club - clean, motivating, and athlete-focused. Combine with the professional medical aesthetic of telemedicine platforms.

## Brand Identity
- **Tone**: Professional yet empowering, athletic yet accessible, medical yet motivating
- **Emotion**: Confidence, hope, progress, expert care
- **Core Value**: Elite athlete care made accessible to everyone
- **Logo**: Muscular turtle mascot with backpack and sunglasses - represents strength, resilience, and steady progress

## Color Palette
- **Primary**: Vibrant lime green (#ceff00 / HSL 72 100% 50%) - energetic, fresh, athletic
- **Primary Foreground**: Dark text (215 25% 15%) for contrast on lime backgrounds
- **Accent**: Teal green (160 70% 42%) - complementary for success states
- **Background**: Light warm gray (210 20% 98%) in light mode, deep blue-gray (215 25% 9%) in dark mode
- **Note**: The lime green is a bold, energetic choice that should be used for CTAs and primary actions

## Layout System

### Mobile-First Foundation
- **Primary Device**: iPhone 12 mini (375×812px)
- **Container**: Single-column layout, full-width screens
- **Padding**: Consistent horizontal padding of p-4 (16px) on mobile, p-6 (24px) on larger screens
- **Vertical Spacing**: Use py-6, py-8, py-12 for section spacing
- **Tailwind Units**: Primarily use spacing units of 2, 4, 6, 8, 12, 16, 20 for consistency

### Screen Structure
Each screen follows this pattern:
- **Header Area**: Title (text-2xl font-bold) + subtitle/helper text (text-sm text-gray-600)
- **Content Area**: Forms, cards, or information panels with generous spacing (space-y-6)
- **Footer Area**: Primary CTA button fixed or near bottom with secondary back button

## Typography Hierarchy

### Font Selection
- **Primary**: Inter or SF Pro Display (system font) for clean, modern readability
- **Weights**: 400 (regular), 600 (semibold), 700 (bold)

### Type Scale
- **Screen Titles**: text-2xl font-bold (24px)
- **Section Headers**: text-lg font-semibold (18px)
- **Body Text**: text-base (16px) - never smaller for primary content
- **Helper Text**: text-sm text-gray-600 (14px)
- **Captions**: text-xs text-gray-500 (12px) - use sparingly

## Component Library

### Buttons
- **Primary CTA**: Full-width rounded-lg py-4 font-semibold text-base - positioned at bottom of screen
- **Secondary/Back**: Outlined or ghost style, smaller, positioned top-left or below primary
- **States**: Clear hover and active states with subtle transforms

### Form Elements
- **Radio/Segmented Controls**: Large touch targets (min 44px height), rounded corners, clear selected state
- **Dropdowns/Selectors**: Card-based selection with visual icons where applicable
- **Sliders**: Large thumb (24px), clear track, visible current value
- **Text Inputs**: Rounded borders, p-3 minimum, clear focus states

### Cards
- **Standard Card**: Rounded-xl border shadow-sm p-6 bg-white
- **Highlight/Takeaway Cards**: Subtle background tint, border-l-4 accent stripe
- **Collapsible/Accordion**: Clear expand/collapse indicators, smooth transitions

### Progress Indicators
- **Step Counter**: Visual dots or numbers showing current position (1/7, 2/7, etc.)
- **Progress Bar**: Linear indicator at top of screen showing completion percentage

## Content Strategy

### Key Takeaway Approach
Each screen focuses on ONE primary goal:
- **WelcomeScreen**: Establish trust and value ("360° care team")
- **ProfileGoalScreen**: Understand the user's identity and motivation
- **InjuryDetailsScreen**: Capture clinical details efficiently
- **ConstraintsScreen**: Ensure plan is realistic and achievable
- **PlanOverviewScreen**: Show high-level recovery strategy
- **PlanDetailsScreen**: Build confidence with structure and clarity
- **SummaryNextStepsScreen**: Motivate action and commitment

### Copy Guidelines
- **Titles**: Clear, action-oriented (max 6 words)
- **Subtitles**: Benefit-focused helper text (1 sentence)
- **Bullets**: Max 3 per section, start with verbs
- **CTAs**: Action verbs that indicate progress ("See My Plan", "Continue", "Start Recovery")

## Visual Elements

### Icons
- **Library**: Heroicons (outline style for most, solid for selected states)
- **Usage**: Illustrate input options (body parts, equipment types), section headers, benefits
- **Size**: w-6 h-6 for inline, w-8 h-8 for card headers, w-12 h-12 for feature icons

### Images
**Hero Image**: Not applicable for this step-based flow app - relies on clean interface and clear progression

**Illustrative Graphics**: 
- Consider simple illustrations for the "Meet Your Care Team" concept on WelcomeScreen
- Body diagram for injury selection on InjuryDetailsScreen
- Equipment icons for ConstraintsScreen

### Animations
- **Screen Transitions**: Subtle slide-in/fade (duration-200)
- **Button Interactions**: Scale on press (scale-95 active state)
- **Minimal**: Avoid distracting animations - focus on smooth, purposeful motion

## Accessibility
- **Touch Targets**: Minimum 44×44px for all interactive elements
- **Contrast**: WCAG AA minimum (4.5:1 for text)
- **Focus States**: Clear keyboard navigation indicators
- **Labels**: All form inputs with associated labels
- **Error States**: Clear validation messages with icons

## Screen-Specific Guidelines

### WelcomeScreen
- Large bold title with "Herominutes" brand name
- 3 key benefit bullets with icons
- Emphasized "360° care team" concept
- Large, prominent "Get Started" CTA

### Form Screens (Profile, Injury, Constraints)
- Progressive disclosure - one question set at a time
- Large, tappable selection options (cards or segmented controls)
- Inline validation feedback
- Clear back navigation

### Plan Screens (Overview, Details, Summary)
- Card-based layouts highlighting key information
- Use of color/borders to emphasize important takeaways
- Collapsible sections for detailed information without overwhelming
- Visual separation of phases/stages

This design system ensures a clean, professional, mobile-optimized experience that guides users confidently through their recovery plan creation while maintaining the Herominutes brand of accessible expert care.