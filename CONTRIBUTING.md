# Contributing to CelebConnect Backend

Thank you for your interest in contributing to CelebConnect! This guide will help you get started with contributing to our backend API.

## 🚀 Getting Started

### Prerequisites

- Node.js 18.x or higher
- PostgreSQL 14.x or higher
- Redis 7.x or higher
- Docker (optional, for containerized development)

### Setup Instructions

1. **Fork the repository**
   ```bash
   # Fork on GitHub and clone your fork
   git clone https://github.com/YOUR_USERNAME/celebconnect-backend.git
   cd celebconnect-backend
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   ```bash
   cp .env.example .env
   # Edit .env with your local configuration
   ```

4. **Start development services**
   ```bash
   # Using Docker (recommended)
   docker-compose up -d postgres redis
   
   # Or start services manually
   # Start PostgreSQL and Redis locally
   ```

5. **Run database migrations**
   ```bash
   npm run migration:run
   ```

6. **Seed the database**
   ```bash
   npm run seed
   ```

7. **Start development server**
   ```bash
   npm run start:dev
   ```

## 🏗️ Development Workflow

### Branch Strategy

- `main` - Production-ready code
- `develop` - Integration branch for features
- `feature/*` - Individual feature branches
- `hotfix/*` - Critical bug fixes

### Creating a Feature Branch

```bash
# Create and switch to a new feature branch
git checkout -b feature/amazing-feature

# Make your changes
git add .
git commit -m "feat: add amazing feature"

# Push to your fork
git push origin feature/amazing-feature

# Create a pull request
```

### Commit Message Convention

We follow [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

Types:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

Examples:
```
feat(auth): add OAuth2 integration with Google
fix(wallet): resolve transaction signing issue
docs(api): update authentication endpoints
```

## 🧪 Testing

### Running Tests

```bash
# Run all tests
npm run test

# Run tests with coverage
npm run test:cov

# Run tests in watch mode
npm run test:watch

# Run specific test file
npm test -- auth/auth.service.spec.ts
```

### Writing Tests

- Unit tests should test individual functions/classes
- Integration tests should test API endpoints
- E2E tests should test complete user flows
- Aim for 90%+ test coverage

### Test Structure

```typescript
// Example test file
import { Test, TestingModule } from '@nestjs/testing';
import { AuthService } from './auth.service';

describe('AuthService', () => {
  let service: AuthService;

  beforeEach(async () => {
    const module: TestingModule = await Test.createTestingModule({
      providers: [AuthService],
    }).compile();

    service = module.get<AuthService>(AuthService);
  });

  it('should be defined', () => {
    expect(service).toBeDefined();
  });

  describe('validateUser', () => {
    it('should return user for valid credentials', async () => {
      const result = await service.validateUser('test@example.com', 'password');
      expect(result).toBeDefined();
      expect(result.email).toBe('test@example.com');
    });

    it('should throw error for invalid credentials', async () => {
      await expect(
        service.validateUser('invalid@example.com', 'wrong-password')
      ).rejects.toThrow('Invalid credentials');
    });
  });
});
```

## 📝 Code Style

### TypeScript Configuration

We use strict TypeScript configuration:
- All functions must have return types
- No implicit any types
- Strict null checks enabled
- All imports must be used

### ESLint & Prettier

```bash
# Check linting
npm run lint

# Auto-fix linting issues
npm run lint -- --fix

# Format code
npm run format
```

### Code Formatting Rules

- Use 2 spaces for indentation
- Use single quotes for strings
- No trailing semicolons (except where required)
- Maximum line length: 100 characters
- Use meaningful variable and function names

## 🔒 Security

### Security Best Practices

1. **Never commit secrets or API keys**
2. **Validate all user inputs**
3. **Use parameterized queries**
4. **Implement proper error handling**
5. **Follow principle of least privilege**

### Security Review Process

All code changes undergo security review:
- Automated vulnerability scanning
- Manual security review for sensitive changes
- Dependency vulnerability checks
- Penetration testing for major features

## 📚 Documentation

### API Documentation

- Use Swagger/OpenAPI for API documentation
- Document all endpoints with examples
- Include error responses
- Keep documentation up to date

### Code Documentation

```typescript
/**
 * Authenticates a user with email and password
 * @param email User's email address
 * @param password User's password
 * @returns Promise<User> User object with authentication token
 * @throws UnauthorizedException for invalid credentials
 * @example
 * ```typescript
 * const user = await authService.login('user@example.com', 'password123');
 * ```
 */
async login(email: string, password: string): Promise<User> {
  // Implementation
}
```

## 🚀 Deployment

### Pre-deployment Checklist

- [ ] All tests pass
- [ ] Code coverage is 90%+
- [ ] No security vulnerabilities
- [ ] Documentation is updated
- [ ] Environment variables are configured
- [ ] Database migrations are tested

### Deployment Process

1. **Development**: Auto-deploy from `develop` branch
2. **Staging**: Manual deployment after PR approval
3. **Production**: Manual deployment with approval

## 🤝 Pull Request Process

### Creating a Pull Request

1. **Update documentation** if needed
2. **Add tests** for new functionality
3. **Ensure all tests pass**
4. **Update CHANGELOG.md** if applicable
5. **Create PR** with descriptive title and description

### PR Template

```markdown
## Description
Brief description of changes made.

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] Tests added/updated
- [ ] No breaking changes (or documented)
```

### Review Process

- **Automated checks** must pass
- **Code review** required from at least 2 maintainers
- **Security review** for sensitive changes
- **Testing** must pass on all environments

## 🐛 Bug Reports

### Reporting Bugs

1. **Use the issue template** for bug reports
2. **Provide detailed information**:
   - Steps to reproduce
   - Expected behavior
   - Actual behavior
   - Environment details
   - Screenshots if applicable

3. **Include logs** and error messages
4. **Search existing issues** before creating new ones

## 💡 Feature Requests

### Requesting Features

1. **Check roadmap** for planned features
2. **Use the feature request template**
3. **Provide clear use case** and requirements
4. **Consider implementation complexity**
5. **Offer to contribute** if possible

## 📞 Getting Help

### Resources

- **Documentation**: [API Docs](https://docs.celebconnect.com)
- **Discord**: [Community Server](https://discord.gg/celebconnect)
- **Issues**: [GitHub Issues](https://github.com/Legacy-Protocol/celebconnect-backend/issues)
- **Email**: backend@celebconnect.com

### Code of Conduct

We are committed to providing a welcoming and inclusive environment. Please read our [Code of Conduct](CODE_OF_CONDUCT.md) and help us maintain a positive community.

## 🎉 Recognition

Contributors are recognized through:
- **GitHub contributor stats**
- **Release notes mentions**
- **Community spotlights**
- **Swag and rewards** for significant contributions

Thank you for contributing to CelebConnect! 🚀
