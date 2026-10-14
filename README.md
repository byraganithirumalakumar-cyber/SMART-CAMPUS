# 🎓 Smart Campus Lost & Found

> A modern, secure, responsive web platform designed for college campuses to help students report lost items, register found belongings, securely verify claims, and coordinate safe handovers.

Built for college hackathons, presentation judging, and real-world campus deployment.

---

## 🌟 Key Features

1. **Dual Lost & Found Reporting**
   - Report lost items with category, description, last-seen campus location, date, and photo.
   - Report found belongings turned in to campus centers or found across campus areas.
   - Client-side image validation (format and size limits) with instant preview.

2. **Smart Campus Search & Multi-Filter Registry**
   - Real-time instant search across titles, descriptions, and locations.
   - Filter by report type (*Lost* vs *Found*), category, campus building, and status (*Open*, *Pending Review*, *Resolved*).
   - Sort by newest or oldest reports.

3. **Confidential Ownership Verification (Claims Workflow)**
   - Claimants provide private proof only the real owner would know (e.g. lock screen wallpaper, serial suffix, unique scratches, contents).
   - Identifying details remain strictly confidential and are never exposed publicly.
   - Item reporters review, approve, or reject claims from their dashboard.

4. **Student & Security Dashboard**
   - Overview stats: Active Lost Reports, Found Reports, Incoming Claims, and Submitted Claims.
   - Review incoming claims with 1-click Approve or Reject.
   - Mark belongings as resolved/returned upon successful handover.

5. **Campus Safety First**
   - Recommends verified campus meeting zones (Main Security Gate, Student Help Desk, Library Circulation Counter).
   - Zero exposure of personal email addresses or phone numbers.
   - Clear warnings against sharing sensitive passwords or paying upfront fees.

6. **Hackathon Demo & Cloud Dual Engine**
   - **Out-of-the-box Demo Mode:** Works immediately with rich campus seed data and localStorage state even before configuring Supabase credentials. Includes 1-click Quick Test Login for judges and evaluators.
   - **Cloud Production Ready:** Connects seamlessly to Supabase PostgreSQL, Supabase Auth, and Supabase Storage bucket `item-images` once keys are provided.

---

## 🛠️ Technology Stack

- **Frontend:** React 18 with Vite
- **Styling:** Tailwind CSS with custom navy & teal campus palette
- **Icons:** Lucide React
- **Routing:** React Router v6
- **Backend & Database:** Supabase (PostgreSQL with Row Level Security)
- **Authentication:** Supabase Auth (Email & Password + Session persistence)
- **Object Storage:** Supabase Storage (`item-images` bucket)
- **Deployment Platform:** Vercel / Netlify

---

## 📁 Project Structure

```text
smart-campus-lost-and-found/
├── src/
│   ├── components/
│   │   ├── Navbar.jsx          # Header with logo, auth status & mobile menu
│   │   ├── Footer.jsx          # Campus safe zones, emergency links & credits
│   │   ├── ItemCard.jsx        # Rounded card with badges & image fallback
│   │   ├── ClaimModal.jsx      # Private claim submission popup
│   │   ├── StatusBadge.jsx     # Open / Pending / Resolved badges
│   │   └── CategoryBadge.jsx   # Category badges with Lucide icons
│   ├── pages/
│   │   ├── Home.jsx            # Hero, quick search, categories, recent items
│   │   ├── Browse.jsx          # Search registry with multi-dimension filters
│   │   ├── ReportItem.jsx      # Form with photo preview and validation
│   │   ├── ItemDetails.jsx     # Full view with confidential claim trigger
│   │   ├── Auth.jsx            # Sign In / Register + 1-click demo login
│   │   └── Dashboard.jsx       # Reports manager & claim approval center
│   ├── context/
│   │   ├── AuthContext.jsx     # Supabase Auth + local demo user state
│   │   └── ItemContext.jsx     # Supabase DB queries + localStorage fallback
│   ├── lib/
│   │   ├── supabase.js         # Supabase client & image upload helper
│   │   ├── constants.js        # Campus buildings, categories, safe zones
│   │   └── demoData.js         # Realistic campus seed data
│   ├── styles/
│   │   └── index.css           # Tailwind layers and custom styling
│   ├── App.jsx                 # Routing configuration
│   └── main.jsx                # Application root
├── supabase/
│   ├── schema.sql              # PostgreSQL tables, RLS policies & triggers
│   └── seed.sql                # Optional fictional demo items
├── .env.example                # Template environment variables
├── .env                        # Local environment variables
├── vite.config.js              # Vite build configuration
├── tailwind.config.js          # Tailwind styling configuration
└── package.json                # Project dependencies
```

---

## 🚀 Quick Start (Local Setup)

### Prerequisites
- Node.js (v18 or higher recommended; v20 LTS included)
- npm (v9 or higher)

### 1. Navigate to Project
```bash
cd "c:\Users\THIRUMALA KUMAR B\OneDrive\Desktop\smart-campus-lost-and-found"
```

### 2. Start the Development Server
```bash
npm run dev
```
Open [http://localhost:5173](http://localhost:5173) in your browser. The application will launch immediately in **Hackathon Demo Mode** with realistic sample items!

---

## 🗄️ Supabase Cloud Configuration (Optional for Production)

To connect the application to your live Supabase cloud database:

### 1. Create a Free Supabase Project
1. Go to [supabase.com](https://supabase.com) and click **Start your project**.
2. Create a new organization and project (e.g. `smart-campus-lost-found`).
3. Set a strong database password and choose your nearest region.

### 2. Run the Database Schema
1. In your Supabase Dashboard, open the **SQL Editor** tab on the left sidebar.
2. Open the file `supabase/schema.sql` from this repository.
3. Paste the entire SQL script into the SQL Editor and click **Run**.
   - This creates `public.profiles`, `public.items`, `public.claims`, auto-timestamp triggers, user creation triggers, and all Row Level Security (RLS) policies.
   - It also creates the `item-images` public storage bucket.

### 3. Retrieve API Keys
1. Go to **Project Settings** -> **API**.
2. Copy your:
   - **Project URL** (e.g. `https://xyzproject.supabase.co`)
   - **anon / public key** (e.g. `eyJhbGci...`)

### 4. Update `.env`
Edit the `.env` file in the root folder:
```env
VITE_SUPABASE_URL=https://your-project-id.supabase.co
VITE_SUPABASE_ANON_KEY=your-actual-anon-public-key
VITE_CAMPUS_NAME=Greenwood University
```

Restart your Vite dev server (`npm run dev`). The application will automatically detect your live Supabase database and transition from Demo Mode to Live Cloud Mode!

---

## 🔒 Security & Privacy Protections

- **Database-Level Row Level Security (RLS):**
  - Public items can be read by any visitor for open campus discovery.
  - Only authenticated students can create new reports and claims.
  - Reports can only be updated or deleted by their verified original author.
  - **Private Claims Isolation:** Claims and secret identifying details can **only** be read by the claimant and the original item reporter. Public visitors cannot query other people's claim explanations.
- **Client Security:**
  - Never exposes Supabase service-role keys.
  - Masks emails and phone numbers from public card listings.
  - Enforces 5MB client-side image limits and strictly verifies file MIME types.

---

## 🚢 Production Build & Deployment

### Build for Production
```bash
npm run build
```
This produces an optimized, minified production build in the `dist/` directory.

### Deploy to Vercel
1. Install Vercel CLI: `npm i -g vercel` (or connect your GitHub repo via [vercel.com](https://vercel.com)).
2. Run:
   ```bash
   vercel
   ```
3. Set the Environment Variables in the Vercel dashboard:
   - `VITE_SUPABASE_URL`
   - `VITE_SUPABASE_ANON_KEY`
   - `VITE_CAMPUS_NAME`

---

## 📋 Hackathon Demonstration Checklist

When presenting to judges:
1. **Homepage:** Show the sleek campus hero, live stats counter, and category exploration.
2. **Search & Filter:** Search for "AirPods" or filter by "Bags & Bottles" to show instant search.
3. **1-Click Quick Login:** Click **"Quick Test Login"** on the top banner to sign in instantly as a demo student.
4. **Report an Item:** Report a found item, upload a photo with live preview, and submit.
5. **Ownership Claim:** Open an item and submit a private claim with secret identifying proof.
6. **Dashboard & Approval:** Navigate to Dashboard -> **Incoming Claims**, review the claimant's private message, and click **"Approve & Coordinate Handover"** to show real-time status resolution!
