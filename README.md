# CelebConnect Backend API

[![CI/CD](https://github.com/Legacy-Protocol/celebconnect-backend/workflows/CI/badge.svg)](https://github.com/Legacy-Protocol/celebconnect-backend/actions)
[![Coverage](https://codecov.io/gh/Legacy-Protocol/celebconnect-backend/branch/main/graph/badge.svg)](https://codecov.io/gh/Legacy-Protocol/celebconnect-backend)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-4.9+-blue.svg)](https://www.typescriptlang.org/)

A scalable, enterprise-grade NestJS backend for the CelebConnect platform, featuring account abstraction, real-time features, and Stellar blockchain integration.

## 🚀 Features

### Core Features
- **Account Abstraction**: Seamless Web3 onboarding with social login
- **Stellar Integration**: Complete blockchain transaction management
- **Real-time Communication**: WebSocket support for live updates
- **Multi-tenant Architecture**: Scalable for millions of users
- **Advanced Security**: Military-grade encryption and authentication

### Desktop-First Optimizations
- **Batch Processing**: Optimized for desktop bandwidth
- **Real-time Updates**: Instant notifications and live leaderboards
- **Advanced Analytics**: Desktop-optimized data processing
- **Background Jobs**: Efficient async processing
- **Caching Strategy**: Redis-based performance optimization

## 📋 Prerequisites

- **Node.js**: 18.x or higher
- **PostgreSQL**: 14.x or higher
- **Redis**: 7.x or higher
- **Stellar CLI**: Latest version
- **Docker**: Latest version (for containerization)

## 🛠️ Installation

### Local Development

```bash
# Clone the repository
git clone https://github.com/Legacy-Protocol/celebconnect-backend.git
cd celebconnect-backend

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env

# Start PostgreSQL and Redis
docker-compose up -d postgres redis

# Run database migrations
npm run migration:run

# Seed the database
npm run seed

# Start development server
npm run start:dev
```

### Docker Development

```bash
# Build and start all services
docker-compose up --build

# View logs
docker-compose logs -f backend

# Stop services
docker-compose down
```

## 🏗️ Architecture

### Project Structure
```
src/
├── auth/                    # Authentication & authorization
│   ├── auth.controller.ts
│   ├── auth.service.ts
│   ├── auth.module.ts
│   ├── strategies/          # OAuth strategies
│   └── dto/               # Auth DTOs
├── users/                  # User management
│   ├── user.entity.ts
│   ├── users.controller.ts
│   ├── users.service.ts
│   └── users.module.ts
├── wallets/               # Wallet & account abstraction
│   ├── wallet.entity.ts
│   ├── wallets.controller.ts
│   ├── wallets.service.ts
│   └── wallets.module.ts
├── stellar/               # Stellar blockchain integration
│   ├── stellar.service.ts
│   ├── stellar.module.ts
│   └── contracts/         # Smart contract interactions
├── gifts/                 # Gift system
│   ├── gift.entity.ts
│   ├── gifts.controller.ts
│   ├── gifts.service.ts
│   └── gifts.module.ts
├── celebrities/           # Celebrity management
│   ├── celebrity.entity.ts
│   ├── celebrities.controller.ts
│   ├── celebrities.service.ts
│   └── celebrities.module.ts
├── rewards/              # Reward system
│   ├── reward.entity.ts
│   ├── rewards.controller.ts
│   ├── rewards.service.ts
│   └── rewards.module.ts
├── notifications/        # Real-time notifications
│   ├── notifications.gateway.ts
│   ├── notifications.service.ts
│   └── notifications.module.ts
├── analytics/            # Analytics & metrics
│   ├── analytics.service.ts
│   ├── analytics.controller.ts
│   └── analytics.module.ts
├── common/              # Shared utilities
│   ├── decorators/
│   ├── guards/
│   ├── interceptors/
│   ├── pipes/
│   └── filters/
├── config/              # Configuration files
│   ├── database.config.ts
│   ├── stellar.config.ts
│   └── redis.config.ts
└── app.module.ts        # Root module
```

### Architecture Patterns
- **Clean Architecture**: Separation of concerns
- **Domain-Driven Design**: Business logic isolation
- **CQRS**: Command Query Responsibility Segregation
- **Event-Driven**: Async event processing
- **Microservices**: Modular, scalable design

## 🔧 Configuration

### Environment Variables

```env
# Application
NODE_ENV=development
PORT=8000
API_PREFIX=api/v1

# Database
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_USERNAME=celebconnect
DATABASE_PASSWORD=your_password
DATABASE_NAME=celebconnect

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_PASSWORD=your_redis_password

# JWT
JWT_SECRET=your-super-secret-jwt-key
JWT_EXPIRES_IN=7d
JWT_REFRESH_SECRET=your-refresh-secret
JWT_REFRESH_EXPIRES_IN=30d

# Stellar
STELLAR_NETWORK=public
STELLAR_HORIZON_URL=https://horizon.stellar.org
STELLAR_TREASURY_SECRET_KEY=your-treasury-secret-key
PLATFORM_ENCRYPTION_SECRET=your-platform-encryption-secret

# OAuth Providers
GOOGLE_CLIENT_ID=your-google-client-id
GOOGLE_CLIENT_SECRET=your-google-client-secret
FACEBOOK_APP_ID=your-facebook-app-id
FACEBOOK_APP_SECRET=your-facebook-app-secret
TWITTER_CONSUMER_KEY=your-twitter-consumer-key
TWITTER_CONSUMER_SECRET=your-twitter-consumer-secret

# File Storage
AWS_ACCESS_KEY_ID=your-aws-access-key
AWS_SECRET_ACCESS_KEY=your-aws-secret-key
AWS_REGION=us-east-1
AWS_S3_BUCKET=celebconnect-uploads

# Email
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password

# Monitoring
SENTRY_DSN=your-sentry-dsn
LOG_LEVEL=info
```

## 📚 API Documentation

### Authentication Endpoints

```typescript
// Social Login
POST /api/v1/auth/google
POST /api/v1/auth/facebook
POST /api/v1/auth/twitter

// Token Management
POST /api/v1/auth/refresh
DELETE /api/v1/auth/logout
```

### User Management

```typescript
// User Profile
GET /api/v1/users/profile
PUT /api/v1/users/profile
DELETE /api/v1/users/account

// User Preferences
GET /api/v1/users/preferences
PUT /api/v1/users/preferences
```

### Wallet Operations

```typescript
// Wallet Management
GET /api/v1/wallets/balance
GET /api/v1/wallets/transactions
POST /api/v1/wallets/fund

// Transaction Signing
POST /api/v1/wallets/sign
POST /api/v1/wallets/execute
```

### Gift System

```typescript
// Send Gifts
POST /api/v1/gifts/send
GET /api/v1/gifts/history
GET /api/v1/gifts/analytics

// Gift Categories
GET /api/v1/gifts/categories
GET /api/v1/gifts/popular
```

### Celebrity Management

```typescript
// Celebrity Profiles
GET /api/v1/celebrities
GET /api/v1/celebrities/:id
POST /api/v1/celebrities/:id/follow

// Celebrity Rewards
GET /api/v1/celebrities/:id/rewards
POST /api/v1/celebrities/:id/rewards/claim
```

## 🔄 Real-time Features

### WebSocket Events

```typescript
// Client Events
'join_celebrity_room'     // Join celebrity updates
'leave_celebrity_room'     // Leave celebrity updates
'send_gift'               // Send gift notification
'claim_reward'             // Claim reward notification

// Server Events
'gift_received'           // New gift received
'reward_unlocked'         // New reward available
'leaderboard_updated'     // Leaderboard change
'celebrity_online'       // Celebrity status update
```

### Server-Sent Events

```typescript
// Real-time Updates
/api/v1/stream/gifts/:celebrityId     // Live gift feed
/api/v1/stream/leaderboard/:celebrityId // Live leaderboard
/api/v1/stream/notifications/:userId     // User notifications
```

## 🧪 Testing

### Unit Tests
```bash
# Run all unit tests
npm run test

# Run with coverage
npm run test:cov

# Run specific test file
npm run test -- auth/auth.service.spec.ts
```

### Integration Tests
```bash
# Run integration tests
npm run test:e2e

# Run with specific test
npm run test:e2e -- gifts.e2e-spec.ts
```

### Test Database
```bash
# Setup test database
npm run test:db:setup

# Reset test database
npm run test:db:reset
```

## 🚀 Deployment

### Production Build
```bash
# Build for production
npm run build

# Start production server
npm run start:prod
```

### Docker Deployment
```bash
# Build Docker image
docker build -t celebconnect-backend .

# Run with Docker
docker run -p 8000:8000 celebconnect-backend
```

### Kubernetes Deployment
```bash
# Deploy to Kubernetes
kubectl apply -f k8s/

# Check deployment status
kubectl get pods -l app=celebconnect-backend
```

## 📊 Monitoring & Logging

### Application Monitoring
- **Health Checks**: `/health`, `/ready`, `/live`
- **Metrics**: Prometheus metrics endpoint
- **Tracing**: Jaeger distributed tracing
- **Error Tracking**: Sentry integration

### Logging
```typescript
// Structured logging
import { Logger } from '@nestjs/common';

const logger = new Logger('UserService');
logger.log('User created successfully', { userId: user.id });
logger.error('Failed to create user', error.stack);
```

## 🔒 Security

### Security Features
- **JWT Authentication**: Secure token-based auth
- **Rate Limiting**: API abuse prevention
- **Input Validation**: Comprehensive DTO validation
- **SQL Injection Protection**: TypeORM parameterized queries
- **XSS Protection**: Input sanitization
- **CORS Configuration**: Proper cross-origin setup

### Security Headers
```typescript
// Security middleware
app.use(helmet());
app.use(cors({
  origin: process.env.ALLOWED_ORIGINS?.split(','),
  credentials: true,
}));
```

## 📈 Performance

### Optimization Strategies
- **Database Indexing**: Optimized query performance
- **Redis Caching**: Frequent data caching
- **Connection Pooling**: Database connection management
- **Batch Processing**: Stellar transaction batching
- **Compression**: Gzip response compression

### Performance Monitoring
```typescript
// Performance metrics
import { PerformanceInterceptor } from './common/interceptors/performance.interceptor';

app.useGlobalInterceptors(new PerformanceInterceptor());
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines
- Follow the [Code Style Guide](./docs/CODE_STYLE.md)
- Write comprehensive tests
- Update documentation
- Ensure CI/CD passes

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Support

- **Documentation**: [Wiki](https://github.com/Legacy-Protocol/celebconnect-backend/wiki)
- **Issues**: [GitHub Issues](https://github.com/Legacy-Protocol/celebconnect-backend/issues)
- **Discord**: [Community Server](https://discord.gg/celebconnect)
- **Email**: backend@celebconnect.com

## 🗺️ Roadmap

### v1.0.0 (Current)
- [x] Basic authentication
- [x] Stellar integration
- [x] Gift system
- [x] Real-time updates

### v1.1.0 (Next)
- [ ] Advanced analytics
- [ ] Mobile optimization
- [ ] Enhanced security
- [ ] Performance improvements

### v2.0.0 (Future)
- [ ] Microservices architecture
- [ ] AI-powered features
- [ ] Advanced gamification
- [ ] Enterprise features
