# Backend Setup Guide

## Overview

The Bus Management System now includes a standalone Express.js backend that can run independently from the frontend. This guide will help you set up and run both the backend and frontend.

## Project Structure

\`\`\`
bus-management-system/
├── backend/                    # Standalone Express backend
│   ├── db/
│   │   ├── database.js        # Database operations
│   │   └── data.json          # Data persistence file
│   ├── routes/                # API route handlers
│   │   ├── auth.js
│   │   ├── buses.js
│   │   ├── routes.js
│   │   ├── schedules.js
│   │   ├── bookings.js
│   │   ├── drivers.js
│   │   └── maintenance.js
│   ├── server.js              # Express server setup
│   ├── package.json           # Backend dependencies
│   ├── .env                   # Backend environment variables
│   └── README.md              # Backend documentation
├── app/                       # Next.js frontend
├── lib/
│   ├── api-config.ts          # API endpoint configuration
│   ├── api-client-v2.ts       # Updated API client
│   └── ...
├── .env.local                 # Frontend environment variables
└── ...
\`\`\`

## Quick Start

### Step 1: Start the Backend

1. Open a terminal and navigate to the backend folder:
   \`\`\`bash
   cd backend
   \`\`\`

2. Install dependencies:
   \`\`\`bash
   npm install
   \`\`\`

3. Start the backend server:
   \`\`\`bash
   npm run dev
   \`\`\`

   You should see:
   \`\`\`
   Bus Management System Backend running on http://localhost:5000
   \`\`\`

### Step 2: Start the Frontend

1. Open a new terminal in the project root directory

2. Install frontend dependencies (if not already done):
   \`\`\`bash
   npm install
   \`\`\`

3. Start the frontend development server:
   \`\`\`bash
   npm run dev
   \`\`\`

   You should see:
   \`\`\`
   ▲ Next.js 15.x.x
   - Local:        http://localhost:3000
   \`\`\`

4. Open your browser and go to `http://localhost:3000`

## Configuration

### Frontend Configuration

The frontend is configured to connect to the backend via the `.env.local` file:

\`\`\`env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
\`\`\`

For production, update this to your deployed backend URL:

\`\`\`env
NEXT_PUBLIC_API_URL=https://your-backend-domain.com/api
\`\`\`

### Backend Configuration

The backend configuration is in `backend/.env`:

\`\`\`env
PORT=5000
NODE_ENV=development
\`\`\`

For production, change to:

\`\`\`env
PORT=5000
NODE_ENV=production
\`\`\`

## API Endpoints

All API endpoints are available at `http://localhost:5000/api/`

### Authentication
- `POST /auth/signup` - Register new user
- `POST /auth/login` - Login user
- `GET /auth/:id` - Get user details

### Buses
- `GET /buses` - Get all buses
- `POST /buses` - Create bus
- `PUT /buses/:id` - Update bus
- `DELETE /buses/:id` - Delete bus

### Routes
- `GET /routes` - Get all routes
- `POST /routes` - Create route
- `PUT /routes/:id` - Update route
- `DELETE /routes/:id` - Delete route

### Schedules
- `GET /schedules` - Get all schedules
- `POST /schedules` - Create schedule
- `PUT /schedules/:id` - Update schedule

### Bookings
- `GET /bookings` - Get all bookings
- `POST /bookings` - Create booking
- `DELETE /bookings/:id` - Cancel booking

### Drivers
- `GET /drivers` - Get all drivers
- `POST /drivers` - Create driver
- `PUT /drivers/:id` - Update driver

### Maintenance
- `GET /maintenance` - Get all maintenance records
- `POST /maintenance` - Create maintenance record
- `PUT /maintenance/:id` - Update maintenance record

## Testing the Backend

### Using cURL

Test if backend is running:
\`\`\`bash
curl http://localhost:5000/api/health
\`\`\`

Sign up a new user:
\`\`\`bash
curl -X POST http://localhost:5000/api/auth/signup \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "password123",
    "name": "Test User",
    "role": "passenger",
    "phone": "1234567890"
  }'
\`\`\`

Get all buses:
\`\`\`bash
curl http://localhost:5000/api/buses
\`\`\`

### Using Postman

1. Import the API endpoints into Postman
2. Set the base URL to `http://localhost:5000/api`
3. Test each endpoint

## Troubleshooting

### Backend won't start
- Check if port 5000 is already in use
- Try changing the PORT in `backend/.env`
- Make sure Node.js is installed: `node --version`

### Frontend can't connect to backend
- Verify backend is running on `http://localhost:5000`
- Check `.env.local` has correct `NEXT_PUBLIC_API_URL`
- Check browser console for CORS errors
- Restart both frontend and backend

### Data not persisting
- Check `backend/db/data.json` exists
- Verify write permissions in the backend folder
- Restart the backend server

### Port already in use
- Backend: Change PORT in `backend/.env`
- Frontend: Run `npm run dev -- -p 3001`

## Deployment

### Deploy Backend

The backend can be deployed to services like:
- Heroku
- Railway
- Render
- AWS EC2
- DigitalOcean

Example for Heroku:
\`\`\`bash
cd backend
heroku create your-app-name
git push heroku main
\`\`\`

### Deploy Frontend

The frontend can be deployed to:
- Vercel (recommended for Next.js)
- Netlify
- AWS Amplify

Example for Vercel:
\`\`\`bash
npm install -g vercel
vercel
\`\`\`

After deployment, update `.env.local` with your backend URL.

## Support

For issues or questions:
1. Check the backend README: `backend/README.md`
2. Check the API documentation in the backend
3. Review error messages in browser console and backend logs
