> Steps to set up development docker containers

### 1. Creating a docker network
```
docker network create goals-net
```

### 2. Docker MongoDB persistent Container
```
docker run --name mongodb -v data:/data/db --rm -d --network goals-net mongo
```

### 3. Building Backend Image and Container
```
cd backend
docker build -t goals-node .
docker run --name goals-backend -v $(pwd):/app -v logs:/app/logs -v /app/node_modules --network goals-net --rm -p 80:80 goals-node
```
### 4. Building frontend Image and Container
```
cd .. && cd frontend
docker build -t goals-react .
docker run --name goals-frontend -v $(pwd)/src:/app/src -p 3000:3000 --rm -d -it goals-react
```

