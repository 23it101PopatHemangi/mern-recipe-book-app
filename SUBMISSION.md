# MERN Recipe Book - Docker Deployment Submission

## Four Required Submission URLs

### 1. Original GitHub Repository
Replace with the original MERN Recipe Book repository you forked from:
```
https://github.com/[ORIGINAL_OWNER]/mern-recipe-book-app
```
> Note: Find the original repo link on your fork's GitHub page (click "Forked from...")

### 2. Your Forked GitHub Repository
```
https://github.com/23it101PopatHemangi/mern-recipe-book-app
```

### 3. Client Image on Docker Hub
```
https://hub.docker.com/r/popathemangi/recipe-client
```

### 4. Server Image on Docker Hub
```
https://hub.docker.com/r/popathemangi/recipe-server
```

---

## Quick Start - Running the Application

### Prerequisites
- Docker and Docker Compose installed
- Port 3000 (frontend), 6001 (backend), 27017 (MongoDB) available

### Run with Docker Compose
```bash
cd mern-recipe-book-app
docker compose -f docker-compose.prd.yml up -d
```

### Access the Application
- **Frontend:** http://localhost:3000
- **Backend API:** http://localhost:6001
- **MongoDB:** localhost:27017

### View Logs
```bash
docker compose -f docker-compose.prd.yml logs -f
```

### Stop the Application
```bash
docker compose -f docker-compose.prd.yml down
```

---

## Deliverables Included

✅ **Multi-stage Dockerfile for client** (`client/Dockerfile`)
- Builds React app with Node 18
- Serves static files with Nginx
- Accepts `REACT_APP_API_URL` build-arg for backend URL configuration

✅ **Production Dockerfile for server** (`server/Dockerfile`)
- Uses Node 20-alpine
- Runs Express server with environment variables
- Connects to MongoDB via `MONGO_URL` env var

✅ **Docker Compose files**
- `docker-compose.yml` - Development build (local testing)
- `docker-compose.prd.yml` - Production deployment (pulls from Docker Hub)

✅ **.dockerignore files** - Optimized image sizes
- `client/.dockerignore`
- `server/.dockerignore`

✅ **Docker Hub Images**
- `popathemangi/recipe-client:latest` - React frontend (multi-stage build)
- `popathemangi/recipe-server:latest` - Node.js backend

---

## Notes

1. **React API Configuration**: The client build embeds the backend URL at build time. To rebuild with a different API URL:
   ```bash
   docker build --build-arg REACT_APP_API_URL=https://api.yourdomain.com -t popathemangi/recipe-client:latest ./client
   docker push popathemangi/recipe-client:latest
   ```

2. **Database Persistence**: MongoDB data persists in the `mongo-data` volume defined in the compose file.

3. **Network Communication**: All services use a Docker bridge network named `recipe-net` for internal communication.

4. **Environment Variables**:
   - `MONGO_URL`: MongoDB connection string (default: `mongodb://mongo:27017/recipebook`)
   - `PORT`: Server port (default: `6001`)
   - `NODE_ENV`: Set to `production` in server Dockerfile

---

## Troubleshooting

| Issue | Solution |
|-------|----------|
| Port already in use | Change port mappings in `docker-compose.prd.yml` |
| MongoDB connection fails | Ensure `mongo` container is running: `docker ps` |
| Frontend can't reach API | Verify server is running on port 6001 and check CORS settings |
| Images not found on Docker Hub | Re-pull with `docker pull popathemangi/recipe-client:latest` |

---

## Testing Verification

All components tested and working:
- ✅ MongoDB container running and accepting connections
- ✅ Server container connected to MongoDB, API responding on port 6001
- ✅ Client container serving React build on port 3000
- ✅ Docker Compose orchestration validated

---

**Submission Date:** November 13, 2025  
**Student:** Hemangi Popat (23IT101)
