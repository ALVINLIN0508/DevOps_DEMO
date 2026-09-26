<a id="readme-top"></a>

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/ALVINLIN0508/rakkaranta">
   
  </a>

<h3 align="center">Rakkaranta Frontend - Code Documentation</h3>

  <p align="center">
    Complete guide to the Rakkaranta vacation rental frontend codebase
    <br />
    <a href="https://github.com/ALVINLIN0508/rakkaranta"><strong>View Repository »</strong></a>
  </p>
</div>

---

<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#project-overview">Project Overview</a></li>
    <li><a href="#tech-stack">Tech Stack</a></li>
    <li>
      <a href="#project-structure">Project Structure</a>
      <ul>
        <li><a href="#directory-layout">Directory Layout</a></li>
        <li><a href="#core-directories">Core Directories Explained</a></li>
      </ul>
    </li>
    <li>
      <a href="#core-components">Core Components</a>
      <ul>
        <li><a href="#shared-components">Shared Components</a></li>
        <li><a href="#guest-components">Guest Components</a></li>
      </ul>
    </li>
    <li>
      <a href="#pages">Pages</a>
      <ul>
        <li><a href="#public-pages">Public Pages</a></li>
        <li><a href="#authentication-pages">Authentication Pages</a></li>
        <li><a href="#booking-pages">Booking Pages</a></li>
        <li><a href="#admin-pages">Admin Pages</a></li>
      </ul>
    </li>
    <li>
      <a href="#services">Services & API</a>
      <ul>
        <li><a href="#api-client">API Client</a></li>
        <li><a href="#service-functions">Service Functions</a></li>
      </ul>
    </li>
    <li>
      <a href="#context-and-state-management">Context & State Management</a>
      <ul>
        <li><a href="#auth-context">AuthContext</a></li>
      </ul>
    </li>
    <li>
      <a href="#setup-and-installation">Setup & Installation</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation-steps">Installation Steps</a></li>
      </ul>
    </li>
    <li>
      <a href="#running-the-project">Running the Project</a>
      <ul>
        <li><a href="#development-mode">Development Mode</a></li>
        <li><a href="#production-build">Production Build</a></li>
      </ul>
    </li>
    <li><a href="#key-features">Key Features</a></li>
    <li><a href="#architecture-and-flow">Architecture & Data Flow</a></li>
    <li><a href="#coding-conventions">Coding Conventions</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>

---

## Project Overview

**Rakkaranta** is a modern vacation rental booking system for a 4-cabin resort located in Ukkohalla, Hyrynsalmi, Finland. The frontend provides a user-friendly interface for:

- **Guest Users**: Browse cabins, view amenities, select dates, and complete reservations with PIN-based check-in
- **Admin Users**: Manage bookings, view all reservations, and handle guest services

The system features advanced date conflict detection, email PIN delivery, and a responsive design optimized for both desktop and mobile devices.

**Cabins**:

- Cabin A: Lentäjän Poika 1 (27 m², 2+2 guests)
- Cabin B: Lentäjän Poika 2 (27 m², 2+2 guests)
- Cabin C: Henry Ford Cabin
- Cabin D: Beach House

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Tech Stack

- **Frontend Framework**: React 18.x
- **Build Tool**: Vite (fast development server and optimized builds)
- **Styling**: Tailwind CSS (utility-first CSS framework)
- **Routing**: React Router v6 (client-side routing with programmatic navigation)
- **State Management**: React Hooks (useState, useEffect, useRef, useContext)
- **HTTP Client**: Fetch API (modern async/await pattern)
- **CSS Processing**: PostCSS with Tailwind plugins

**Dependencies** (from `frontend/package.json`):

- react: ^18.x
- react-dom: ^18.x
- react-router-dom: ^6.x
- vite: Latest
- tailwindcss: Latest
- postcss: Latest

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Project Structure

### Directory Layout

```
frontend/
├── public/                          # Static assets
│   └── [cabin images and logos]
├── src/
│   ├── components/                  # Reusable React components
│   │   ├── guest/                   # Guest-specific components
│   │   │   └── PINLoginForm.jsx
│   │   ├── public/                  # Public page components
│   │   │   └── home page.html
│   │   └── shared/                  # Shared utility components
│   │       ├── CalendarDatePicker.jsx
│   │       ├── DatePickerCalendar.jsx
│   │       └── ProtectedRoute.jsx
│   ├── pages/                       # Page components (routes)
│   │   ├── HomePage.jsx
│   │   ├── AdminDashboardPage.jsx
│   │   ├── AdminLoginPage.jsx
│   │   ├── GuestLoginPage.jsx
│   │   ├── GuestDashboardPage.jsx
│   │   ├── GuestServicesPage.jsx
│   │   ├── NotFoundPage.jsx
│   │   ├── A_Lentäjän_poika1.jsx
│   │   ├── B_LentäjänPoika2.jsx
│   │   ├── C_HenryFordCabin.jsx
│   │   ├── D_BeachHouse.jsx
│   │   ├── A_reservation.jsx
│   │   ├── B_reservation.jsx
│   │   ├── C_reservation.jsx
│   │   ├── D_reservation.jsx
│   │   ├── Yhteiset_Tilat.jsx
│   │   └── [other page components]
│   ├── services/                    # API client and service functions
│   │   ├── apiClient.js
│   │   └── index.js
│   ├── context/                     # React Context for state management
│   │   └── AuthContext.jsx
│   ├── App.jsx                      # Main app component with routing
│   ├── main.jsx                     # Entry point
│   └── index.css                    # Global styles
├── package.json                     # Dependencies
├── vite.config.js                   # Vite configuration
├── tailwind.config.js               # Tailwind CSS configuration
├── postcss.config.js                # PostCSS configuration
└── README.md                        # Project readme
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Core Directories Explained

#### `/components`

Reusable React components used across multiple pages:

- **`/shared`**: Common components shared by multiple pages
  - `DatePickerCalendar.jsx`: Interactive calendar component for selecting dates. Shows booked dates as disabled/grayed out. Accepts props: `value` (current date), `onChange` (callback), `min` (minimum selectable date), `isDateBooked` (function to check if date is booked)
  - `ProtectedRoute.jsx`: Wrapper component that checks authentication status before rendering protected pages. Redirects unauthenticated users to login

- **`/guest`**: Components specific to guest functionality
  - `PINLoginForm.jsx`: Form for guests to enter their PIN code for check-in verification

- **`/public`**: Static/public-facing components
  - `home page.html`: Legacy home page HTML (being phased out)

#### `/pages`

Page-level components that represent different routes in the application:

- **Cabin Detail Pages**: Display cabin information, amenities, and images
  - `A_Lentäjän_poika1.jsx`, `B_LentäjänPoika2.jsx`, `C_HenryFordCabin.jsx`, `D_BeachHouse.jsx`: Each cabin has a dedicated detail page with photo gallery, amenities list, and "Book Now" button
  - `Yhteiset_Tilat.jsx`: Shared facilities page

- **Reservation Pages**: Booking interface for each cabin
  - `A_reservation.jsx`, `B_reservation.jsx`, `C_reservation.jsx`, `D_reservation.jsx`: Booking forms with date selection, email input, and PIN generation

- **Authentication Pages**:
  - `AdminLoginPage.jsx`: Admin login interface
  - `GuestLoginPage.jsx`: Guest login interface (PIN verification)

- **Dashboard Pages**:
  - `AdminDashboardPage.jsx`: Admin panel for managing bookings and viewing all reservations
  - `GuestDashboardPage.jsx`: Guest dashboard (TBD)
  - `GuestServicesPage.jsx`: Additional services booking (wellness treatments, EV charging, etc.)

- **Core Pages**:
  - `HomePage.jsx`: Landing page with navigation and cabin showcase
  - `NotFoundPage.jsx`: 404 error page

#### `/services`

API communication and utility functions:

- `apiClient.js`: Configured Fetch API client for backend communication
- `index.js`: Exported service functions for common API calls

#### `/context`

React Context for global state management:

- `AuthContext.jsx`: Manages authentication state (user info, login/logout), prevents prop drilling across deep component trees

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Core Components

### Shared Components

#### DatePickerCalendar.jsx

**Purpose**: Renders an interactive calendar UI for date selection with visual feedback for booked dates.

**Props**:

- `value` (string): Current selected date in YYYY-MM-DD format
- `onChange` (function): Callback fired when a date is selected, receives the new date string
- `min` (string): Minimum selectable date (prevents selecting past dates)
- `isDateBooked` (function): Function that takes a dateStr and returns boolean if date is booked

**Key Features**:

- Month navigation with previous/next buttons
- Day buttons with conditional styling (booked dates appear gray and disabled)
- Prevents selection of booked dates and past dates
- Auto-closes calendar after selection

**Example Usage**:

```jsx
<DatePickerCalendar
  value={selectedDate}
  onChange={(newDate) => setSelectedDate(newDate)}
  min={todayString}
  isDateBooked={(dateStr) => checkIfDateBooked(dateStr)}
/>
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

#### ProtectedRoute.jsx

**Purpose**: Higher-order component that protects routes from unauthorized access.

**Functionality**:

- Checks authentication status from AuthContext
- Redirects unauthenticated users to appropriate login page
- Renders protected component if user is authenticated

**Example Usage**:

```jsx
<Route
  path="/admin/dashboard"
  element={
    <ProtectedRoute role="admin">
      <AdminDashboardPage />
    </ProtectedRoute>
  }
/>
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Guest Components

#### PINLoginForm.jsx

**Purpose**: Guest check-in form for PIN code verification.

**Features**:

- PIN input field with masked display
- Form validation
- Error handling for invalid/expired PIN codes

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Pages

### Public Pages

#### HomePage.jsx

**Purpose**: Landing page and main entry point for the application.

**Features**:

- Navigation header with logo and menu links
- Hero section with branding
- Cabin showcase with booking buttons
- Responsive layout optimized for mobile and desktop

**Navigation Links**:

- About Us
- Contact Us
- Accommodation Benefits
- How to Reach Us

<p align="right">(<a href="#readme-top">back to top</a>)</p>

#### Cabin Detail Pages

**Files**: `A_Lentäjän_poika1.jsx`, `B_LentäjänPoika2.jsx`, `C_HenryFordCabin.jsx`, `D_BeachHouse.jsx`, `Yhteiset_Tilat.jsx`

**Purpose**: Display comprehensive cabin information with photo galleries and amenities.

**Features**:

- Photo gallery with thumbnail navigation
- Detailed cabin specifications and amenities list
- Guest access instructions
- Location and activity information
- "Book Now" button linking to reservation page
- Responsive grid layout (single column on mobile, two-column on desktop)

**Structure**:

- Left section: Cabin details and information
- Right section: Image gallery with navigation controls

**Amenities Displayed**:

- Bedroom and bathroom details
- Kitchen appliances and equipment
- Entertainment and connectivity
- Heating and climate control
- Outdoor features (terrace, grill, etc.)

**Shared Facilities Section**:

- Common areas available to all guests
- Amenities shared across the 4-cabin complex

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Authentication Pages

#### AdminLoginPage.jsx

**Purpose**: Admin authentication interface.

**Features**:

- Admin email/username input
- Password input field
- Login button with loading state
- Error message display
- Link to guest login option

<p align="right">(<a href="#readme-top">back to top</a>)</p>

#### GuestLoginPage.jsx

**Purpose**: Guest PIN code verification interface.

**Features**:

- PIN input form (typically 8-character alphanumeric code)
- Form validation
- Error handling for invalid/expired PINs
- Link to admin login
- PIN received via email after booking

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Booking Pages

**Files**: `A_reservation.jsx`, `B_reservation.jsx`, `C_reservation.jsx`, `D_reservation.jsx`

**Purpose**: Cabin-specific reservation forms for guests to book accommodations.

**Core Workflow**:

1. Guest enters email address
2. Guest selects check-in date using DatePickerCalendar
3. Guest selects check-out date using DatePickerCalendar
4. System checks for date conflicts
5. If no conflicts, system generates 8-character PIN code
6. PIN is emailed to guest
7. Guest receives confirmation

**Features**:

- Email input with validation
- Two date pickers (check-in and check-out)
- Real-time conflict detection
- Display of booked dates on calendar
- "Make a Reservation" button
- Loading states and error handling
- Success notification after PIN generation

**Key State Variables**:

```javascript
const [selectedDates, setSelectedDates] = useState({
  checkin: null,
  checkout: null,
});
const [guestEmail, setGuestEmail] = useState("");
const [bookings, setBookings] = useState([]); // All bookings to check conflicts
const [loading, setLoading] = useState(false);
const [generatingPin, setGeneratingPin] = useState(false);
```

**Conflict Prevention**:

- Frontend validation checks for overlapping dates
- Backend confirms no conflicts exist before PIN generation
- Dates are compared using ISO 8601 string format (YYYY-MM-DD)
- Allows same-day turnovers (guest checkout at noon, next guest check-in afternoon)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Admin Pages

#### AdminDashboardPage.jsx

**Purpose**: Admin control panel for managing bookings and guest information.

**Features**:

- **Booking Creation Section**:
  - Select cabin from dropdown
  - View calendar with booked dates for selected cabin
  - Select date range
  - Enter guest email
  - Generate PIN and send email
- **Bookings View**:
  - Display all active/pending bookings
  - Shows booking dates and cabin information
  - Real-time updates

- **Multi-Cabin Support**:
  - Cabin ID mapping (numeric to string format)
  - Supports both formats for compatibility

**Key Functions**:

- `isDateBooked(cabinId, dateStr)`: Checks if a date is booked for specific cabin
- `hasConflictingDates()`: Validates no overlaps in selected date range
- `autoGeneratePin()`: Main booking workflow - email validation, conflict checking, PIN generation, email sending

<p align="right">(<a href="#readme-top">back to top</a>)</p>

#### GuestDashboardPage.jsx

**Purpose**: Guest dashboard for viewing their reservation details (TBD).

**Planned Features**:

- Display current/past reservations
- Check PIN validity period
- View cabin details and access instructions
- Contact information

<p align="right">(<a href="#readme-top">back to top</a>)</p>

#### GuestServicesPage.jsx

**Purpose**: Additional services booking interface for guests.

**Services Available**:

- **Wellness Services**: Massage, spa treatments, natural product therapies
- **EV Charging**: Port selection and time slot booking
- **Other Services**: Additional activities or amenities

**Features**:

- Time slot selector for service scheduling
- Guest information display from session storage
- Service booking modal with confirmation
- Support for multiple guests per service

**Session Storage**:

- Guest information stored during check-in process
- Used to pre-fill service booking forms

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Services & API

### API Client

#### apiClient.js

**Purpose**: Centralized HTTP client for all backend API communications using Fetch API.

**Base Configuration**:

```javascript
const API_BASE_URL = "http://localhost:5000/api";
```

**Common Headers**:

- `Content-Type: application/json`
- Optional: Authentication headers (when available)

**Error Handling**:

- Validates HTTP response status
- Throws descriptive errors for failed requests
- Logs errors for debugging

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Service Functions

#### index.js

**Purpose**: Exported service functions for common API operations.

**Key API Endpoints Used**:

| Method | Endpoint                     | Purpose                              |
| ------ | ---------------------------- | ------------------------------------ |
| GET    | `/api/cabins`                | Fetch all cabins with details        |
| GET    | `/api/cabins/all-bookings`   | Get all active/pending bookings      |
| POST   | `/api/cabins/generate-pin`   | Create booking and generate PIN code |
| POST   | `/api/cabins/verify-pin`     | Verify guest PIN code validity       |
| POST   | `/api/cabins/send-pin-email` | Send PIN code via email to guest     |

**Request/Response Examples**:

**Generate PIN**:

```javascript
// Request
POST /api/cabins/generate-pin
{
  "cabin_id": 1,
  "check_in_date": "2026-06-01",
  "check_out_date": "2026-06-08",
  "number_of_days": 7,
  "guest_email": "guest@example.com"
}

// Response (Success - 201)
{
  "success": true,
  "data": {
    "booking_id": 42,
    "cabin_id": "A",
    "pin_code": "CR77Q1EE",
    "check_in_date": "2026-06-01",
    "check_out_date": "2026-06-08",
    "days": 7,
    "validity_start": "2026-06-01T04:00:00.000Z",
    "validity_end": "2026-06-08T12:00:00.000Z"
  }
}

// Response (Conflict - 409)
{
  "error": "Selected dates have conflicts with existing bookings",
  "conflicting_dates": "2026-06-05 to 2026-06-06"
}
```

**Verify PIN**:

```javascript
// Request
POST /api/cabins/verify-pin
{
  "pin_code": "CR77Q1EE"
}

// Response (Valid - 200)
{
  "success": true,
  "data": {
    "cabin_id": "A",
    "cabin_name": "Lentäjän Poika 1",
    "check_in_date": "2026-06-01",
    "check_out_date": "2026-06-08",
    "validity_start": "2026-06-01T04:00:00.000Z",
    "validity_end": "2026-06-08T12:00:00.000Z"
  }
}
```

**Send Email**:

```javascript
// Request
POST /api/cabins/send-pin-email
{
  "email": "guest@example.com",
  "pin_code": "CR77Q1EE",
  "cabin_name": "Lentäjän Poika 1"
}

// Response (Success - 200)
{
  "success": true,
  "message": "Email sent successfully",
  "data": {
    "email": "guest@example.com",
    "cabin_name": "Lentäjän Poika 1",
    "sent_at": "2026-05-29T10:30:00.000Z"
  }
}
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Context and State Management

### AuthContext.jsx

**Purpose**: Global authentication context that manages user login state across the entire application.

**Context Value**:

```javascript
{
  user: {
    id: string,
    email: string,
    role: 'admin' | 'guest',
    loginTime: timestamp
  },
  isAuthenticated: boolean,
  login: (email, role) => Promise,
  logout: () => void
}
```

**Key Features**:

- Stores user information globally to avoid prop drilling
- Provides login/logout functions
- Persists authentication state (typically in localStorage)
- Used by ProtectedRoute to check access permissions

**Usage Example**:

```javascript
import { useAuth } from "../context/AuthContext";

function MyComponent() {
  const { user, logout, isAuthenticated } = useAuth();

  if (!isAuthenticated) {
    return <Navigate to="/login" />;
  }

  return <div>Welcome, {user.email}</div>;
}
```

**State Persistence**:

- User data stored in browser localStorage
- Automatically restored on page refresh
- Cleared on logout

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Setup and Installation

### Prerequisites

- **Node.js**: v16.x or higher
- **npm**: v7.x or higher (comes with Node.js)
- **Backend Server**: Running on `http://localhost:5000` (see backend documentation)
- **Git**: For cloning the repository
- **Code Editor**: VS Code recommended

**Verify Installation**:

```bash
node --version    # Should show v16.x or higher
npm --version     # Should show v7.x or higher
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Installation Steps

**1. Clone the repository** (if not already done):

```bash
git clone https://github.com/ALVINLIN0508/rakkaranta.git
cd rakkaranta
```

**2. Navigate to frontend directory**:

```bash
cd frontend
```

**3. Install dependencies**:

```bash
npm install
```

This installs all packages listed in `package.json`:

- React 18
- React Router v6
- Tailwind CSS
- Vite
- And other utilities

**4. Configure environment** (optional):
Create a `.env.local` file in the `frontend/` directory if backend is on non-standard port:

```env
VITE_API_URL=http://localhost:5000
```

**5. Verify installation**:

```bash
npm list
# Should show all packages installed successfully
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Running the Project

### Development Mode

**Start the development server**:

```bash
npm run dev
```

**Output** (typically):

```
  VITE v4.x.x  ready in xxx ms

  ➜  Local:   http://localhost:5173/
  ➜  press h to show help
```

**Access the application**:

- Open browser to `http://localhost:5173/`
- Page automatically reloads on code changes (Hot Module Replacement)

**Development Features**:

- Fast refresh on file changes
- Source maps for easy debugging
- All warnings and errors in console
- No optimization (faster builds)

**Stopping the server**:

```bash
Ctrl + C  # Press Ctrl+C in terminal
```

**Troubleshooting**:

- Port 5173 already in use? Vite will auto-increment to next available port
- Backend not running? API calls will fail - ensure backend on port 5000

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Production Build

**Build for production**:

```bash
npm run build
```

**Process**:

1. Vite optimizes and bundles React code
2. CSS is minified and bundled
3. Output generated in `dist/` directory
4. Build process takes 10-30 seconds

**Build Output**:

```
dist/
├── index.html          # Main entry point
├── assets/
│   ├── index.XXXXX.js  # Bundled JavaScript
│   └── index.XXXXX.css # Bundled CSS
└── [other assets]
```

**Preview production build**:

```bash
npm run preview
# Runs local preview server to test production build
# Access at http://localhost:4173/
```

**Deployment**:

- Upload `dist/` folder to static hosting service
- Ensure backend API URL is correct in environment variables
- Configure CORS if backend on different domain

**Optimization Notes**:

- JavaScript is minified and tree-shaken
- CSS is purged of unused styles via Tailwind
- Assets hashed for cache busting
- Typical bundle size: 200-400KB gzipped

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Key Features

1. **Responsive Design**
   - Mobile-first approach using Tailwind CSS
   - Works seamlessly on all screen sizes (mobile, tablet, desktop)
   - Adaptive layouts with conditional rendering

2. **Advanced Date Selection**
   - Interactive calendar interface
   - Real-time booked date visualization
   - Prevents selection of past dates and conflicts
   - Same-day turnover support (checkout/check-in same day)

3. **Intelligent Conflict Detection**
   - Frontend validation prevents invalid selections
   - Backend confirms no overlaps exist
   - Shows conflicting dates when applicable

4. **Email PIN System**
   - 8-character alphanumeric PIN codes
   - HTML email templates with professional design
   - PIN validity windows (4:00 AM check-in to 12:00 PM checkout)
   - Automatic email delivery after booking

5. **Role-Based Access Control**
   - Guest and admin user types
   - Protected routes require authentication
   - Different dashboards and functionality per role

6. **Multi-Cabin Management**
   - 4 independently bookable cabins
   - Cabin-specific amenities and images
   - Photo gallery with navigation
   - Shared facilities information

7. **Real-Time Booking Management**
   - Admin view of all active bookings
   - Create bookings for guests
   - Send PIN codes on demand
   - View booking status and validity periods

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Architecture and Data Flow

**Request Flow** (Guest Booking):

```
1. Guest lands on HomePage
   ↓
2. Clicks cabin "Book Now" button
   ↓
3. Navigated to A_reservation page
   ↓
4. Enters email address
   ↓
5. Selects check-in date (DatePickerCalendar fetches booked dates)
   ↓
6. Selects check-out date
   ↓
7. Frontend validates no conflicts (hasConflictingDates)
   ↓
8. Clicks "Make a Reservation" button
   ↓
9. Frontend calls POST /api/cabins/generate-pin
   ↓
10. Backend creates booking record and generates PIN
   ↓
11. Backend calls POST /api/cabins/send-pin-email
   ↓
12. Nodemailer sends HTML email with PIN to guest
   ↓
13. Guest receives email and logs in with PIN
```

**Admin Booking Flow**:

```
1. Admin logs into AdminDashboardPage
   ↓
2. Selects cabin from dropdown
   ↓
3. Calendar shows booked dates for selected cabin
   ↓
4. Selects date range for new booking
   ↓
5. Enters guest email
   ↓
6. Clicks "Generate PIN"
   ↓
7. Same flow as guest booking from step 9
```

**Component Hierarchy**:

```
App.jsx (routing)
├── HomePage
│   ├── Navigation header
│   └── Cabin cards (links to detail pages)
├── [Cabin Detail Pages]
│   ├── Header
│   ├── Cabin info + image gallery
│   └── "Book Now" button → /[X]_reservation
├── [Reservation Pages]
│   ├── Email input
│   ├── DatePickerCalendar (check-in)
│   ├── DatePickerCalendar (check-out)
│   └── Submit button
├── AdminDashboardPage
│   ├── ProtectedRoute
│   ├── Cabin selector
│   ├── DatePickerCalendar
│   └── Booking form
└── [Other pages...]
```

**State Management**:

- **Global**: AuthContext (user, authentication)
- **Local**: Component useState hooks
- **API**: Fetch calls to backend

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Coding Conventions

**File Naming**:

- Components: PascalCase (e.g., `DatePickerCalendar.jsx`)
- Page components: PascalCase (e.g., `HomePage.jsx`, `AdminDashboardPage.jsx`)
- Utility files: camelCase (e.g., `apiClient.js`, `index.js`)
- Cabin pages: Include cabin identifier (e.g., `A_Lentäjän_poika1.jsx`)

**Component Structure**:

```jsx
// Imports
import { useState, useEffect } from "react";
import { useNavigate } from "react-router-dom";

// Component definition
export default function MyComponent() {
  // Hooks
  const [state, setState] = useState(initialValue);

  // Effects
  useEffect(() => {
    // Side effects
  }, [dependencies]);

  // Event handlers
  const handleClick = () => {};

  // Render
  return <div>{/* JSX */}</div>;
}
```

**Styling**:

- Use Tailwind CSS utility classes exclusively
- Avoid inline styles
- No external CSS files in components
- Configure custom styles in `tailwind.config.js` if needed

**Comments**:

- All code comments in English
- Use `//` for single-line comments
- Use `/* */` for multi-line comments
- Focus on "why" not "what"

**Date Handling**:

- Use ISO 8601 string format: `YYYY-MM-DD`
- Convert Date objects to strings before API calls
- Compare dates as strings to avoid timezone issues

**Error Handling**:

```jsx
try {
  const response = await fetch(url);
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  const data = await response.json();
} catch (error) {
  console.error("Error:", error);
  setError(error.message);
}
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Contributing

**Development Workflow**:

1. Create feature branch: `git checkout -b feature/cabin-name`
2. Make changes to code
3. Test thoroughly in development mode
4. Commit with descriptive message: `git commit -m 'Add feature description'`
5. Push to branch: `git push origin feature/cabin-name`
6. Create Pull Request with detailed description

**Code Review**:

- Ensure all new code has English comments
- Verify responsive design on multiple screen sizes
- Test with both admin and guest user flows
- Check for console errors/warnings

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## License

This project is licensed under the terms specified in the LICENSE file in the root directory.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Contact

**Project Repository**: [ALVINLIN0508/rakkaranta](https://github.com/ALVINLIN0508/rakkaranta)

**Rakkaranta Location**:

- Fourth Avenue 3, 89400 Hyrynsalmi, Finland
- Located next to Ukkohalla ski resort
- Phone: +358 00 123 4567
- Email: info@rakkaranta.fi

## Maintainer

This project is maintained by Alvin Lin.

GitHub: [ALVINLIN0508](https://github.com/ALVINLIN0508)
**For Backend Documentation**: See [Backend Documentation](../bk/README.md)

<p align="right">(<a href="#readme-top">back to top</a>)</p>
