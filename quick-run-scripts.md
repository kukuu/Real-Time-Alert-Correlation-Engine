# Quick Run Scripts

```
#!/bin/bash
# frontend/scripts/start-dev.sh
#!/bin/bash

echo "Starting React development server..."

# Install dependencies if needed
if [ ! -d "node_modules" ]; then
  echo "Installing dependencies..."
  npm install
fi

# Start the development server
npm run dev
```

```
#!/bin/bash
# project-root/start-all.sh
#!/bin/bash

echo "========================================="
echo "Starting LE Alert Correlation System"
echo "========================================="

echo ""
echo "Step 1: Starting infrastructure services..."
docker-compose up -d --wait

echo ""
echo "Step 2: Starting backend services..."
cd backend
./scripts/start-dev.sh &
BACKEND_PID=$!
cd ..

echo ""
echo "Step 3: Starting React frontend..."
cd frontend
npm install
npm run dev &
FRONTEND_PID=$!
cd ..

echo ""
echo "========================================="
echo "System is starting up!"
echo ""
echo "Access URLs:"
echo "  Frontend:    http://localhost:3000"
echo "  API Gateway: http://localhost:8080"
echo "  Grafana:     http://localhost:3001"
echo "  Prometheus:  http://localhost:9090"
echo ""
echo "Default login:"
echo "  Username: admin"
echo "  Password: admin123"
echo ""
echo "Press Ctrl+C to stop all services"
echo "========================================="

# Wait for termination
trap "echo 'Stopping services...'; kill $BACKEND_PID $FRONTEND_PID; docker-compose down; exit" INT TERM
wait
```

## How to Run /frontend

```
# 1. Navigate to frontend directory
cd frontend

# 2. Install dependencies (first time only)
npm install

# 3. Configure environment
cp .env.example .env
# Edit .env file with your settings

# 4. Start the React app
npm run dev
# OR
npm start

# 5. Open browser to http://localhost:3000
```
