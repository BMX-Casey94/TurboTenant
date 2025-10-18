## Initial Plan 

```
Create a modern Next.js 14 application for a blockchain-based rental security deposit management system. This integrates with TurboTenant's property management platform and uses BSV Blockchain (smart contracts) for escrow.
For future implementations, it would be wise to use MNEE (Stablecoin). 

TECH STACK:
- Next.js 14 (App Router) / Node.js / React
- TypeScript
- Tailwind CSS
- shadcn/ui components
- Recharts for analytics
- Lucide React icons

APPLICATION STRUCTURE:
Create a dual-portal application with:
1. Landlord Dashboard
2. Tenant Portal
3. Shared components for property condition documentation

COLOR SCHEME:
- Primary: Blue (#2563eb) - trust, security
- Secondary: Green (#10b981) - success, money
- Accent: Purple (#8b5cf6) - blockchain, innovation
- Background: Slate gray (#f8fafc)
- Dark mode support

PAGES NEEDED:

1. Landing Page (/)
   - Hero section explaining blockchain deposit escrow
   - Problem/solution sections
   - "Get Started as Landlord" and "Get Started as Tenant" CTAs
   - Feature showcase with icons
   - Stats section (deposits secured, average return time, etc.)

2. Landlord Dashboard (/landlord/dashboard)
   - Overview cards showing:
     * Total deposits in escrow
     * Active contracts
     * Pending reviews
     * Total properties
   - Property list with deposit status badges
   - Recent activity feed
   - Chart showing deposit trends over time
   - Quick actions: "Add Property", "Review Move-Out", "Analytics"

3. Tenant Portal (/tenant/portal)
   - Current lease card with:
     * Property image and address
     * Lease dates
     * Deposit amount
     * Landlord contact
   - Deposit status widget with blockchain transaction link
   - Move-out checklist progress bar
   - Upcoming actions timeline
   - Quick actions: "Submit Move-Out Report", "View Contract Status"

4. Property Condition Capture (/property/[id]/condition)
   - Room-by-room photo upload interface
   - Drag-and-drop area for multiple photos
   - Room selector (Living Room, Kitchen, Bedroom 1, Bathroom, etc.)
   - Photo preview grid with delete option
   - Notes field for each room
   - Progress indicator (e.g., "5/8 rooms documented")
   - Submit button that shows "Uploading to blockchain..."

5. Damage Assessment Review (/assessment/[id])
   - Split-screen photo comparison (move-in vs move-out)
   - Image slider to compare same locations
   - AI-detected damage highlights (red circles/boxes overlaid)
   - Damage list with:
     * Damage type (hole in wall, carpet stain, etc.)
     * Severity indicator
     * Estimated repair cost
     * AI confidence score
   - Cost breakdown summary
   - Total proposed deduction
   - Accept/Dispute action buttons
   - Smart contract status indicator (pending, approved, disputed)

6. Smart Contract Status (/contract/[id]/status)
   - Visual flow diagram showing contract state
   - Party approval checkboxes (landlord/tenant)
   - Transaction details:
     * Contract address
     * Deposit amount
     * Created date
     * Lease end date
     * Time remaining for auto-release
   - Fund distribution preview (who gets what)
   - Link to testnet explorer
   - Event history timeline

7. Dispute Interface (/dispute/[id])
   - Dispute reason selection
   - Evidence upload area (photos, receipts, etc.)
   - Text description field
   - Arbiter selection (third-party, community voting, or auto-release)
   - Timeline of all dispute events
   - Submit dispute button

8. Analytics Dashboard (/landlord/analytics)
   - KPI cards:
     * Average deposit return time
     * Dispute rate percentage
     * Total value in escrow
     * Properties managed
   - Charts:
     * Deposits over time (line chart)
     * Dispute reasons breakdown (pie chart)
     * Refund distribution (bar chart: 100%, 75-99%, 50-74%, <50%)
   - Export data button

COMPONENT REQUIREMENTS:

Create reusable components for:
- PropertyCard: Shows property image, address, deposit status
- DepositStatusBadge: Color-coded badges (Active, Pending Review, Disputed, Released)
- BlockchainTxLink: Shows transaction hash with copy button and explorer link
- PhotoComparisonSlider: Interactive slider to compare two images
- DamageMarker: Overlay on photos showing detected damage
- ContractStateVisual: Flow diagram of contract states
- UploadZone: Drag-and-drop file upload with preview
- TimelineItem: For activity feeds and event history
- StatCard: Dashboard metric card with icon, value, and change indicator

DESIGN PRINCIPLES:
- Modern, clean interface
- Heavy use of cards and shadows for depth
- Smooth transitions and hover effects
- Loading states for blockchain transactions
- Empty states with helpful CTAs
- Responsive (mobile-first)
- Accessibility (proper ARIA labels, keyboard navigation)

MOCK DATA STRUCTURE:

Deposit Contract:
{
  id: string
  propertyId: string
  landlordId: string
  tenantId: string
  depositAmount: number
  status: 'active' | 'pending_review' | 'disputed' | 'released'
  createdAt: timestamp
  leaseEndDate: timestamp
  moveInHashIPFS: string
  moveOutHashIPFS?: string
  proposedRefund?: number
  landlordApproved?: boolean
  tenantApproved?: boolean
  txHash: string
}

Property:
{
  id: string
  address: string
  city: string
  state: string
  zip: string
  imageUrl: string
  depositAmount: number
  contractId?: string
}

Damage Assessment:
{
  id: string
  contractId: string
  damages: Array<{
    type: string
    room: string
    severity: 'minor' | 'moderate' | 'severe'
    estimatedCost: number
    confidence: number
    imageUrls: [before, after]
  }>
  totalDeduction: number
  aiGeneratedAt: timestamp
}

START WITH:
Build the landing page and landlord dashboard first. Use placeholder data to show functionality. Include sample deposit contracts in different states (active, pending review, disputed, released) to demonstrate the full workflow.

STYLING NOTES:
- Use gradient backgrounds for hero sections
- Add subtle animations (fade-in, slide-up) for page elements
- Use shadcn/ui Alert, Card, Badge, Button, Dialog, Tabs, Progress components
- Add blockchain-themed icons (lock, shield, check-circle, alert-triangle)
- Include a subtle blockchain pattern or grid in backgrounds
```

---

## Follow-Ups

### 2: Add Tenant Portal
```
Now add the tenant portal pages. Create:

1. Tenant dashboard at /tenant/portal with:
   - Large lease details card
   - Deposit status widget showing BSV transaction
   - Move-out checklist (8 items) with checkboxes
   - Upcoming milestones timeline

2. Move-out report submission at /tenant/move-out:
   - Step-by-step wizard (3 steps)
   - Step 1: Schedule inspection date
   - Step 2: Upload photos by room
   - Step 3: Review and submit
   - Progress bar at top
   - "Save draft" functionality

Include mock data perhaps for a tenant named "Sarah Johnson" with a lease at "742 Evergreen Terrace, Springfield, IL" ending in 30 days. Show deposit amount of $1,200.
```

### 3: Property Condition Capture
```
Create the property condition capture interface at /property/[id]/condition:

- Left sidebar with room list (checkmarks for completed rooms)
- Main area with:
  * Current room title
  * Drag-and-drop photo upload zone
  * Grid of uploaded photos (max 6 per room)
  * Notes textarea
  * "Previous Room" and "Next Room" navigation
- Right sidebar showing progress (5/8 rooms complete)
- Final step: Review all photos before submitting
- Show "Generating blockchain hash..." loading state on submit
- Success modal with IPFS hash after upload

Use nice photo placeholders (via unsplash) for different rooms.
```

### 4: Damage Assessment Interface
```
Build the damage assessment review page at /assessment/[id]:

- Header showing contract details and countdown timer (7 days to respond)
- Main content in 2 columns:
  * Left: Photo comparison slider (move-in vs move-out)
  * Right: Damage details list
- Each damage item shows:
  * Red marker on photos
  * Damage type with icon
  * Room location
  * Severity badge
  * Cost with Zillow citation
  * AI confidence meter
- Bottom summary card:
  * Original deposit: $1,200
  * Total deductions: $350
  * Proposed refund: $850
- Action buttons: "Accept Assessment" (green) and "Dispute" (red)
- Modal for dispute with reason dropdown and evidence upload

Include 4 sample damages:
1. Nail holes in living room wall - $75
2. Carpet stain in bedroom - $180
3. Broken cabinet hinge - $45
4. Scuff marks on door - $50
```

### 5: Smart Contract Visualizer
```
Create the contract status page at /contract/[id]/status:

- Visual state machine showing contract lifecycle:
  * States: Created → Active → Review → Approved/Disputed → Released
  * Use connected circles with checkmarks for completed states
  * Current state highlighted
- Contract details card:
  * BSV contract address (with copy button)
  * Deposit amount in USD and BSV
  * Created date
  * Lease end date
  * Auto-release countdown (if applicable)
- Approval status:
  * Landlord approval checkbox (checked/unchecked)
  * Tenant approval checkbox (checked/unchecked)
  * Visual: both need to be checked for release
- Fund distribution preview:
  * Visual pie chart or bar showing split
  * Landlord portion
  * Tenant portion
- Transaction history timeline (blockchain events)
- "View on Testnet Explorer" button linking to whatsonchain
- Live status indicator (connected to network)

Use smooth animations for state transitions.
```

### 6: Analytics Dashboard
```
Add comprehensive analytics at /landlord/analytics:

- Date range selector (Last 7 days, 30 days, 90 days, All time)
- 4 KPI cards at top:
  * Total value in escrow (large number with BSV icon)
  * Average release time (X days)
  * Dispute rate (X%)
  * Active contracts (number)
- Charts section:
  * Line chart: Deposits over time (using Recharts)
  * Pie chart: Dispute reasons breakdown
  * Bar chart: Refund distribution percentages
  * Table: Recent transactions with export button
- Filters: Property dropdown, Status dropdown
- Export to CSV button

Use realistic mock data spanning 6 months. Show trends and patterns.
```

### 7: Dispute Resolution Interface
```
Create the dispute interface at /dispute/[id]:

- Alert banner showing "Dispute submitted on [date]"
- Dispute details card:
  * Initiated by: Landlord/Tenant
  * Reason: dropdown selection
  * Description: text area
  * Amount contested: $X
- Evidence upload section:
  * Multiple file upload (photos, PDFs, receipts)
  * Preview of uploaded evidence
  * Captions for each piece of evidence
- Arbiter selection:
  * Radio buttons: "Third-party arbiter", "Community voting", "Auto-release (7 days)"
  * Information about each option
- Timeline of dispute events:
  * Dispute opened
  * Evidence submitted
  * Arbiter assigned
  * Resolution pending
- Action buttons based on user role
- Chat interface for communication between parties

Show a sample dispute about carpet damage ($180) where tenant claims pre-existing stain.
```

### 8: Mobile Responsive Polish
```
Optimize the entire application for mobile devices:

- Hamburger menu for navigation
- Stack cards vertically on small screens
- Simplify charts for mobile (smaller legends)
- Bottom navigation for tenant portal
- Photo upload with camera access on mobile
- Swipeable photo comparison
- Collapsible sidebars
- Floating action button for primary actions
- Test all breakpoints (sm, md, lg, xl)

Ensure all interactions work well on touch devices.
```

---

## Additional Features to Request

### Optional Enhancements:

```
Add a notification system:
- Bell icon in header with badge count
- Notification dropdown with:
  * Move-out requests
  * Deposit reviews pending
  * Dispute updates
  * Contract releases
- Notification settings page
- Email/SMS preferences
```

```
Add onboarding flow:
- Welcome modal for first-time users
- Step-by-step tour of features (use a library like react-joyride or build custom)
- Setup checklist for landlords:
  * Connect BSV wallet
  * Add first property
  * Configure notification preferences
  * Review smart contract templates
```

```
Add wallet connection:
- "Connect Wallet" button in header
- Support for Yours Wallet (testnet)
- Show wallet address and BSV balance
- Transaction history from wallet
- Send/receive testnet BSV
```

---

## Design System Prompt (for Consistency)

```
Establish a design system for the application:

TYPOGRAPHY:
- Headings: font-bold with tight tracking
- Body: font-normal, text-slate-700 dark:text-slate-300
- Captions: text-sm text-slate-500

SPACING:
- Use consistent spacing scale (p-4, p-6, p-8)
- Cards have p-6 padding
- Sections have py-12 on desktop, py-8 on mobile

BUTTONS:
- Primary: bg-blue-600 hover:bg-blue-700 (for main actions)
- Secondary: bg-slate-200 hover:bg-slate-300 (for cancel)
- Success: bg-green-600 hover:bg-green-700 (for approvals)
- Danger: bg-red-600 hover:bg-red-700 (for disputes)
- All buttons: rounded-lg px-4 py-2 font-medium

CARDS:
- bg-white dark:bg-slate-800
- border border-slate-200 dark:border-slate-700
- rounded-xl
- shadow-sm hover:shadow-md transition

BADGES:
- Status indicators with dot: "● Active", "● Pending", "● Disputed"
- Rounded-full px-3 py-1 text-xs font-medium
- Color-coded by status

ICONS:
- Use Lucide React consistently
- Size: h-5 w-5 for inline icons, h-8 w-8 for feature icons
- Color matches text or use accent colors

Apply this design system across all components for visual consistency.
```

---

## Testing Scenarios to Implement

```
Add demo mode with 3 preset scenarios:

1. "Happy Path Demo"
   - Property: 123 Main St
   - Tenant: John Doe
   - Deposit: $1,500
   - Status: Move-out submitted, AI found no damage
   - Action: Accept and instant release
   - Show: Funds transfer animation

2. "Minor Damage Demo"
   - Property: 456 Oak Ave
   - Tenant: Jane Smith  
   - Deposit: $1,200
   - Status: AI detected $200 in repairs
   - Action: Both parties accept
   - Show: Partial refund ($1,000 
