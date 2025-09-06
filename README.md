# Roxiler - Store Rating System (FullStack Application)

A comprehensive store rating system built with Express.js backend and React.js frontend, featuring role-based authentication and a complete rating management system.

## 🏗 Architecture

### Backend (Express.js + SQLite)
- *Framework*: Express.js with Node.js
- *Database*: SQLite with advanced schema design
- *Authentication*: JWT-based with role-based authorization
- *Validation*: Joi schema validation with custom rules
- *Security*: Rate limiting, CORS, password hashing

### Frontend (React.js)
- *Framework*: React 18 with functional components
- *Routing*: React Router DOM v6 with protected routes
- *State Management*: Context API for global state
- *Styling*: Custom CSS with responsive design
- *API Client*: Axios with interceptors

## 👥 User Roles & Permissions

### 🔧 System Administrator
- Manage all users (create, view, filter, sort)
- Manage stores (create, assign owners)
- View system dashboard with statistics
- Access to all system data

### 👤 Normal User
- Browse and search stores
- Submit and update store ratings (1-5 stars)
- View store details and ratings
- Manage personal profile

### 🏪 Store Owner
- View store dashboard with analytics
- See customer ratings and feedback
- Track rating history and trends
- View rating distribution charts

## 🚀 Quick Start

### Prerequisites
- Node.js (v14+)
- PostgreSQL (v12+)
- npm or yarn

### 1. Clone & Setup
bash
git clone <repository-url>
cd Roxiler


### 2. Backend Setup
bash
cd backend
npm install

# Setup environment
cp .env.example .env
# Edit .env with your database credentials

# Start backend server
npm run dev


### 3. Database Setup
bash
# Create PostgreSQL database
createdb rating_system

# Seed with sample data (optional)
npm run seed


### 4. Frontend Setup
bash
cd ../frontend
npm install

# Start frontend development server
npm start


### 5. Access Application
- *Frontend*: http://localhost:3000
- *Backend API*: http://localhost:5000
- *Health Check*: http://localhost:5000/health

## 🔐 Sample Login Credentials

After running the seed script:

| Role | Email | Password |
|------|-------|----------|
| *System Admin* | admin@ratingsystem.com | Admin123! |
| *Normal User* | john.smith@example.com | User123! |
| *Store Owner* | robert.davis@pizzapalace.com | Owner123! |

## 📊 Key Features

### ✅ Authentication & Security
- JWT token-based authentication
- Role-based authorization
- Password encryption with bcrypt
- Rate limiting and CORS protection
- Session management with auto-logout

### ✅ Rating System
- 5-star rating system
- Real-time rating calculations
- Rating history and analytics
- Rating distribution charts
- Prevent duplicate ratings per user-store

### ✅ User Management
- User registration with validation
- Profile management
- Password update functionality
- User filtering and sorting
- Role-based dashboard access

### ✅ Store Management
- Store creation and management
- Store search and filtering
- Owner assignment system
- Store analytics dashboard
- Rating aggregation

### ✅ Data Validation
- *Name*: 20-60 characters
- *Password*: 8-16 chars, 1 uppercase, 1 special character
- *Email*: Standard email validation
- *Address*: Max 400 characters
- *Rating*: Integer 1-5

### ✅ Advanced Features
- Sorting (ascending/descending) on all tables
- Advanced search and filtering
- Responsive mobile-friendly design
- Real-time notifications
- Database triggers for rating calculations
- Comprehensive error handling

## 🗄 Database Schema

### Users Table
sql
- id (UUID, Primary Key)
- name (VARCHAR(60))
- email (VARCHAR(255), Unique)
- password (VARCHAR(255), Hashed)
- address (VARCHAR(400))
- role (ENUM: system_admin, normal_user, store_owner)
- created_at, updated_at


### Stores Table
sql
- id (UUID, Primary Key)
- name (VARCHAR(60))
- email (VARCHAR(255), Unique)
- address (VARCHAR(400))
- owner_id (UUID, FK to Users)
- average_rating (DECIMAL(2,1))
- total_ratings (INTEGER)
- created_at, updated_at


### Ratings Table
sql
- id (UUID, Primary Key)
- user_id (UUID, FK to Users)
- store_id (UUID, FK to Stores)
- rating (INTEGER, 1-5)
- created_at, updated_at
- UNIQUE(user_id, store_id)


## 🛠 API Endpoints

### Authentication
- POST /api/auth/register - User registration
- POST /api/auth/login - User login
- GET /api/auth/profile - Get user profile
- PUT /api/auth/password - Update password

### Admin (system_admin only)
- GET /api/admin/dashboard - System statistics
- POST /api/admin/users - Create user
- GET /api/admin/users - List users (with filters)
- GET /api/admin/users/:id - User details
- POST /api/admin/stores - Create store
- GET /api/admin/stores - List stores (with filters)

### User (normal_user only)
- GET /api/user/stores - Browse stores
- POST /api/user/ratings - Submit rating
- PUT /api/user/ratings - Update rating

### Store Owner (store_owner only)
- GET /api/store/dashboard - Store dashboard
- GET /api/store/ratings - Store ratings

## 📁 Project Structure


Roxiler/
├── backend/                 # Express.js Backend
│   ├── src/
│   │   ├── config/         # Database & schema config
│   │   ├── controllers/    # Request handlers
│   │   ├── middleware/     # Auth & validation middleware
│   │   ├── models/         # Database models
│   │   ├── routes/         # API routes
│   │   ├── utils/          # Utilities & helpers
│   │   └── index.js        # Main server file
│   ├── package.json
│   ├── .env.example
│   └── README.md
├── frontend/               # React.js Frontend
│   ├── src/
│   │   ├── components/     # Reusable components
│   │   ├── context/        # Context providers
│   │   ├── pages/          # Page components
│   │   │   ├── admin/      # Admin pages
│   │   │   ├── user/       # User pages
│   │   │   └── store/      # Store owner pages
│   │   ├── services/       # API services
│   │   ├── utils/          # Utility functions
│   │   ├── App.js          # Main app component
│   │   └── index.js        # Entry point
│   ├── package.json
│   └── README.md
└── README.md               # This file


## 🔧 Development

### Backend Development
bash
cd backend
npm run dev    # Start with nodemon
npm run seed   # Populate sample data


### Frontend Development
bash
cd frontend
npm start      # Start development server
npm run build  # Create production build


### Database Operations
bash
# Reset database (from backend directory)
npm run seed

# Manual database operations
psql -d rating_system


## 🚀 Production Deployment

### Backend
1. Set environment variables
2. Install dependencies: npm install --production
3. Start server: npm start

### Frontend
1. Build production bundle: npm run build
2. Serve static files with nginx/apache
3. Configure API_URL for production

### Environment Variables
bash
# Backend (.env)
NODE_ENV=production
PORT=5000
DB_HOST=your_db_host
DB_NAME=rating_system
DB_USER=your_db_user
DB_PASSWORD=your_db_password
JWT_SECRET=your_jwt_secret
CORS_ORIGIN=https://yourdomain.com

# Frontend (.env)
REACT_APP_API_URL=https://your-api-domain.com/api


## 🧪 Testing

### Manual Testing Checklist
- [ ] User registration with validation
- [ ] Login with different roles
- [ ] Admin dashboard and user management
- [ ] Store creation and management
- [ ] Rating submission and updates
- [ ] Store owner dashboard
- [ ] Search and filtering
- [ ] Sorting functionality
- [ ] Password updates
- [ ] Error handling

## 📝 License

This project is created for educational/interview purposes.

## 🤝 Contributing

1. Fork the repository
2. Create feature branch
3. Make changes
4. Test thoroughly
5. Submit pull request

## ⚡ Performance Considerations

### Backend
- Database indexes on frequently queried fields
- Connection pooling for PostgreSQL
- Rate limiting to prevent abuse
- Efficient SQL queries with joins

### Frontend
- Component memoization opportunities
- Lazy loading for routes
- Optimized bundle size
- Efficient state management

## 🛡 Security Features

- Password hashing with bcrypt (12 rounds)
- JWT token expiration and refresh
- Input validation and sanitization
- SQL injection prevention
- XSS protection through React
- CORS configuration
- Rate limiting

## 📈 Future Enhancements

- [ ] Email notifications
- [ ] File upload for store images
- [ ] Advanced analytics dashboard
- [ ] Mobile app with React Native
- [ ] Real-time notifications with WebSocket
- [ ] Caching with Redis
- [ ] Full-text search
- [ ] Rating comments/reviews
- [ ] Store categories
- [ ] Geolocation features

---

*Built with ❤ for the FullStack Developer Challenge*
