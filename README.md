# 🛒 E-Commerce Web Application

A full-stack e-commerce application built with React, Node.js, Express, and MongoDB Atlas. Features product browsing, detailed product views, and shopping cart functionality with persistent storage.

![Project Status](https://img.shields.io/badge/status-active-success.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

## 📋 Table of Contents

- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [Technical Architecture](#-technical-architecture)
- [Project Structure](#-project-structure)
- [Getting Started](#-getting-started)
- [API Documentation](#-api-documentation)
- [AI Prompts Used](#-ai-prompts-used)
- [Database Schema](#-database-schema)
- [Environment Variables](#-environment-variables)
- [Testing](#-testing)
- [Deployment](#-deployment)
- [Troubleshooting](#-troubleshooting)
- [Future Enhancements](#-future-enhancements)
- [Contributing](#-contributing)
- [License](#-license)

---

## ✨ Features

### User Features
- 🔍 **Product Browsing**: Browse products with search and category filtering
- 📱 **Responsive Design**: Fully responsive UI for mobile, tablet, and desktop
- 🛍️ **Product Details**: Detailed product information with image gallery
- 🛒 **Shopping Cart**: Add/remove items, update quantities
- 💾 **Persistent Cart**: Cart data saved in localStorage
- 📊 **Stock Management**: Real-time stock availability indicators
- 💰 **Price Calculation**: Automatic subtotal, tax, and shipping calculation

### Technical Features
- ⚡ **Fast Performance**: Optimized React components
- 🔒 **Error Handling**: Comprehensive error boundaries
- 🎨 **Modern UI**: Clean, Material Design-inspired interface
- 🔄 **State Management**: Efficient Context API implementation
- 📡 **REST API**: Well-structured backend API
- 🗄️ **Database**: MongoDB Atlas for cloud data storage

---

## 🛠 Technology Stack

### Frontend
| Technology | Version | Purpose |
|-----------|---------|---------|
| React | 18.x | UI Library |
| React Router | 6.x | Client-side routing |
| Context API | - | State management |
| CSS3 | - | Styling |
| Axios | 1.x | HTTP client |

### Backend
| Technology | Version | Purpose |
|-----------|---------|---------|
| Node.js | 18.x+ | Runtime environment |
| Express.js | 4.x | Web framework |
| Mongoose | 7.x | MongoDB ODM |
| CORS | 2.x | Cross-origin resource sharing |
| dotenv | 16.x | Environment variables |

### Database
| Technology | Purpose |
|-----------|---------|
| MongoDB Atlas | Cloud database |

### Development Tools
- npm/yarn - Package management
- Git - Version control
- VS Code - Code editor (recommended)

---

## 🏗 Technical Architecture

### Architecture Overview

```
┌─────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                         │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              React Application (Port 3000)           │   │
│  │                                                       │   │
│  │  ├── Components (Header, ProductCard, CartItem)     │   │
│  │  ├── Pages (ProductList, ProductDetails, Cart)      │   │
│  │  ├── Context (CartContext)                           │   │
│  │  └── Services (API Service)                          │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                              ↕ HTTP/REST API
┌─────────────────────────────────────────────────────────────┐
│                         SERVER LAYER                         │
│  ┌─────────────────────────────────────────────────────┐   │
│  │          Express.js Server (Port 5000)              │   │
│  │                                                       │   │
│  │  ├── Routes (Product Routes)                         │   │
│  │  ├── Controllers (Product Logic)                     │   │
│  │  ├── Models (Mongoose Schemas)                       │   │
│  │  └── Middleware (CORS, JSON Parser, Error Handler)  │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
                              ↕ MongoDB Protocol
┌─────────────────────────────────────────────────────────────┐
│                       DATABASE LAYER                         │
│  ┌─────────────────────────────────────────────────────┐   │
│  │              MongoDB Atlas (Cloud)                   │   │
│  │                                                       │   │
│  │  └── Collections                                     │   │
│  │      └── products                                    │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

### Data Flow

#### Product Listing Flow
```
User → ProductList Page → API Service → GET /api/products
  → Express Router → Product Controller → MongoDB
  → Products Array → JSON Response → React State → UI Render
```

#### Add to Cart Flow
```
User Clicks "Add to Cart" → CartContext.addToCart()
  → Update State → Save to localStorage → Update UI
  → Cart Badge Updates → Success Message
```

#### Product Details Flow
```
User Clicks Product → Navigate to /product/:id
  → API Service → GET /api/products/:id
  → Express Router → Product Controller → MongoDB
  → Single Product → JSON Response → React State → UI Render
```

### Component Hierarchy

```
App
├── CartProvider (Context)
│   ├── Header
│   │   ├── Logo
│   │   └── Navigation (Cart Badge)
│   │
│   ├── Routes
│   │   ├── ProductList
│   │   │   ├── Search Input
│   │   │   ├── Category Filters
│   │   │   └── ProductCard[] (Grid)
│   │   │
│   │   ├── ProductDetails
│   │   │   ├── Product Image
│   │   │   ├── Product Info
│   │   │   ├── Quantity Controls
│   │   │   └── Add to Cart Button
│   │   │
│   │   └── Cart
│   │       ├── CartItem[]
│   │       └── Cart Summary
│   │           ├── Price Breakdown
│   │           └── Checkout Button
│   │
│   └── Footer
```

---

## 📁 Project Structure

### Backend Structure
```
ecommerce-backend/
├── node_modules/
├── config/
│   └── db.js                 # MongoDB connection
├── models/
│   └── Product.js            # Product schema
├── routes/
│   └── products.js           # Product routes
├── .env                      # Environment variables
├── .gitignore
├── package.json
├── server.js                 # Main server file
└── seedProducts.js           # Database seeding script
```

### Frontend Structure
```
ecommerce-frontend/
├── node_modules/
├── public/
│   ├── index.html
│   └── favicon.ico
├── src/
│   ├── components/
│   │   ├── Header.jsx
│   │   ├── Header.css
│   │   ├── ProductCard.jsx
│   │   ├── ProductCard.css
│   │   ├── CartItem.jsx
│   │   ├── CartItem.css
│   │   ├── Loading.jsx
│   │   └── Loading.css
│   ├── pages/
│   │   ├── ProductList.jsx
│   │   ├── ProductList.css
│   │   ├── ProductDetails.jsx
│   │   ├── ProductDetails.css
│   │   ├── Cart.jsx
│   │   └── Cart.css
│   ├── context/
│   │   └── CartContext.jsx
│   ├── services/
│   │   └── api.js            # API service
│   ├── App.jsx
│   ├── App.css
│   ├── index.js
│   └── index.css
├── .env
├── .gitignore
├── package.json
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- **Node.js**: v18.0.0 or higher ([Download](https://nodejs.org/))
- **npm**: v9.0.0 or higher (comes with Node.js)
- **MongoDB Atlas Account**: Free tier available ([Sign up](https://www.mongodb.com/cloud/atlas))
- **Git**: For version control ([Download](https://git-scm.com/))

### MongoDB Atlas Setup

1. **Create Account**
   - Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
   - Sign up for a free account

2. **Create Cluster**
   - Click "Build a Database"
   - Select "Free" tier (M0)
   - Choose your preferred region
   - Click "Create Cluster"

3. **Database Access**
   - Go to "Database Access" in left sidebar
   - Click "Add New Database User"
   - Create username and password (save these!)
   - Select "Read and write to any database"

4. **Network Access**
   - Go to "Network Access" in left sidebar
   - Click "Add IP Address"
   - Click "Allow Access from Anywhere" (0.0.0.0/0) for development
   - Click "Confirm"

5. **Get Connection String**
   - Go to "Database" in left sidebar
   - Click "Connect" on your cluster
   - Select "Connect your application"
   - Copy the connection string
   - Replace `<username>` and `<password>` with your credentials
   - Add `/ecommerce` before the `?` in the connection string

### Backend Setup

```bash
# 1. Create and navigate to backend directory
mkdir ecommerce-backend
cd ecommerce-backend

# 2. Initialize npm
npm init -y

# 3. Install dependencies
npm install express mongoose cors dotenv

# 4. Create .env file
echo "PORT=5000
MONGODB_URI=your_mongodb_connection_string_here" > .env

# 5. Create necessary files
# Copy server.js content from the provided file

# 6. Seed the database
node seedProducts.js

# 7. Start the server
node server.js
# Server should be running at http://localhost:5000
```

### Frontend Setup

```bash
# 1. Create React app (in project root)
npx create-react-app ecommerce-frontend
cd ecommerce-frontend

# 2. Install dependencies
npm install react-router-dom axios

# 3. Create .env file
echo "REACT_APP_API_URL=http://localhost:5000/api" > .env

# 4. Create folder structure
mkdir src/components src/pages src/context src/services

# 5. Copy all component, page, context, and service files

# 6. Start development server
npm start
# App should open at http://localhost:3000
```

### Quick Start (Both Servers)

**Terminal 1 - Backend:**
```bash
cd ecommerce-backend
node server.js
```

**Terminal 2 - Frontend:**
```bash
cd ecommerce-frontend
npm start
```

### Verification

✅ Backend running: Visit `http://localhost:5000`
✅ API working: Visit `http://localhost:5000/api/products`
✅ Frontend running: Visit `http://localhost:3000`

---

## 📡 API Documentation

### Base URL
```
http://localhost:5000/api
```

### Endpoints

#### 1. Get All Products
```http
GET /products
```

**Query Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| category | string | Filter by category (optional) |
| search | string | Search products by name (optional) |

**Response:**
```json
[
  {
    "_id": "507f1f77bcf86cd799439011",
    "id": "prod-001",
    "name": "Wireless Headphones",
    "description": "Premium noise-canceling wireless headphones",
    "price": 99.99,
    "image": "https://images.unsplash.com/...",
    "category": "Electronics",
    "stock": 50,
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:30:00.000Z"
  }
]
```

#### 2. Get Single Product
```http
GET /products/:id
```

**URL Parameters:**
| Parameter | Type | Description |
|-----------|------|-------------|
| id | string | Product ID (e.g., "prod-001") |

**Response:**
```json
{
  "_id": "507f1f77bcf86cd799439011",
  "id": "prod-001",
  "name": "Wireless Headphones",
  "description": "Premium noise-canceling wireless headphones with 30-hour battery life.",
  "price": 99.99,
  "image": "https://images.unsplash.com/...",
  "category": "Electronics",
  "stock": 50,
  "createdAt": "2024-01-15T10:30:00.000Z",
  "updatedAt": "2024-01-15T10:30:00.000Z"
}
```

**Error Response (404):**
```json
{
  "message": "Product not found"
}
```

#### 3. Create Product (Testing Only)
```http
POST /products
```

**Request Body:**
```json
{
  "id": "prod-009",
  "name": "New Product",
  "description": "Product description",
  "price": 49.99,
  "image": "https://example.com/image.jpg",
  "category": "Electronics",
  "stock": 20
}
```

#### 4. Delete Product (Testing Only)
```http
DELETE /products/:id
```

### Error Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 201 | Created |
| 404 | Not Found |
| 500 | Server Error |

---

## 🤖 AI Prompts Used

This project was developed using AI-assisted development. Below are the key prompts used to generate different parts of the application.

### 1. Initial Project Requirements

```
Build a complete E-Commerce Website with the following specifications:

Project Overview:
Create a basic e-commerce application that enables users to:
1. Explore a list of products (Product Listing Page)
2. View product details (Product Details Page)
3. Manage a shopping cart with basic state management (Cart Page)

Technical Requirements:
Frontend: React.js with React Router, Context API for state management
Backend: Node.js with Express.js, REST API endpoints
Database: MongoDB Atlas with product schema

Deliverables:
1. Technical architecture documentation
2. Full code base (frontend + backend)
3. Setup instructions
```

### 2. Technical Architecture Documentation

```
Create comprehensive technical architecture documentation including:
- Complete technology stack breakdown
- Detailed folder structure for frontend and backend
- Database schema definition with all fields
- Complete API endpoint documentation
- Data flow diagrams
- State management structure
- Security considerations
- Future enhancement suggestions
```

### 3. Backend Code Generation

```
Generate complete backend code for the e-commerce application with:
1. Express.js server setup with CORS and middleware
2. MongoDB connection using Mongoose
3. Product model with validation
4. REST API routes (GET all, GET by ID, POST, DELETE)
5. Error handling middleware
6. Sample product seeding script
7. Environment variable configuration
```

### 4. Frontend React Components

```
Generate React components for the e-commerce application:
1. Header with navigation and cart badge
2. ProductCard with image, details, and stock indicators
3. CartItem with quantity controls and remove button
4. Loading component with spinner animation
5. All components should be responsive and follow Material Design
```

### 5. Frontend Pages

```
Generate React page components:
1. ProductList with search, category filters, and grid layout
2. ProductDetails with image, description, quantity selector
3. Cart page with items list and order summary
4. Include loading states, error handling, and empty states
5. Implement responsive design for all screen sizes
```

### 6. State Management & API Integration

```
Create:
1. CartContext using React Context API with:
   - Add to cart functionality
   - Remove from cart
   - Update quantity
   - Calculate totals
   - localStorage persistence
2. API service with Axios for all backend calls
3. Error handling for network requests
```

### 7. Styling & Responsiveness

```
Create modern, responsive CSS styling:
- Material Design principles
- Consistent color scheme
- Smooth animations and transitions
- Mobile-first approach
- Hover effects and interactive elements
- Accessibility considerations
```

### 8. Documentation & Setup

```
Generate comprehensive documentation:
- README with setup instructions
- MongoDB Atlas configuration guide
- Environment variables documentation
- API documentation with examples
- Troubleshooting guide
- Testing checklist
```

### Prompt Engineering Best Practices Used

1. **Specificity**: Detailed requirements for each component
2. **Context**: Clear project scope and constraints
3. **Examples**: Expected output formats and structures
4. **Iteration**: Breaking complex tasks into manageable chunks
5. **Validation**: Including testing and verification steps

---

## 🗄 Database Schema

### Product Schema

```javascript
{
  id: {
    type: String,
    required: true,
    unique: true,
    description: "Unique product identifier (e.g., 'prod-001')"
  },
  name: {
    type: String,
    required: true,
    description: "Product name"
  },
  description: {
    type: String,
    required: true,
    description: "Detailed product description"
  },
  price: {
    type: Number,
    required: true,
    min: 0,
    description: "Product price in USD"
  },
  image: {
    type: String,
    required: true,
    description: "Product image URL"
  },
  category: {
    type: String,
    required: true,
    description: "Product category (e.g., 'Electronics', 'Accessories')"
  },
  stock: {
    type: Number,
    required: true,
    min: 0,
    default: 0,
    description: "Available stock quantity"
  },
  createdAt: {
    type: Date,
    description: "Timestamp of creation (auto-generated)"
  },
  updatedAt: {
    type: Date,
    description: "Timestamp of last update (auto-generated)"
  }
}
```

### Sample Product Data

```json
{
  "id": "prod-001",
  "name": "Wireless Headphones",
  "description": "Premium noise-canceling wireless headphones with 30-hour battery life.",
  "price": 99.99,
  "image": "https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=500",
  "category": "Electronics",
  "stock": 50
}
```

---

## 🔐 Environment Variables

### Backend (.env)

```env
# Server Configuration
PORT=5000

# Database Configuration
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/ecommerce?retryWrites=true&w=majority

# Optional: Node Environment
NODE_ENV=development
```

### Frontend (.env)

```env
# API Configuration
REACT_APP_API_URL=http://localhost:5000/api

# Optional: Other configurations
REACT_APP_SITE_NAME=E-Shop
```

### Security Notes

⚠️ **Never commit `.env` files to version control**
- Add `.env` to `.gitignore`
- Use environment-specific `.env` files
- Store production secrets in secure vault
- Rotate credentials regularly

---

## 🧪 Testing

### Manual Testing Checklist

#### Product List Page
- [ ] Products load successfully
- [ ] Search filters products correctly
- [ ] Category filters work
- [ ] Product cards display all information
- [ ] Clicking product navigates to details
- [ ] Loading state displays
- [ ] Error handling works
- [ ] Responsive on mobile/tablet

#### Product Details Page
- [ ] Product details load correctly
- [ ] Images display properly
- [ ] Stock indicator accurate
- [ ] Quantity controls work
- [ ] Add to cart updates badge
- [ ] Success message displays
- [ ] Back button works
- [ ] Out of stock products handled

#### Cart Page
- [ ] Cart items display correctly
- [ ] Quantity updates work
- [ ] Remove button works
- [ ] Totals calculate correctly
- [ ] Empty cart message shows
- [ ] Clear cart works
- [ ] Navigation works
- [ ] localStorage persists cart

### API Testing

Using cURL or Postman:

```bash
# Test get all products
curl http://localhost:5000/api/products

# Test get single product
curl http://localhost:5000/api/products/prod-001

# Test with category filter
curl "http://localhost:5000/api/products?category=Electronics"

# Test with search
curl "http://localhost:5000/api/products?search=wireless"
```

---

## 🌐 Deployment

### Backend Deployment (Heroku)

```bash
# Install Heroku CLI
# Login to Heroku
heroku login

# Create app
heroku create your-app-name

# Set environment variables
heroku config:set MONGODB_URI=your_connection_string

# Deploy
git push heroku main

# Check logs
heroku logs --tail
```

### Frontend Deployment (Vercel)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Set environment variables in Vercel dashboard
# REACT_APP_API_URL=https://your-backend.herokuapp.com/api
```

### Alternative: Full Stack on Render

1. Connect GitHub repository
2. Create Web Service for backend
3. Create Static Site for frontend
4. Configure environment variables
5. Deploy

---

## 🔧 Troubleshooting

### Common Issues & Solutions

#### 1. MongoDB Connection Failed

**Error:** `MongooseServerSelectionError: connect ECONNREFUSED`

**Solutions:**
- Verify MongoDB URI in `.env`
- Check network access in MongoDB Atlas (whitelist IP)
- Ensure database user credentials are correct
- Check if cluster is active

#### 2. CORS Errors

**Error:** `Access to fetch blocked by CORS policy`

**Solutions:**
- Verify CORS is enabled in backend
- Check API URL in frontend `.env`
- Ensure backend is running
- Try adding specific origin in CORS config

#### 3. Port Already in Use

**Error:** `EADDRINUSE: address already in use`

**Solutions:**
```bash
# Find process using port (Mac/Linux)
lsof -i :5000

# Kill process
kill -9 <PID>

# Or change PORT in .env
PORT=5001
```

#### 4. Module Not Found

**Error:** `Cannot find module 'express'`

**Solutions:**
```bash
# Delete node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

#### 5. Cart Not Persisting

**Solutions:**
- Check browser localStorage is enabled
- Clear browser cache
- Check for JavaScript errors in console
- Verify CartContext is wrapping App

#### 6. Images Not Loading

**Solutions:**
- Check internet connection
- Verify image URLs are valid
- Check for CORS issues with image host
- Use fallback images

---

## 🚀 Future Enhancements

### Phase 1: User Features
- [ ] User authentication (JWT)
- [ ] User profiles and order history
- [ ] Product reviews and ratings
- [ ] Wishlist functionality
- [ ] Product recommendations

### Phase 2: Advanced Features
- [ ] Payment integration (Stripe/PayPal)
- [ ] Order tracking
- [ ] Email notifications
- [ ] Advanced search with filters
- [ ] Product sorting options

### Phase 3: Admin Features
- [ ] Admin dashboard
- [ ] Product management (CRUD)
- [ ] Inventory management
- [ ] Order management
- [ ] Analytics and reports

### Phase 4: Technical Improvements
- [ ] Unit and integration tests
- [ ] CI/CD pipeline
- [ ] Performance optimization
- [ ] SEO optimization
- [ ] PWA features
- [ ] Multi-language support

### Phase 5: Advanced Functionality
- [ ] Real-time inventory updates
- [ ] Chat support
- [ ] Social media integration
- [ ] Advanced analytics
- [ ] Mobile app (React Native)

---

## 👥 Contributing

Contributions are welcome! Please follow these steps:

1. **Fork the repository**
2. **Create a feature branch**
   ```bash
   git checkout -b feature/amazing-feature
   ```
3. **Commit your changes**
   ```bash
   git commit -m 'Add some amazing feature'
   ```
4. **Push to the branch**
   ```bash
   git push origin feature/amazing-feature
   ```
5. **Open a Pull Request**

### Code Style Guidelines
- Use ESLint configuration
- Follow React best practices
- Write descriptive commit messages
- Add comments for complex logic
- Update documentation

---

## 📄 License

This project is licensed under the MIT License.

```
MIT License

Copyright (c) 2024 E-Commerce Project

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 📞 Support

For support, please:
- Open an issue on GitHub
- Check existing documentation
- Review troubleshooting guide

---

## 🙏 Acknowledgments

- React team for the amazing framework
- Express.js community
- MongoDB Atlas for database hosting
- Unsplash for product images
- All contributors and testers

---

## 📊 Project Statistics

- **Lines of Code**: ~3,000+
- **Components**: 8
- **API Endpoints**: 4
- **Database Collections**: 1
- **Development Time**: 2-3 days
- **AI Assistance**: Claude (Anthropic)

---

## 🔗 Useful Links

- [React Documentation](https://react.dev)
- [Express.js Guide](https://expressjs.com)
- [MongoDB Atlas Docs](https://docs.atlas.mongodb.com)
- [React Router Documentation](https://reactrouter.com)
- [Mongoose Documentation](https://mongoosejs.com)

---

**Made with ❤️ using React, Node.js, and MongoDB**

*Last Updated: November 2024*
