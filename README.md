# Service Aggregator Platform

A full-stack web application that connects **service providers** (caterers, photographers, florists, decorators, etc.) with **consumers** looking to book services for events.

Providers can manage services, packages, availability, and booking requests.  
Consumers can browse services, compare packages, book dates, and track booking status.

---

## Features

### For Consumers
- Register / Login
- Browse and filter services
- View service details, images, and packages
- Book a service with package selection
- View availability calendar (available vs blocked dates)
- Cancel bookings
- Receive in-app notifications

### For Providers
- Register / Login as Provider
- Add, edit, and delete services
- Upload multiple service images (Cloudinary)
- Create multiple packages (name, description, price)
- Manage availability / blocked dates
- Confirm or cancel booking requests
- Automatic date blocking when a booking is confirmed
- In-app notifications for new bookings

### General
- JWT authentication with role-based access
- Responsive UI
- Loading and empty states
- Cascading delete: deleting a service cancels related bookings

---

## Tech Stack

### Frontend
- React.js
- React Router
- Axios
- Context API (auth state)
- react-calendar

### Backend
- Node.js
- Express.js
- MongoDB + Mongoose
- JWT (jsonwebtoken)
- bcryptjs
- Cloudinary + Multer (image uploads)
- dotenv, cors

### Deployment
- Frontend: Vercel
- Backend: Render
- Database: MongoDB Atlas

---

## Project Structure

    service-aggregator-backend/          <- Repository root
    ├── service-aggregator-backend/      <- Backend (Node + Express)
    │   ├── config/
    │   ├── middleware/
    │   ├── models/
    │   ├── routes/
    │   ├── server.js
    │   └── package.json
    │
    └── service-aggregator-frontend/     <- Frontend (React)
        ├── src/
        │   ├── components/
        │   ├── context/
        │   ├── api.js
        │   └── App.js
        └── package.json

---

## How to Run Locally

### 1. Backend

    cd service-aggregator-backend
    npm install

Create a `.env` file:

    MONGO_URI=your_mongodb_connection_string
    JWT_SECRET=your_secret_key
    PORT=5000
    CLOUDINARY_CLOUD_NAME=your_cloud_name
    CLOUDINARY_API_KEY=your_api_key
    CLOUDINARY_API_SECRET=your_api_secret

Start the backend:

    npm run dev

Backend runs on: http://localhost:5000

---

### 2. Frontend

    cd service-aggregator-frontend
    npm install

Create a `.env` file:

    REACT_APP_API_URL=http://localhost:5000

Start the frontend:

    npm start

Frontend runs on: http://localhost:3000

---

## API Endpoints

### Auth
- POST /api/auth/register
- POST /api/auth/login

### Services
- GET /api/services
- POST /api/services (Provider only, supports image upload)
- PUT /api/services/:id (Owner only)
- DELETE /api/services/:id (Owner only)
- GET /api/services/my-services (Provider only)
- POST /api/services/:id/block-date
- DELETE /api/services/:id/block-date/:dateId

### Bookings
- POST /api/bookings (Consumer only)
- GET /api/bookings/my-bookings
- PATCH /api/bookings/:id/status (Confirm / Cancel)

### Notifications
- GET /api/notifications
- GET /api/notifications/unread-count
- PATCH /api/notifications/:id/read
- PATCH /api/notifications/read-all

---

## Key Implementation Details

- Role-based access: Providers manage services; consumers book them
- Packages: Services can have multiple packages instead of a single price
- Availability model: Dates are available by default; confirmed bookings and manual blocks mark dates as unavailable
- Image uploads: Stored on Cloudinary via Multer
- Notifications: In-app alerts for booking requests, confirmations, and cancellations

---

## Future Improvements

- Ratings and reviews
- Email notifications
- Payment integration
- Advanced search and filters
- Admin dashboard
- Unit and integration tests

---

## Author

**Navraj Chauhan**