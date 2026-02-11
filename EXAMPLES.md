# Usage Examples

This document provides practical examples of how these rules will guide Cursor's AI agent.

## Example 1: Python Code Review

### Scenario
You're writing a Python function and ask Cursor to review it.

### Your Code
```python
def get_user(id):
    try:
        user = db.query(id)
        return user
    except:
        return None
```

### Cursor's Response (Guided by Rules)
The AI will suggest improvements based on `python-standards.mdc`:

```python
def get_user(user_id: str) -> User | None:
    """Retrieve user by ID from database.
    
    Args:
        user_id: Unique identifier for the user
        
    Returns:
        User object if found, None otherwise
        
    Raises:
        DatabaseError: If database connection fails
    """
    try:
        user = db.query(user_id)
        return user
    except UserNotFoundError as e:
        logger.warning(f"User {user_id} not found: {e}")
        return None
    except DatabaseError as e:
        logger.error(f"Database error querying user {user_id}: {e}")
        raise
```

**Changes Applied:**
- ✅ Added type hints
- ✅ Improved parameter naming (`id` → `user_id`)
- ✅ Added Google-style docstring
- ✅ Specific exception handling
- ✅ Proper logging

## Example 2: React Component Creation

### Scenario
You ask Cursor to create a user profile component.

### Cursor's Output (Guided by Rules)

```typescript
interface UserProfileProps {
  userId: string;
  onUpdate?: (user: User) => void;
}

export function UserProfile({ userId, onUpdate }: UserProfileProps) {
  const { user, loading, error } = useUser(userId);
  
  const handleSave = useCallback(
    async (updates: Partial<User>) => {
      try {
        const updated = await userService.update(userId, updates);
        onUpdate?.(updated);
      } catch (err) {
        logger.error('Failed to update user:', err);
      }
    },
    [userId, onUpdate]
  );
  
  if (loading) return <LoadingSpinner />;
  if (error) return <ErrorMessage error={error} />;
  if (!user) return <NotFound />;
  
  return (
    <div className="user-profile">
      <UserCard user={user} onSave={handleSave} />
    </div>
  );
}

// Custom hook extracted per react-patterns.mdc
function useUser(userId: string) {
  const [user, setUser] = useState<User | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);
  
  useEffect(() => {
    let cancelled = false;
    
    async function fetchUser() {
      try {
        const data = await userService.get(userId);
        if (!cancelled) {
          setUser(data);
          setLoading(false);
        }
      } catch (err) {
        if (!cancelled) {
          setError(err as Error);
          setLoading(false);
        }
      }
    }
    
    fetchUser();
    return () => { cancelled = true; };
  }, [userId]);
  
  return { user, loading, error };
}
```

**Rules Applied:**
- ✅ TypeScript interfaces for props
- ✅ Custom hook extraction (`useUser`)
- ✅ Proper error handling
- ✅ `useCallback` for memoization
- ✅ Loading and error states
- ✅ Cleanup in useEffect

## Example 3: Dockerfile Creation

### Scenario
You ask Cursor to create a Dockerfile for a Node.js app.

### Cursor's Output (Guided by Rules)

```dockerfile
# Build stage
FROM node:20-alpine AS builder
WORKDIR /app

# Copy dependency files
COPY package*.json ./
RUN npm ci --only=production

# Copy source and build
COPY . .
RUN npm run build

# Production stage
FROM node:20-alpine
WORKDIR /app

# Create non-root user
RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001

# Copy built assets and dependencies
COPY --from=builder --chown=nodejs:nodejs /app/dist ./dist
COPY --from=builder --chown=nodejs:nodejs /app/node_modules ./node_modules
COPY --from=builder --chown=nodejs:nodejs /app/package.json ./

# Switch to non-root user
USER nodejs

# Expose port and define health check
EXPOSE 3000
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s \
  CMD node -e "require('http').get('http://localhost:3000/health')"

CMD ["node", "dist/index.js"]
```

**Rules Applied:**
- ✅ Multi-stage build
- ✅ Alpine base image
- ✅ Non-root user
- ✅ Proper layer ordering
- ✅ Health check included

## Example 4: Error Handling Improvement

### Scenario
You have a TypeScript API call and ask for error handling improvements.

### Before
```typescript
async function fetchUserData(userId: string) {
  const response = await fetch(`/api/users/${userId}`);
  return response.json();
}
```

### After (Guided by Rules)
```typescript
class UserFetchError extends Error {
  constructor(
    message: string,
    public userId: string,
    public statusCode?: number
  ) {
    super(message);
    this.name = 'UserFetchError';
  }
}

async function fetchUserData(userId: string): Promise<User> {
  try {
    const response = await fetch(`/api/users/${userId}`);
    
    if (!response.ok) {
      logger.error(`Failed to fetch user ${userId}: ${response.status}`);
      throw new UserFetchError(
        `User fetch failed: ${response.statusText}`,
        userId,
        response.status
      );
    }
    
    const data = await response.json();
    return UserSchema.parse(data); // Runtime validation
  } catch (error) {
    if (error instanceof UserFetchError) {
      throw error;
    }
    
    logger.error('Network error fetching user:', error);
    throw new UserFetchError(
      'Network error occurred',
      userId
    );
  }
}
```

**Rules Applied:**
- ✅ Custom error class
- ✅ Explicit return type
- ✅ Proper error handling and logging
- ✅ HTTP status checking
- ✅ Runtime validation

## Example 5: Git Commit Messages

### Scenario
You make changes and ask Cursor to commit them.

### Cursor's Commit Messages (Guided by Rules)

```bash
# Good commit messages following general-standards.mdc
feat: add user authentication with JWT tokens
fix: resolve memory leak in background worker
docs: update API documentation for v2 endpoints
refactor: extract user validation into separate service
test: add integration tests for payment flow
chore: upgrade dependencies to latest versions
```

**Rules Applied:**
- ✅ Conventional commit format
- ✅ Clear, descriptive messages
- ✅ Proper type prefixes

## Example 6: Kubernetes Manifest

### Scenario
You ask Cursor to create a Kubernetes deployment.

### Cursor's Output (Guided by Rules)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  labels:
    app: myapp
    component: backend
    environment: production
    version: "1.0.0"
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
      component: backend
  template:
    metadata:
      labels:
        app: myapp
        component: backend
        environment: production
        version: "1.0.0"
    spec:
      containers:
      - name: app
        image: myapp:1.0.0
        imagePullPolicy: IfNotPresent
        ports:
        - containerPort: 8080
          name: http
        resources:
          requests:
            memory: "128Mi"
            cpu: "100m"
          limits:
            memory: "512Mi"
            cpu: "500m"
        livenessProbe:
          httpGet:
            path: /health
            port: 8080
          initialDelaySeconds: 30
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        readinessProbe:
          httpGet:
            path: /ready
            port: 8080
          initialDelaySeconds: 5
          periodSeconds: 5
          timeoutSeconds: 3
          failureThreshold: 2
        env:
        - name: NODE_ENV
          value: production
        - name: PORT
          value: "8080"
      securityContext:
        runAsNonRoot: true
        runAsUser: 1000
        fsGroup: 1000
```

**Rules Applied:**
- ✅ Resource requests and limits
- ✅ Liveness and readiness probes
- ✅ Consistent labeling
- ✅ Security context (non-root)
- ✅ Proper health check configuration

## How Rules Activate

Rules activate automatically based on context:

| Rule | Activates When |
|------|----------------|
| `general-standards.mdc` | Always (alwaysApply: true) |
| `python-standards.mdc` | Opening any `.py` file |
| `typescript-standards.mdc` | Opening any `.ts` file |
| `react-patterns.mdc` | Opening any `.tsx` or `.jsx` file |
| `docker-kubernetes.mdc` | Opening Dockerfile or k8s YAML files |

## Testing the Rules

To verify rules are working:

1. Copy rules to your project's `.cursor/rules/`
2. Open a file that should activate a rule (e.g., `example.py`)
3. Ask Cursor: "Review this code and suggest improvements"
4. Cursor's suggestions should align with the rule guidelines

---

These examples demonstrate how rules provide consistent, high-quality guidance across your entire development workflow.
