# Full-Stack Estate (RiyalEstate)

A full-stack real estate platform built with **Express, Prisma, MongoDB, React (Vite), and Socket.IO**.  
It provides authentication, property listings, user profiles, chat/messaging, and real-time updates.

---

## 🚀 Project Structure

### 📌 API (Backend)
- **Framework:** Express.js  
- **Database:** MongoDB (via Prisma ORM)  
- **Entry point:** `api/app.js`  
- **Prisma:** `api/lib/prisma.js`, schema at `api/prisma/schema.prisma`  
- **Routes:** Auth, Posts, Users, Chats, Messages  
- **Controllers:** Handle authentication, user management, posts, chats, and messages  
- **Config:** `.env` (not committed — required at runtime)

### 📌 Client (Frontend)
- **Framework:** React + Vite  
- **Entry point:** `client/src/main.jsx`  
- **Router:** `client/src/App.jsx`  
- **State management:** Context API (`AuthContext`, `SocketContext`)  
- **Key components:** Upload widget, map (react-leaflet), chat, cards, lists  
- **Config:** `vite.config.js`, `index.html`

### 📌 Socket Server
- **Framework:** Socket.IO  
- **Entry point:** `socket/app.js`  
- **Purpose:** Real-time chat and notifications  

---

## 🛠 Quick Start (Development)

### Prerequisites
- Node.js (>=16)  
- npm  
- MongoDB Atlas (connection string)  

### 1. API
```bash
cd api
npm install
# configure .env file with DATABASE_URL, JWT_SECRET_KEY, CLIENT_URL
node app.js
```

- Runs on port **8800**
- Expects MongoDB connection in `.env`
- Prisma schema in `api/prisma/schema.prisma`

### 2. Socket Server
```bash
cd socket
npm install
node app.js
```

- Runs on port **4000**
- CORS origin: `http://localhost:5173`

### 3. Client
```bash
cd client
npm install
npm run dev
```

- Runs on port **5173**
- API base URL: `http://localhost:8800/api`

---

## 📌 Features

- **Authentication** (register, login, logout)
- **User management** (profile, saved posts, notifications)
- **Real estate listings** (create, view, filter posts)
- **Chat & messaging** (real-time via Socket.IO)
- **Map integration** (React-Leaflet)
- **Cloudinary upload widget** for images

---

## 🔑 Environment Variables

Create `api/.env` with:

```env
DATABASE_URL=
JWT_SECRET_KEY=your_secret_key
CLIENT_URL=http://localhost:5173
```

---

## 🔧 Development Tips

- Add `"start": "node app.js"` or `"dev": "nodemon app.js"` in `api/package.json` and `socket/package.json`
- Ensure `CLIENT_URL` matches your frontend dev server
- If Cloudinary upload fails, check `UploadWidget.jsx` and widget configuration

---

## 📦 Scripts

### Client
- **Lint** → `npm run lint`
- **Build** → `npm run build`
- **Dev** → `npm run dev`

### API / Socket
Add these to `package.json`:
- **Start** → `"start": "node app.js"`
- **Dev** → `"dev": "nodemon app.js"`

---

## 📂 Key Files to Explore

### Backend
- `api/app.js` - Main server entry point
- `api/controllers/*` - Route handlers for different features
- `api/lib/prisma.js` - Database configuration
- `api/prisma/schema.prisma` - Database schema definition

### Socket
- `socket/app.js` - WebSocket server for real-time features

### Frontend
- `client/src/main.jsx` - React application entry point
- `client/src/App.jsx` - Main app component with routing
- `client/src/lib/apiRequest.js` - API communication utilities
- `client/src/context/` - React Context providers

---

## 🏗 Architecture Overview

```
riyalestate/
├── api/                    # Express.js backend
│   ├── app.js             # Server entry point
│   ├── controllers/       # Route handlers
│   ├── lib/               # Utilities (Prisma client)
│   ├── prisma/            # Database schema
│   └── .env               # Environment variables
├── client/                # React frontend
│   ├── src/
│   │   ├── main.jsx       # App entry point
│   │   ├── App.jsx        # Main component
│   │   ├── context/       # State management
│   │   ├── components/    # UI components
│   │   └── lib/           # API utilities
│   └── vite.config.js     # Vite configuration
└── socket/                # Socket.IO server
    └── app.js             # WebSocket server
```

---

## 🔌 API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login  
- `POST /api/auth/logout` - User logout

### Posts (Properties)
- `GET /api/posts` - Get all posts with filters
- `GET /api/posts/:id` - Get single post
- `POST /api/posts` - Create new post
- `PUT /api/posts/:id` - Update post
- `DELETE /api/posts/:id` - Delete post

### Users
- `GET /api/users/profile/:id` - Get user profile
- `PUT /api/users/:id` - Update user profile
- `GET /api/users/:id/posts` - Get user's posts

### Chat & Messages
- `GET /api/chats` - Get user's chats
- `GET /api/chats/:id` - Get chat messages
- `POST /api/chats` - Create new chat
- `POST /api/messages` - Send message

---

## 🔄 Socket.IO Events

### Client → Server
- `newUser` - User joins the application
- `sendMessage` - Send chat message

### Server → Client
- `getMessage` - Receive new message
- `notification` - Receive notifications

---

## 🗄 Database Schema

Key models in `api/prisma/schema.prisma`:

- **User** - User accounts and authentication
- **Post** - Property listings with details
- **Chat** - Chat conversations between users
- **Message** - Individual chat messages
- **SavedPost** - User's bookmarked properties

---

## ✅ Current Status

- ✅ Development-ready setup
- ❌ No test suite configured yet
- ❌ CI/CD not included by default

---

## 🚀 Next Steps

### Recommended Improvements
1. **Add Testing**
   ```bash
   # API testing
   npm install --save-dev jest supertest
   
   # Frontend testing
   npm install --save-dev vitest @testing-library/react
   ```

2. **Add Development Scripts**
   ```json
   {
     "scripts": {
       "start": "node app.js",
       "dev": "nodemon app.js",
       "test": "jest"
     }
   }
   ```

3. **Environment Setup**
   - Create `.env.example` files
   - Add environment validation
   - Set up different configs for dev/prod

4. **Database Setup**
   ```bash
   # Generate Prisma client
   npx prisma generate
   
   # Push schema to database
   npx prisma db push
   ```

---

## 🐛 Troubleshooting

### Common Issues

**Database Connection:**
- Verify `DATABASE_URL` format is correct
- Ensure MongoDB Atlas allows connections from your IP
- Check if database name exists

**Socket Connection:**
- Confirm socket server runs on port 4000
- Verify CORS settings match client URL
- Check firewall settings for WebSocket connections

**Image Upload:**
- Configure Cloudinary credentials in environment
- Verify upload widget configuration
- Check file size limits

---

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/new-feature`
3. Commit changes: `git commit -m 'Add new feature'`
4. Push to branch: `git push origin feature/new-feature`
5. Submit Pull Request

---

## 📄 License

This project is licensed under the MIT License.

---

**Ready to build your real estate platform! 🏠✨**

