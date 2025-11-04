# Bus Management System - API Documentation

## Base URL

\`\`\`
http://localhost:5000/api
\`\`\`

For production, replace with your deployed backend URL.

## Authentication Endpoints

### Sign Up

Create a new user account.

**Endpoint:** `POST /auth/signup`

**Request Body:**
\`\`\`json
{
  "email": "user@example.com",
  "password": "password123",
  "name": "John Doe",
  "role": "passenger",
  "phone": "1234567890"
}
\`\`\`

**Role-specific fields:**
- **passenger**: phone (optional)
- **driver**: licenseNumber (required)
- **admin**: employeeId (required)

**Response:**
\`\`\`json
{
  "message": "User created successfully",
  "user": {
    "id": "uuid",
    "email": "user@example.com",
    "name": "John Doe",
    "role": "passenger",
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
\`\`\`

### Login

Authenticate a user.

**Endpoint:** `POST /auth/login`

**Request Body:**
\`\`\`json
{
  "email": "user@example.com",
  "password": "password123"
}
\`\`\`

**Response:**
\`\`\`json
{
  "message": "Login successful",
  "user": {
    "id": "uuid",
    "email": "user@example.com",
    "name": "John Doe",
    "role": "passenger"
  }
}
\`\`\`

### Get User

Get user details by ID.

**Endpoint:** `GET /auth/:id`

**Response:**
\`\`\`json
{
  "id": "uuid",
  "email": "user@example.com",
  "name": "John Doe",
  "role": "passenger"
}
\`\`\`

## Bus Endpoints

### Get All Buses

**Endpoint:** `GET /buses`

**Response:**
\`\`\`json
[
  {
    "id": "uuid",
    "busNumber": "BUS-001",
    "capacity": 50,
    "model": "Volvo B11R",
    "registrationNumber": "MH-01-AB-1234",
    "status": "active",
    "createdAt": "2024-01-01T00:00:00Z"
  }
]
\`\`\`

### Get Bus by ID

**Endpoint:** `GET /buses/:id`

**Response:**
\`\`\`json
{
  "id": "uuid",
  "busNumber": "BUS-001",
  "capacity": 50,
  "model": "Volvo B11R",
  "registrationNumber": "MH-01-AB-1234",
  "status": "active"
}
\`\`\`

### Create Bus

**Endpoint:** `POST /buses`

**Request Body:**
\`\`\`json
{
  "busNumber": "BUS-003",
  "capacity": 50,
  "model": "Volvo B11R",
  "registrationNumber": "MH-01-AB-1236",
  "status": "active"
}
\`\`\`

**Response:**
\`\`\`json
{
  "message": "Bus created successfully",
  "bus": {
    "id": "uuid",
    "busNumber": "BUS-003",
    "capacity": 50,
    "model": "Volvo B11R",
    "registrationNumber": "MH-01-AB-1236",
    "status": "active",
    "createdAt": "2024-01-01T00:00:00Z"
  }
}
\`\`\`

### Update Bus

**Endpoint:** `PUT /buses/:id`

**Request Body:**
\`\`\`json
{
  "status": "maintenance"
}
\`\`\`

### Delete Bus

**Endpoint:** `DELETE /buses/:id`

**Response:**
\`\`\`json
{
  "message": "Bus deleted successfully"
}
\`\`\`

## Route Endpoints

### Get All Routes

**Endpoint:** `GET /routes`

**Response:**
\`\`\`json
[
  {
    "id": "uuid",
    "name": "Mumbai to Pune",
    "startCity": "Mumbai",
    "endCity": "Pune",
    "distance": 150,
    "stops": ["Mumbai Central", "Lonavala", "Pune Station"],
    "estimatedDuration": 240,
    "createdAt": "2024-01-01T00:00:00Z"
  }
]
\`\`\`

### Create Route

**Endpoint:** `POST /routes`

**Request Body:**
\`\`\`json
{
  "name": "Mumbai to Bangalore",
  "startCity": "Mumbai",
  "endCity": "Bangalore",
  "distance": 850,
  "stops": ["Mumbai Central", "Aurangabad", "Hyderabad", "Bangalore"],
  "estimatedDuration": 1440
}
\`\`\`

### Update Route

**Endpoint:** `PUT /routes/:id`

### Delete Route

**Endpoint:** `DELETE /routes/:id`

## Schedule Endpoints

### Get All Schedules

**Endpoint:** `GET /schedules`

**Query Parameters:**
- `routeId` - Filter by route
- `busId` - Filter by bus

**Example:** `GET /schedules?routeId=route-1`

**Response:**
\`\`\`json
[
  {
    "id": "uuid",
    "busId": "bus-1",
    "routeId": "route-1",
    "departureTime": "08:00",
    "arrivalTime": "12:00",
    "date": "2024-01-15",
    "fare": 500,
    "availableSeats": 50,
    "createdAt": "2024-01-01T00:00:00Z"
  }
]
\`\`\`

### Create Schedule

**Endpoint:** `POST /schedules`

**Request Body:**
\`\`\`json
{
  "busId": "bus-1",
  "routeId": "route-1",
  "departureTime": "08:00",
  "arrivalTime": "12:00",
  "date": "2024-01-15",
  "fare": 500,
  "availableSeats": 50
}
\`\`\`

### Update Schedule

**Endpoint:** `PUT /schedules/:id`

## Booking Endpoints

### Get All Bookings

**Endpoint:** `GET /bookings`

**Query Parameters:**
- `userId` - Filter by user

**Example:** `GET /bookings?userId=user-1`

### Get Booking by ID

**Endpoint:** `GET /bookings/:id`

### Create Booking

**Endpoint:** `POST /bookings`

**Request Body:**
\`\`\`json
{
  "userId": "user-1",
  "scheduleId": "schedule-1",
  "seats": 2,
  "totalPrice": 1000,
  "passengerName": "John Doe",
  "passengerPhone": "1234567890"
}
\`\`\`

**Response:**
\`\`\`json
{
  "message": "Booking created successfully",
  "booking": {
    "id": "uuid",
    "userId": "user-1",
    "scheduleId": "schedule-1",
    "seats": 2,
    "totalPrice": 1000,
    "status": "confirmed",
    "bookingDate": "2024-01-01T00:00:00Z"
  }
}
\`\`\`

### Cancel Booking

**Endpoint:** `DELETE /bookings/:id`

**Response:**
\`\`\`json
{
  "message": "Booking cancelled successfully"
}
\`\`\`

## Driver Endpoints

### Get All Drivers

**Endpoint:** `GET /drivers`

### Create Driver

**Endpoint:** `POST /drivers`

**Request Body:**
\`\`\`json
{
  "userId": "user-2",
  "name": "Mike Driver",
  "licenseNumber": "DL123456",
  "phone": "9876543210",
  "status": "active"
}
\`\`\`

### Update Driver

**Endpoint:** `PUT /drivers/:id`

## Maintenance Endpoints

### Get All Maintenance Records

**Endpoint:** `GET /maintenance`

**Query Parameters:**
- `busId` - Filter by bus

### Create Maintenance Record

**Endpoint:** `POST /maintenance`

**Request Body:**
\`\`\`json
{
  "busId": "bus-1",
  "type": "regular",
  "description": "Oil change and filter replacement",
  "cost": 5000,
  "date": "2024-01-15",
  "status": "pending"
}
\`\`\`

### Update Maintenance Record

**Endpoint:** `PUT /maintenance/:id`

## Health Check

### Check Backend Status

**Endpoint:** `GET /health`

**Response:**
\`\`\`json
{
  "status": "Backend is running",
  "timestamp": "2024-01-01T00:00:00Z"
}
\`\`\`

## Error Responses

All error responses follow this format:

\`\`\`json
{
  "error": "Error message",
  "status": 400
}
\`\`\`

### Common Status Codes

- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `404` - Not Found
- `409` - Conflict (e.g., user already exists)
- `500` - Server Error

## Rate Limiting

Currently, there is no rate limiting. For production, consider implementing rate limiting.

## CORS

The backend accepts requests from any origin. For production, update CORS configuration in `server.js`.

## Authentication

Currently, authentication is stateless. For production, consider implementing:
- JWT tokens
- Session management
- Refresh tokens
