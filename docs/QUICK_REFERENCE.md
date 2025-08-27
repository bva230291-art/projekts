# Documentation Quick Reference

A quick reference guide for common documentation patterns and best practices.

## 📝 Common Documentation Patterns

### Function Documentation

#### JavaScript/TypeScript
```javascript
/**
 * @function functionName
 * @description Brief description
 * @param {string} param1 - Description
 * @param {Object} options - Options object
 * @param {boolean} options.key - Option description
 * @returns {Promise<Object>} Return description
 * @throws {Error} When error occurs
 * @example
 * const result = await functionName('value', { key: true });
 * @since 1.0.0
 */
```

#### Python
```python
def function_name(param1: str, options: dict = None) -> dict:
    """
    Brief description.
    
    Args:
        param1 (str): Description
        options (dict, optional): Options. Defaults to None.
            - key (bool): Option description
    
    Returns:
        dict: Return description
        
    Raises:
        ValueError: When error occurs
        
    Example:
        >>> result = function_name('value', {'key': True})
        
    Since:
        1.0.0
    """
```

#### Java
```java
/**
 * Brief description.
 * 
 * @param param1 Description
 * @param options Options object
 * @return Return description
 * @throws IllegalArgumentException When error occurs
 * @since 1.0.0
 */
public Object functionName(String param1, Map<String, Object> options) {
    // Implementation
}
```

### Component Documentation

#### React
```jsx
/**
 * @component ComponentName
 * @description Brief description
 * 
 * @param {Object} props - Component props
 * @param {string} props.title - Title description
 * @param {Function} props.onClick - Click handler
 * @param {React.ReactNode} props.children - Child elements
 * 
 * @example
 * <ComponentName title="Hello" onClick={handleClick}>
 *   <p>Content</p>
 * </ComponentName>
 * 
 * @accessibility
 * - Keyboard navigation support
 * - Screen reader friendly
 * 
 * @since 1.0.0
 */
```

#### Vue
```vue
<script>
/**
 * ComponentName - Brief description
 * 
 * @example
 * <ComponentName title="Hello" @click="handleClick">
 *   <p>Content</p>
 * </ComponentName>
 * 
 * @accessibility
 * - Keyboard navigation support
 * - Screen reader friendly
 * 
 * @since 1.0.0
 */
export default {
  name: 'ComponentName',
  props: {
    /** Title description */
    title: {
      type: String,
      required: true
    }
  },
  emits: ['click']
}
</script>
```

#### Angular
```typescript
/**
 * ComponentName - Brief description
 * 
 * @example
 * <app-component-name title="Hello" (click)="handleClick($event)">
 *   <p>Content</p>
 * </app-component-name>
 * 
 * @accessibility
 * - Keyboard navigation support
 * - Screen reader friendly
 * 
 * @since 1.0.0
 */
@Component({
  selector: 'app-component-name',
  templateUrl: './component-name.component.html'
})
export class ComponentNameComponent {
  /** Title description */
  @Input() title!: string;
  
  @Output() click = new EventEmitter<void>();
}
```

### API Endpoint Documentation

#### REST API
```markdown
## POST /api/resource

Creates a new resource.

### Request Body
```json
{
  "name": "string",
  "description": "string",
  "metadata": {
    "key": "value"
  }
}
```

### Response
```json
{
  "success": true,
  "data": {
    "id": "string",
    "name": "string",
    "created_at": "datetime"
  }
}
```

### Error Responses
- `400 Bad Request` - Invalid input data
- `401 Unauthorized` - Missing or invalid API key
- `409 Conflict` - Resource already exists

### Example
```bash
curl -X POST /api/resource \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"name": "Example", "description": "Test resource"}'
```
```

#### GraphQL
```graphql
"""
Creates a new resource.
"""
type Mutation {
  createResource(input: CreateResourceInput!): CreateResourcePayload!
}

"""
Input for creating a resource.
"""
input CreateResourceInput {
  """The name of the resource."""
  name: String!
  
  """Optional description."""
  description: String
  
  """Additional metadata."""
  metadata: JSON
}

"""
Response for creating a resource.
"""
type CreateResourcePayload {
  """The created resource."""
  resource: Resource!
  
  """Success status."""
  success: Boolean!
}

"""
Example query:
mutation CreateResource($input: CreateResourceInput!) {
  createResource(input: $input) {
    success
    resource {
      id
      name
      createdAt
    }
  }
}
"""
```

## 🎨 CSS Documentation

### BEM Methodology
```scss
// Block
.component-name {
  // Base styles
  
  // Modifiers
  &--primary { }
  &--secondary { }
  &--small { }
  &--large { }
  
  // Elements
  &__title { }
  &__content { }
  &__action {
    &:hover { }
    &:focus { }
    &:disabled { }
  }
}

// Responsive
@media (max-width: 768px) {
  .component-name { }
}

// Dark theme
@media (prefers-color-scheme: dark) {
  .component-name { }
}
```

### CSS Custom Properties
```scss
.component-name {
  --component-padding: 1rem;
  --component-border-radius: 4px;
  --component-background: #ffffff;
  --component-text-color: #333333;
  
  padding: var(--component-padding);
  border-radius: var(--component-border-radius);
  background: var(--component-background);
  color: var(--component-text-color);
}
```

## 🧪 Testing Documentation

### Unit Tests
```javascript
/**
 * @test functionName
 * @description Unit tests for functionName
 */
describe('functionName', () => {
  it('should handle basic case', () => {
    const result = functionName('test');
    expect(result).toBe('expected');
  });

  it('should handle edge case', () => {
    const result = functionName('');
    expect(result).toBe('');
  });

  it('should throw error for invalid input', () => {
    expect(() => functionName(null)).toThrow('Invalid input');
  });
});
```

### Component Tests
```javascript
/**
 * @test ComponentName
 * @description Unit tests for ComponentName component
 */
describe('ComponentName', () => {
  it('renders with title', () => {
    render(<ComponentName title="Test" />);
    expect(screen.getByText('Test')).toBeInTheDocument();
  });

  it('calls onClick when clicked', () => {
    const mockOnClick = jest.fn();
    render(<ComponentName title="Test" onClick={mockOnClick} />);
    
    fireEvent.click(screen.getByRole('button'));
    expect(mockOnClick).toHaveBeenCalled();
  });
});
```

## 📊 Data Structure Documentation

### TypeScript Interfaces
```typescript
/**
 * User data structure
 */
interface User {
  /** Unique identifier */
  id: string;
  
  /** User's full name */
  name: string;
  
  /** Email address */
  email: string;
  
  /** Account creation date */
  createdAt: Date;
  
  /** User preferences */
  preferences: UserPreferences;
  
  /** Account status */
  status: 'active' | 'inactive' | 'suspended';
}

/**
 * User preferences
 */
interface UserPreferences {
  /** Theme preference */
  theme: 'light' | 'dark' | 'auto';
  
  /** Language preference */
  language: string;
  
  /** Notification settings */
  notifications: NotificationSettings;
}
```

### JSON Schema
```json
{
  "type": "object",
  "properties": {
    "id": {
      "type": "string",
      "description": "Unique identifier"
    },
    "name": {
      "type": "string",
      "description": "User's full name",
      "minLength": 1
    },
    "email": {
      "type": "string",
      "format": "email",
      "description": "Email address"
    },
    "createdAt": {
      "type": "string",
      "format": "date-time",
      "description": "Account creation date"
    }
  },
  "required": ["id", "name", "email"],
  "additionalProperties": false
}
```

## 🔧 Configuration Documentation

### Environment Variables
```bash
# Database Configuration
DATABASE_URL=postgresql://user:pass@localhost:5432/dbname
DATABASE_POOL_SIZE=10

# API Configuration
API_PORT=3000
API_HOST=0.0.0.0
API_CORS_ORIGIN=https://example.com

# Authentication
JWT_SECRET=your-secret-key
JWT_EXPIRES_IN=24h

# External Services
REDIS_URL=redis://localhost:6379
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=your-access-key
AWS_SECRET_ACCESS_KEY=your-secret-key
```

### Configuration Objects
```javascript
/**
 * Application configuration
 */
const config = {
  /** Database settings */
  database: {
    /** Connection URL */
    url: process.env.DATABASE_URL,
    /** Connection pool size */
    poolSize: parseInt(process.env.DATABASE_POOL_SIZE) || 10,
    /** Connection timeout in milliseconds */
    timeout: 30000
  },
  
  /** API settings */
  api: {
    /** Server port */
    port: parseInt(process.env.API_PORT) || 3000,
    /** Server host */
    host: process.env.API_HOST || '0.0.0.0',
    /** CORS origin */
    corsOrigin: process.env.API_CORS_ORIGIN || '*'
  },
  
  /** Authentication settings */
  auth: {
    /** JWT secret key */
    jwtSecret: process.env.JWT_SECRET,
    /** JWT expiration time */
    jwtExpiresIn: process.env.JWT_EXPIRES_IN || '24h'
  }
};
```

## 🚀 Performance Documentation

### Performance Notes
```javascript
/**
 * @function expensiveOperation
 * @description Performs expensive operation
 * 
 * @performance
 * - Time Complexity: O(n log n)
 * - Space Complexity: O(n)
 * - Memory usage: ~2x input size
 * - For datasets > 1000 items, consider streaming
 * 
 * @optimization
 * - Uses memoization for repeated calculations
 * - Implements early termination for invalid data
 * - Batches operations to reduce memory pressure
 * 
 * @example
 * const result = expensiveOperation(largeDataset, { batchSize: 100 });
 */
```

### Benchmark Examples
```javascript
/**
 * Performance benchmarks
 * 
 * @benchmark
 * - Small dataset (100 items): ~5ms
 * - Medium dataset (1000 items): ~50ms
 * - Large dataset (10000 items): ~500ms
 * - Memory usage: ~2MB per 1000 items
 * 
 * @optimization-tips
 * - Use streaming for datasets > 10000 items
 * - Implement caching for repeated operations
 * - Consider worker threads for CPU-intensive tasks
 */
```

## 🔒 Security Documentation

### Security Considerations
```javascript
/**
 * @function processUserData
 * @description Processes user data securely
 * 
 * @security
 * - Validates all input data
 * - Sanitizes user content
 * - Uses parameterized queries
 * - Implements rate limiting
 * - Logs security events
 * 
 * @authentication
 * - Requires valid JWT token
 * - Validates user permissions
 * - Implements session management
 * 
 * @authorization
 * - Checks user role permissions
 * - Validates resource ownership
 * - Implements row-level security
 * 
 * @example
 * const result = await processUserData(userData, { userId: '123' });
 */
```

## 📈 Migration Documentation

### Breaking Changes
```javascript
/**
 * @function processData
 * @description Processes data (v2.0.0)
 * 
 * @breaking-changes
 * - Changed return format from object to array
 * - Removed legacy 'format' parameter
 * - Updated error response structure
 * 
 * @migration
 * // Old usage (v1.x)
 * const result = processData(data, { format: 'legacy' });
 * 
 * // New usage (v2.0+)
 * const result = await processData(data, { batchSize: 100 });
 * 
 * @deprecated
 * Legacy format support will be removed in v3.0.0
 * 
 * @since 2.0.0
 */
```

## 🎯 Accessibility Documentation

### Accessibility Guidelines
```javascript
/**
 * @component AccessibleComponent
 * @description Accessible component example
 * 
 * @accessibility
 * - Supports keyboard navigation (Tab, Enter, Space)
 * - Implements ARIA labels and roles
 * - Provides focus management
 * - Supports screen readers
 * - High contrast mode compatible
 * - Respects reduced motion preferences
 * 
 * @aria
 * - role="button" for interactive elements
 * - aria-label for descriptive labels
 * - aria-expanded for expandable content
 * - aria-controls for controlled elements
 * 
 * @keyboard
 * - Tab: Navigate between elements
 * - Enter/Space: Activate buttons
 * - Escape: Close modals/dropdowns
 * - Arrow keys: Navigate lists/options
 * 
 * @example
 * <AccessibleComponent
 *   aria-label="Submit form"
 *   role="button"
 *   tabIndex={0}
 *   onKeyDown={handleKeyDown}
 * >
 *   Submit
 * </AccessibleComponent>
 */
```

---

*This quick reference provides common patterns and examples for consistent documentation across your projects.*