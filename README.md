# Gate Pass System

A secure, full-stack residential college gate pass management system built with Next.js, React, and MongoDB.  
Students request passes, parents approve via tokenized workflows, wardens oversee, and security staff verify via QR codes.

---

## Table of Contents

- [Features](#features)  
- [Tech Stack](#tech-stack)  
- [App Flow](#app-flow)  
- [User Roles](#user-roles)  
- [Demo](#demo)  
- [Getting Started](#getting-started)  
- [Project Structure](#project-structure)  
- [Authentication & Security](#authentication--security)  
- [API Endpoints](#api-endpoints)  
- [Contributing](#contributing)  
- [License](#license)  

---

## Features

- **Role-Based Dashboards**: Student, Parent, Warden, Security  
- **Multi-Step Approval**: Sequential, tokenized parent approvals with expiration  
- **QR Code Verification**: Secure check-out/check-in by security staff  
- **Onboarding Flow**: Clerk-based sign-up with profile completion  
- **Real-Time Data**: MongoDB + Mongoose for robust persistence  
- **Responsive UI**: Tailwind CSS + shadcn/ui components  

---

## Tech Stack

- **Frontend**: Next.js 15 (App Router), React 19  
- **Styling**: Tailwind CSS 4, shadcn/ui, Radix UI  
- **Backend**: Next.js API Routes  
- **Database**: MongoDB & Mongoose  
- **Auth**: Clerk (with API keys)  
- **Forms & Validation**: React Hook Form & Zod  
- **Utilities**: QR Code generation, Date-fns

---

## App Flow

1. **Onboarding**: New users sign up via Clerk and complete their profile (role, IDs, contact info).  
2. **Routing**: Upon login, users are redirected to `/dashboard` which routes them based on role:  
   - Students → `/student`  
   - Parents → `/parent`  
   - Wardens → `/warden`  
   - Security Guards → `/security`  
3. **Student Actions**: Students create gate pass requests, view status, and access QR codes for approved passes.  
4. **Parent Approvals**: Parents receive sequential, expiring tokens to approve/reject their child’s requests.  
5. **Warden Oversight**: Wardens review all passes, manage student-parent links, and ensure policy compliance.  
6. **Security Verification**: Security guards scan QR codes to check students out/in, updating pass status.

---

## User Roles

**Student**  
- Create new gate pass requests with reason, destination, and timings.  
- View personal pass history and statuses.  
- Access and present approved pass QR codes.  

**Parent**  
- Approve or reject child’s gate pass requests using secure, time-limited tokens.  
- View list of pending and past approvals.  

**Warden**  
- View and manage all gate passes across the campus.  
- Link students to parent accounts and manage student records.  
- Provide final oversight and intervention if needed.  

**Security Guard**  
- Scan QR codes to check students out and in at exit/entry points.  
- View active and approved gate passes ready for verification.  

---

## Getting Started

### Prerequisites

- Node.js ≥ 18  
- npm or yarn  
- MongoDB connection URI  
- Clerk account with API keys  

### Installation

```bash
git clone https://github.com/akm2006/gatepass.git
cd gatepass
npm install
# or
yarn install
````

### Environment Variables

```bash
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_live_xxx
NEXT_PUBLIC_CLERK_FRONTEND_API=your-frontend-api.clerk.app
CLERK_SECRET_KEY=sk_live_yyy
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/dbname
```

### Scripts

* `npm run dev` — Development server
* `npm run build` — Production build
* `npm run start` — Production server
* `npm run lint` — Lint code

---

## Project Structure

```bash
├── app/                    # Next.js App Router 
│   ├── api/                # API routes 
│   ├── onboarding/         # Profile setup 
│   ├── dashboard/          # Role-based routing 
│   ├── student/            # Student UI 
│   ├── parent/             # Parent UI 
│   ├── warden/             # Warden UI 
│   └── security/           # Security UI 
├── components/             # Role-specific components 
├── lib/                    # Auth utilities 
├── server/                 # DB config, models, utils 
└── styles/                 # Global styles & Tailwind
```

---

## Authentication & Security

* Clerk for user authentication and middleware route protection.
* Tokenized approvals with expiration.
* QR code generation for secure physical verification.
* Role guards to enforce access at each route.

---

## API Endpoints

| Route                       | Method | Description                       |
| --------------------------- | ------ | --------------------------------- |
| `/api/gate-passes`          | GET    | Fetch passes by role              |
| `/api/gate-passes`          | POST   | Create pass (students only)       |
| `/api/gate-passes/approve`  | POST   | Parent approve/reject with token  |
| `/api/gate-passes/checkout` | POST   | Security guard checks out student |
| `/api/gate-passes/checkin`  | POST   | Security guard checks in student  |

---

## License

Distributed under the [MIT License](LICENSE).

```
