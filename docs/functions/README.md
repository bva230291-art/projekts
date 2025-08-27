# Function Documentation

This section contains documentation for all public functions and methods.

## JavaScript/TypeScript Functions

### Utility Functions

#### `formatDate(date, format)`

Formats a date according to the specified format string.

**Parameters:**
- `date` (Date | string | number): The date to format
- `format` (string): Format string (e.g., 'YYYY-MM-DD', 'MM/DD/YYYY')

**Returns:**
- `string`: Formatted date string

**Throws:**
- `TypeError`: If date parameter is invalid
- `Error`: If format string is invalid

**Example Usage:**
```javascript
import { formatDate } from './utils/date';

// Basic usage
const formatted = formatDate(new Date(), 'YYYY-MM-DD');
console.log(formatted); // "2024-01-01"

// With different formats
formatDate('2024-01-01', 'MM/DD/YYYY'); // "01/01/2024"
formatDate(1640995200000, 'DD-MM-YYYY'); // "01-01-2022"

// With time
formatDate(new Date(), 'YYYY-MM-DD HH:mm:ss'); // "2024-01-01 12:30:45"
```

#### `validateEmail(email)`

Validates an email address using RFC 5322 specification.

**Parameters:**
- `email` (string): Email address to validate

**Returns:**
- `boolean`: True if email is valid, false otherwise

**Example Usage:**
```javascript
import { validateEmail } from './utils/validation';

validateEmail('user@example.com'); // true
validateEmail('invalid.email'); // false
validateEmail('test@domain.co.uk'); // true
validateEmail(''); // false
```

#### `debounce(func, delay, options)`

Creates a debounced function that delays invoking func until after delay milliseconds.

**Parameters:**
- `func` (Function): The function to debounce
- `delay` (number): The number of milliseconds to delay
- `options` (Object, optional): Options object
  - `leading` (boolean): Invoke on the leading edge (default: false)
  - `trailing` (boolean): Invoke on the trailing edge (default: true)

**Returns:**
- `Function`: Debounced function with cancel method

**Example Usage:**
```javascript
import { debounce } from './utils/performance';

// Basic debouncing
const debouncedSearch = debounce((query) => {
  console.log('Searching for:', query);
}, 300);

// Usage in event handler
document.getElementById('search').addEventListener('input', (e) => {
  debouncedSearch(e.target.value);
});

// With leading edge
const debouncedClick = debounce(handleClick, 1000, { leading: true });

// Cancel pending invocation
debouncedSearch.cancel();
```

#### `deepClone(obj)`

Creates a deep copy of an object or array.

**Parameters:**
- `obj` (any): The object to clone

**Returns:**
- `any`: Deep copy of the input object

**Throws:**
- `TypeError`: If object contains circular references
- `Error`: If object contains non-serializable values

**Example Usage:**
```javascript
import { deepClone } from './utils/object';

const original = {
  name: 'John',
  address: {
    street: '123 Main St',
    city: 'Anytown'
  },
  hobbies: ['reading', 'coding']
};

const copy = deepClone(original);
copy.address.city = 'New City';

console.log(original.address.city); // "Anytown" (unchanged)
console.log(copy.address.city); // "New City"
```

### API Helper Functions

#### `apiRequest(endpoint, options)`

Makes HTTP requests to API endpoints with automatic error handling and retries.

**Parameters:**
- `endpoint` (string): API endpoint URL
- `options` (Object, optional): Request options
  - `method` (string): HTTP method (default: 'GET')
  - `headers` (Object): Request headers
  - `body` (any): Request body
  - `timeout` (number): Request timeout in ms (default: 5000)
  - `retries` (number): Number of retry attempts (default: 3)
  - `retryDelay` (number): Delay between retries in ms (default: 1000)

**Returns:**
- `Promise<Object>`: Response data

**Throws:**
- `NetworkError`: If network request fails
- `TimeoutError`: If request times out
- `ApiError`: If API returns error response

**Example Usage:**
```javascript
import { apiRequest } from './api/client';

// GET request
try {
  const users = await apiRequest('/users');
  console.log(users);
} catch (error) {
  console.error('Failed to fetch users:', error.message);
}

// POST request
const newUser = await apiRequest('/users', {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer token'
  },
  body: {
    name: 'John Doe',
    email: 'john@example.com'
  }
});

// With custom timeout and retries
const data = await apiRequest('/slow-endpoint', {
  timeout: 10000,
  retries: 5,
  retryDelay: 2000
});
```

#### `buildQueryString(params)`

Builds a URL query string from an object of parameters.

**Parameters:**
- `params` (Object): Object containing query parameters

**Returns:**
- `string`: URL-encoded query string

**Example Usage:**
```javascript
import { buildQueryString } from './utils/url';

const params = {
  page: 1,
  limit: 10,
  search: 'john doe',
  active: true,
  tags: ['tech', 'programming']
};

const queryString = buildQueryString(params);
console.log(queryString); // "page=1&limit=10&search=john%20doe&active=true&tags=tech&tags=programming"

// Usage with fetch
const url = `https://api.example.com/users?${buildQueryString(params)}`;
fetch(url);
```

## Python Functions

### Data Processing Functions

#### `clean_data(df, options=None)`

Cleans and preprocesses a pandas DataFrame.

**Parameters:**
- `df` (pandas.DataFrame): Input DataFrame to clean
- `options` (dict, optional): Cleaning options
  - `remove_duplicates` (bool): Remove duplicate rows (default: True)
  - `handle_missing` (str): How to handle missing values ('drop', 'fill', 'interpolate')
  - `fill_value` (any): Value to use when filling missing data
  - `normalize_strings` (bool): Normalize string columns (default: True)

**Returns:**
- `pandas.DataFrame`: Cleaned DataFrame

**Raises:**
- `ValueError`: If invalid options are provided
- `TypeError`: If input is not a DataFrame

**Example Usage:**
```python
import pandas as pd
from utils.data import clean_data

# Basic usage
df = pd.DataFrame({
    'name': ['John Doe', 'jane smith', None],
    'age': [25, None, 30],
    'email': ['john@example.com', 'JANE@EXAMPLE.COM', 'bob@test.com']
})

cleaned_df = clean_data(df)
print(cleaned_df)

# With custom options
cleaned_df = clean_data(df, {
    'handle_missing': 'fill',
    'fill_value': {'age': 0, 'name': 'Unknown'},
    'normalize_strings': True
})
```

#### `validate_schema(data, schema)`

Validates data against a JSON schema.

**Parameters:**
- `data` (dict): Data to validate
- `schema` (dict): JSON schema definition

**Returns:**
- `tuple`: (is_valid: bool, errors: list)

**Example Usage:**
```python
from utils.validation import validate_schema

schema = {
    "type": "object",
    "properties": {
        "name": {"type": "string", "minLength": 1},
        "age": {"type": "integer", "minimum": 0},
        "email": {"type": "string", "format": "email"}
    },
    "required": ["name", "email"]
}

data = {
    "name": "John Doe",
    "age": 25,
    "email": "john@example.com"
}

is_valid, errors = validate_schema(data, schema)
if is_valid:
    print("Data is valid!")
else:
    print("Validation errors:", errors)
```

### Machine Learning Functions

#### `train_model(X, y, model_type='random_forest', **kwargs)`

Trains a machine learning model with the given data.

**Parameters:**
- `X` (array-like): Feature matrix
- `y` (array-like): Target vector
- `model_type` (str): Type of model to train ('random_forest', 'svm', 'neural_network')
- `**kwargs`: Additional parameters for the model

**Returns:**
- `tuple`: (trained_model, metrics: dict)

**Raises:**
- `ValueError`: If invalid model_type is provided
- `Exception`: If training fails

**Example Usage:**
```python
from sklearn.datasets import load_iris
from ml.models import train_model

# Load sample data
X, y = load_iris(return_X_y=True)

# Train random forest
model, metrics = train_model(X, y, model_type='random_forest', n_estimators=100)
print(f"Accuracy: {metrics['accuracy']:.2f}")

# Train SVM with custom parameters
model, metrics = train_model(X, y, model_type='svm', C=1.0, kernel='rbf')

# Train neural network
model, metrics = train_model(
    X, y, 
    model_type='neural_network',
    hidden_layer_sizes=(100, 50),
    max_iter=1000
)
```

## Go Functions

### HTTP Handler Functions

#### `HandleUserCreate(w http.ResponseWriter, r *http.Request)`

HTTP handler for creating new users.

**Parameters:**
- `w` (http.ResponseWriter): HTTP response writer
- `r` (*http.Request): HTTP request

**Request Body:**
```json
{
  "username": "string",
  "email": "string",
  "password": "string"
}
```

**Response:**
- Status 201: User created successfully
- Status 400: Invalid request data
- Status 409: User already exists
- Status 500: Internal server error

**Example Usage:**
```go
package main

import (
    "net/http"
    "github.com/gorilla/mux"
)

func main() {
    r := mux.NewRouter()
    r.HandleFunc("/users", HandleUserCreate).Methods("POST")
    
    http.ListenAndServe(":8080", r)
}

// Test with curl
// curl -X POST http://localhost:8080/users \
//   -H "Content-Type: application/json" \
//   -d '{"username":"john","email":"john@example.com","password":"secret"}'
```

#### `ValidateToken(token string) (*User, error)`

Validates a JWT token and returns the associated user.

**Parameters:**
- `token` (string): JWT token to validate

**Returns:**
- `*User`: User associated with the token
- `error`: Error if validation fails

**Example Usage:**
```go
package auth

import (
    "errors"
    "github.com/dgrijalva/jwt-go"
)

func AuthMiddleware(next http.HandlerFunc) http.HandlerFunc {
    return func(w http.ResponseWriter, r *http.Request) {
        token := r.Header.Get("Authorization")
        if token == "" {
            http.Error(w, "Missing token", http.StatusUnauthorized)
            return
        }
        
        user, err := ValidateToken(token)
        if err != nil {
            http.Error(w, "Invalid token", http.StatusUnauthorized)
            return
        }
        
        // Add user to request context
        ctx := context.WithValue(r.Context(), "user", user)
        next.ServeHTTP(w, r.WithContext(ctx))
    }
}
```

### Database Functions

#### `ConnectDB(config *Config) (*sql.DB, error)`

Establishes a connection to the database.

**Parameters:**
- `config` (*Config): Database configuration

**Returns:**
- `*sql.DB`: Database connection
- `error`: Error if connection fails

**Example Usage:**
```go
package database

import (
    "database/sql"
    _ "github.com/lib/pq"
)

type Config struct {
    Host     string
    Port     int
    User     string
    Password string
    DBName   string
    SSLMode  string
}

func main() {
    config := &Config{
        Host:     "localhost",
        Port:     5432,
        User:     "postgres",
        Password: "password",
        DBName:   "myapp",
        SSLMode:  "disable",
    }
    
    db, err := ConnectDB(config)
    if err != nil {
        log.Fatal("Failed to connect to database:", err)
    }
    defer db.Close()
    
    // Use database connection
    rows, err := db.Query("SELECT * FROM users")
    if err != nil {
        log.Fatal("Query failed:", err)
    }
    defer rows.Close()
}
```

## Performance Considerations

### Caching
- Use memoization for expensive computations
- Implement appropriate cache invalidation strategies
- Consider memory usage when caching large datasets

### Async Operations
- Use async/await for I/O operations in JavaScript
- Implement proper error handling for async functions
- Consider using Promise.all() for parallel operations

### Database Queries
- Use prepared statements to prevent SQL injection
- Implement connection pooling for better performance
- Add appropriate database indexes

### Memory Management
- Clean up event listeners and timers
- Avoid memory leaks in long-running processes
- Use weak references where appropriate

## Testing Examples

### Unit Tests (JavaScript)
```javascript
// utils.test.js
import { formatDate, validateEmail } from './utils';

describe('formatDate', () => {
  test('formats date correctly', () => {
    const date = new Date('2024-01-01');
    expect(formatDate(date, 'YYYY-MM-DD')).toBe('2024-01-01');
  });
  
  test('throws error for invalid date', () => {
    expect(() => formatDate('invalid', 'YYYY-MM-DD')).toThrow(TypeError);
  });
});

describe('validateEmail', () => {
  test('validates correct email', () => {
    expect(validateEmail('test@example.com')).toBe(true);
  });
  
  test('rejects invalid email', () => {
    expect(validateEmail('invalid-email')).toBe(false);
  });
});
```

### Integration Tests (Python)
```python
# test_api.py
import pytest
from api.client import ApiClient

@pytest.fixture
def api_client():
    return ApiClient(base_url='http://localhost:8000', api_key='test-key')

def test_create_user(api_client):
    user_data = {
        'username': 'testuser',
        'email': 'test@example.com',
        'password': 'password123'
    }
    
    response = api_client.create_user(user_data)
    
    assert response.status_code == 201
    assert response.json()['username'] == 'testuser'

def test_get_users(api_client):
    response = api_client.get_users(page=1, limit=10)
    
    assert response.status_code == 200
    assert 'users' in response.json()
    assert isinstance(response.json()['users'], list)
```