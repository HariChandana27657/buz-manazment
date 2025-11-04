# Bus Management System - Complete Installation Guide

## System Requirements

- Node.js v14 or higher
- npm v6 or higher
- Git (optional, for cloning)
- A code editor (VS Code recommended)

## Project Overview

The Bus Management System consists of two main components:

1. **Frontend**: React/Next.js application (runs on port 3000)
2. **Backend**: Express.js API server (runs on port 5000)

Both can run independently or together.

## Installation Steps

### Step 1: Extract the Project

1. Download the project ZIP file
2. Extract it to your desired location
3. You should see a folder structure like:
   \`\`\`
   bus-management-system/
   ├── backend/
   ├── app/
   ├── components/
   ├── lib/
   ├── package.json
   └── ...
   \`\`\`

### Step 2: Install Backend Dependencies

1. Open a terminal/command prompt
2. Navigate to the backend folder:
   \`\`\`bash
   cd backend
   \`\`\`

3. Install dependencies:
   \`\`\`bash
   npm install
   \`\`\`

   This will install:
   - express (web framework)
   - cors (cross-origin requests)
   - dotenv (environment variables)
   - uuid (unique IDs)

### Step 3: Install Frontend Dependencies

1. Open a new terminal in the project root (not in backend folder)
2. Install dependencies:
   \`\`\`bash
   npm install
   \`\`\`

   This will install all React, Next.js, and UI dependencies.

### Step 4: Configure Environment Variables

#### Backend Configuration

1. Navigate to `backend/.env`
2. Verify the configuration:
   \`\`\`env
   PORT=5000
   NODE_ENV=development
   \`\`\`

3. If port 5000 is already in use, change it to another port (e.g., 5001)

#### Frontend Configuration

1. Check `.env.local` in the project root
2. Verify the backend URL:
   \`\`\`env
   NEXT_PUBLIC_API_URL=http://localhost:5000/api
   \`\`\`

3. If you changed the backend port, update this accordingly

## Running the System

### Option 1: Run Both Backend and Frontend

#### Terminal 1 - Start Backend

\`\`\`bash
cd backend
npm run dev
\`\`\`

You should see:
\`\`\`
Bus Management System Backend running on http://localhost:5000
\`\`\`

#### Terminal 2 - Start Frontend

\`\`\`bash
npm run dev
\`\`\`

You should see:
\`\`\`
▲ Next.js 15.x.x
- Local:        http://localhost:3000
\`\`\`

#### Open in Browser

Go to: `http://localhost:3000`

### Option 2: Run Only Frontend (with mock data)

If you don't want to run the backend, the frontend will use mock data:

\`\`\`bash
npm run dev
\`\`\`

Go to: `http://localhost:3000`

### Option 3: Run Only Backend

If you want to test the API:

\`\`\`bash
cd backend
npm run dev
\`\`\`

Test with curl:
\`\`\`bash
curl http://localhost:5000/api/health
\`\`\`

## First Time Setup

### Default Test Accounts

The system comes with pre-configured test accounts:

**Passenger Account:**
- Email: passenger@example.com
- Password: password123
- Role: Passenger

**Driver Account:**
- Email: driver@example.com
- Password: password123
- Role: Driver

**Admin Account:**
- Email: admin@example.com
- Password: password123
- Role: Admin

### Testing the System

1. Go to `http://localhost:3000`
2. Click "Login" or "Sign Up"
3. Use one of the test accounts above
4. Explore the features:
   - **Passenger**: Book buses, view QR passes, manage bookings
   - **Driver**: View assigned routes, passenger lists, trip details
   - **Admin**: Manage buses, routes, drivers, maintenance records

## Stopping the Servers

### Stop Backend
In the backend terminal, press: `Ctrl + C`

### Stop Frontend
In the frontend terminal, press: `Ctrl + C`

## Troubleshooting

### Issue: "npm: command not found"

**Solution**: Install Node.js from https://nodejs.org/
- Download the LTS version
- Run the installer
- Restart your terminal
- Verify: `node --version`

### Issue: "Port 5000 already in use"

**Solution**: Change the backend port

1. Edit `backend/.env`:
   \`\`\`env
   PORT=5001
   \`\`\`

2. Update `.env.local`:
   \`\`\`env
   NEXT_PUBLIC_API_URL=http://localhost:5001/api
   \`\`\`

3. Restart both servers

### Issue: "Port 3000 already in use"

**Solution**: Run frontend on different port

\`\`\`bash
npm run dev -- -p 3001
\`\`\`

Then go to: `http://localhost:3001`

### Issue: Frontend can't connect to backend

**Checklist:**
- [ ] Backend is running on port 5000
- [ ] `.env.local` has correct `NEXT_PUBLIC_API_URL`
- [ ] No firewall blocking port 5000
- [ ] Check browser console (F12) for errors

### Issue: "Cannot find module" error

**Solution**: Reinstall dependencies

\`\`\`bash
# For backend
cd backend
rm -rf node_modules package-lock.json
npm install

# For frontend
cd ..
rm -rf node_modules package-lock.json
npm install
\`\`\`

### Issue: Data not saving

**Solution**: Check backend database

1. Verify `backend/db/data.json` exists
2. Check folder permissions
3. Restart backend server

## Next Steps

1. **Explore the Code**: Open files in VS Code to understand the structure
2. **Customize**: Modify colors, text, and features as needed
3. **Add Features**: Extend the system with new functionality
4. **Deploy**: When ready, deploy to production

## Deployment

### Deploy Backend

Popular options:
- Heroku (free tier available)
- Railway
- Render
- AWS
- DigitalOcean

### Deploy Frontend

Popular options:
- Vercel (recommended for Next.js)
- Netlify
- AWS Amplify

See `BACKEND_SETUP.md` for detailed deployment instructions.

## Getting Help

1. Check the README files in each folder
2. Review error messages in terminal
3. Check browser console (F12) for frontend errors
4. Verify all ports are correct
5. Ensure both servers are running

## File Structure

\`\`\`
bus-management-system/
├── backend/                    # Express backend
│   ├── db/
│   │   ├── database.js        # Database operations
│   │   └── data.json          # Data storage
│   ├── routes/                # API endpoints
│   ├── server.js              # Main server file
│   ├── package.json
│   ├── .env
│   └── README.md
├── app/                       # Next.js pages
│   ├── page.tsx              # Home page
│   ├── login/page.tsx        # Login page
│   ├── signup/page.tsx       # Sign up page
│   ├── booking/page.tsx      # Booking system
│   ├── driver/page.tsx       # Driver dashboard
│   ├── admin/                # Admin pages
│   └── layout.tsx            # Main layout
├── components/               # React components
├── lib/                      # Utilities
│   ├── api-config.ts         # API configuration
│   ├── api-client-v2.ts      # API client
│   └── auth-context.tsx      # Auth state
├── .env.local                # Frontend config
├── package.json              # Frontend dependencies
└── README.md                 # Project README
\`\`\`

## Support

For detailed information:
- Backend: See `backend/README.md`
- Setup: See `BACKEND_SETUP.md`
- Frontend: See `README.md`
