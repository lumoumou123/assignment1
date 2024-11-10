## Agile Software Practice - Assignment 1.

## Version

- Docker Compose File Version: `3.8`

## Services

### MongoDB

- **Image**: `mongo:8.0-rc`
- **Container Name**: `mongo`
- **Environment Variables**:
  - `MONGO_INITDB_ROOT_USERNAME`: `admin`
  - `MONGO_INITDB_ROOT_PASSWORD`: `password`
- **Networks**:
  - `mongodb-mongo-express`
  - `mongodb-moviesapi`

### Mongo Express

- **Image**: `mongo-express:1.0-20-alpine3.19`
- **Container Name**: `mongo-express`
- **Environment Variables**:
  - `ME_CONFIG_MONGODB_ADMINUSERNAME`: `admin`
  - `ME_CONFIG_MONGODB_ADMINPASSWORD`: `password`
  - `ME_CONFIG_MONGODB_SERVER`: `mongo`
- **Depends On**:
  - `mongo`
- **Ports**:
  - `8081:8081`
- **Networks**:
  - `mongodb-mongo-express`

### Redis

- **Image**: `redis:alpine`
- **Container Name**: `redis`
- **Networks**:
  - `redis-moviesapi`

### Movie API

- **Image**: `doconnor/movies-api:1.0`
- **Container Name**: `movies-api`
- **Ports**:
  - `9000:9000`
- **Environment Variables**:
  - `MONGODB_URI`: `mongodb://admin:password@mongo:27017`
  - `REDIS_URI`: `redis://redis:6379`
  - `ENABLE_WRITING_HANDLERS`: `'false'`
- **Depends On**:
  - `mongo`
  - `redis`
- **Networks**:
  - `mongodb-moviesapi`
  - `redis-moviesapi`

## Network Settings

- **Network Names**: `mongodb-mongo-express`, `mongodb-moviesapi`, `redis-moviesapi`
- **Driver**: `bridge`

## note
 - **Grading Spectrum**: Application stack is partially integrated.
                         Stack is fully integrated. Container isolation requirements.
Trying to use addSeed.js to add seeding data but encountering failure