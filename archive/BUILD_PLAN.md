# BuildPhase

## Product Overview
Google review-powered provider directory organized by building/renovation phases — residential & commercial

## Tech Stack
- **Frontend**: Next.js 14 + TypeScript + Tailwind CSS
- **Backend**: Next.js API Routes
- **Database**: PostgreSQL
- **Search**: Algolia or Meilisearch
- **Maps**: Google Maps API
- **Reviews**: Google Places API integration
- **Caching**: Redis (for Google API rate limits)
- **Hosting**: Vercel

## Core Features

### 1. Phase-Based Directory
- Residential build phases (11 phases)
- Commercial build phases (adds fire, elevator, etc.)
- Phase navigation UI (timeline style)
- Provider filtering by phase + location + rating

### 2. Provider Profiles
- Google review sync (auto-updating)
- Star rating + review count
- Service areas (geo-based)
- Phase badges (which phases they cover)
- Portfolio photos
- Contact/quote request

### 3. Customer Journey
- Project type selector (residential/commercial)
- Phase guide with explanations
- "I'm in this phase, who do I need?" recommendations
- Save/bookmark providers
- Get multiple quotes feature

### 4. Provider Dashboard
- Claim profile flow
- Review analytics
- Lead notifications
- Profile optimization tips
- Competitor comparison

## Database Schema

```sql
-- Providers
providers: id, name, google_place_id, rating, review_count, phone, website, address, lat, lng, created_at

-- Provider Phases
provider_phases: id, provider_id, phase_id, is_featured

-- Phases
phases: id, name, category (residential/commercial), order_index, description

-- Locations
locations: id, city, state, zip, lat, lng

-- Customer Projects
customer_projects: id, customer_email, project_type, current_phase_id, location_id, created_at

-- Saved Providers
saved_providers: id, customer_project_id, provider_id, saved_at

-- Quote Requests
quote_requests: id, customer_project_id, provider_id, description, status, created_at

-- Review Sync
review_syncs: id, provider_id, google_reviews_json, synced_at
```

## API Endpoints

```
GET    /api/phases
GET    /api/providers?phase=X&location=Y
GET    /api/providers/:id
POST   /api/providers/:id/claim
GET    /api/providers/:id/reviews
POST   /api/quote-requests
GET    /api/search
POST   /api/sync-reviews (cron job)
```

## MVP Milestones

### Phase 1: Directory Core (Week 1-2)
- [ ] Phase taxonomy setup
- [ ] Provider profile pages
- [ ] Google review integration
- [ ] Search by location + phase

### Phase 2: Customer Features (Week 3-4)
- [ ] Project wizard
- [ ] Provider comparison
- [ ] Quote request system
- [ ] Save/bookmark

### Phase 3: Provider Features (Week 5)
- [ ] Claim profile flow
- [ ] Lead dashboard
- [ ] Profile analytics
- [ ] Upgrade to featured listing

### Phase 4: Scale (Week 6)
- [ ] Programmatic SEO pages
- [ ] City/phase landing pages
- [ ] Review sync automation
- [ ] Paid tier checkout

## Pricing Tiers (Provider Side)
- **Free**: Basic listing, Google reviews, contact form
- **Pro**: $49/mo — Featured placement, lead notifications, analytics
- **Business**: $99/mo — Priority placement, review generation tools, competitor insights

## Marketing Flywheel → Services
- "Your Google rating is 3.2 — let us run a review generation campaign"
- "You're getting profile views but no leads — let us optimize and run local ads"
- "Your competitors outrank you — let us manage your Google Business Profile"
