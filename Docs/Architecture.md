# System Architecture

## Major Components

### 1. Frontend
Responsible for:
- Trading UI
- Order book display
- Order placement/cancellation
- Positions and balances
- Real-time WebSocket updates

### 2. API Server
Responsible for:
- Authentication
- Request validation
- Order APIs
- Account APIs
- Market APIs
- Position/history APIs
- WebSocket connections
- Authorization

### 3. Matching Engine
Responsible for:
- Maintaining the in-memory order book
- Price-time priority matching
- Generating trades
- Updating order execution state

### 4. PostgreSQL
Responsible for:
- Users
- Accounts/balances
- Orders
- Trades
- Positions
- Balance transactions
- Persistent authoritative state

### 5. Redis
Responsible for:
- Caching
- Real-time/shared state where appropriate
- Pub/Sub or event distribution where required

### 6. WebSocket Layer
Responsible for:
- Public market updates
- Private user updates
- Order/trade notifications
- Balance/position updates
- Client reconnection handling

## Component Communication

```text
Frontend
   |
   | REST
   v
API Server
   |
   | Order Commands
   v
Matching Engine
   |
   | Trades / Order Updates
   v
API Server
   |
   +---------> PostgreSQL
   |
   +---------> Redis
   |
   +---------> WebSocket Clients