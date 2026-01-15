# Docker Setup for Hotel Booking App

## Prerequisites
- Docker installed on your machine
- Docker Compose installed

## Quick Start

1. **Create your environment file:**
   ```bash
   cp .env.example .env
   ```
   Then edit `.env` with your actual credentials.

2. **Build and start all services:**
   ```bash
   docker-compose up --build
   ```

3. **Access the application:**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:7000
   - MongoDB: localhost:27017

## Docker Commands

### Start services (detached mode)
```bash
docker-compose up -d
```

### Stop services
```bash
docker-compose down
```

### Stop services and remove volumes (clean slate)
```bash
docker-compose down -v
```

### View logs
```bash
# All services
docker-compose logs -f

# Specific service
docker-compose logs -f backend
docker-compose logs -f frontend
docker-compose logs -f mongodb
```

### Rebuild specific service
```bash
docker-compose up --build backend
docker-compose up --build frontend
```

### Execute commands in running container
```bash
# Access backend shell
docker-compose exec backend sh

# Access MongoDB shell
docker-compose exec mongodb mongosh -u admin -p password123
```

## Development Mode

For development with hot-reload, you can modify the docker-compose.yml or create a `docker-compose.dev.yml`:

```bash
# Use development override
docker-compose -f docker-compose.yml -f docker-compose.dev.yml up
```

## Environment Variables

Required environment variables (set in `.env` file):
- `JWT_SECRET_KEY` - Secret key for JWT tokens
- `CLOUDINARY_CLOUD_NAME` - Cloudinary cloud name
- `CLOUDINARY_API_KEY` - Cloudinary API key
- `CLOUDINARY_API_SECRET` - Cloudinary API secret
- `STRIPE_API_KEY` - Stripe secret key
- `VITE_STRIPE_PUB_KEY` - Stripe publishable key

## Architecture

- **MongoDB**: Database service running on port 27017
- **Backend**: Node.js/Express API running on port 7000
- **Frontend**: React app served by Nginx on port 3000

All services are connected via a Docker network called `hotel-booking-network`.

## Troubleshooting

### Port already in use
If you get a port conflict, change the port mapping in docker-compose.yml:
```yaml
ports:
  - "3001:80"  # Change 3000 to 3001
```

### MongoDB connection issues
Check if MongoDB is running:
```bash
docker-compose ps
```

### Clear all Docker resources
```bash
docker-compose down -v
docker system prune -a
```
