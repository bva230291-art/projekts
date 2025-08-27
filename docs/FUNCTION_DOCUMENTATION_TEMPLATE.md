# Function Documentation Template

This template provides a standardized way to document functions, methods, and procedures across different programming languages.

## Function Documentation Structure

### Basic Function Documentation

```javascript
/**
 * @function functionName
 * @description Brief description of what the function does
 * @param {string} param1 - Description of the first parameter
 * @param {number} param2 - Description of the second parameter
 * @param {Object} options - Configuration options
 * @param {string} options.key1 - Description of option key1
 * @param {boolean} options.key2 - Description of option key2
 * @returns {Promise<Object>} Description of what the function returns
 * @throws {Error} Description of when this error is thrown
 * @example
 * // Basic usage
 * const result = await functionName('value1', 42, { key1: 'option' });
 * 
 * // Advanced usage
 * const result = await functionName('value1', 42, {
 *   key1: 'option',
 *   key2: true
 * });
 * @since 1.0.0
 * @author Your Name
 */
```

### Python Function Documentation

```python
def function_name(param1: str, param2: int, options: dict = None) -> dict:
    """
    Brief description of what the function does.
    
    A more detailed description that can span multiple lines and explain
    the function's purpose, behavior, and usage patterns.
    
    Args:
        param1 (str): Description of the first parameter
        param2 (int): Description of the second parameter
        options (dict, optional): Configuration options. Defaults to None.
            - key1 (str): Description of option key1
            - key2 (bool): Description of option key2
    
    Returns:
        dict: Description of what the function returns
        
    Raises:
        ValueError: Description of when this error is raised
        TypeError: Description of when this error is raised
        
    Example:
        Basic usage:
        >>> result = function_name('value1', 42, {'key1': 'option'})
        
        Advanced usage:
        >>> result = function_name('value1', 42, {
        ...     'key1': 'option',
        ...     'key2': True
        ... })
        
    Note:
        Additional notes about the function's behavior or implementation.
        
    See Also:
        related_function: Description of related function
        
    Since:
        1.0.0
    """
```

### Java Method Documentation

```java
/**
 * Brief description of what the method does.
 * 
 * A more detailed description that can span multiple lines and explain
 * the method's purpose, behavior, and usage patterns.
 * 
 * @param param1 Description of the first parameter
 * @param param2 Description of the second parameter
 * @param options Configuration options
 * @return Description of what the method returns
 * @throws IllegalArgumentException Description of when this exception is thrown
 * @throws NullPointerException Description of when this exception is thrown
 * @since 1.0.0
 * @author Your Name
 * @see RelatedClass#relatedMethod
 */
public Object methodName(String param1, int param2, Map<String, Object> options) {
    // Implementation
}
```

## Function Categories

### Utility Functions

#### String Manipulation
```javascript
/**
 * @function capitalizeFirstLetter
 * @description Capitalizes the first letter of a string
 * @param {string} str - The input string to capitalize
 * @returns {string} The string with the first letter capitalized
 * @example
 * capitalizeFirstLetter('hello world'); // Returns: 'Hello world'
 * capitalizeFirstLetter(''); // Returns: ''
 */
function capitalizeFirstLetter(str) {
    if (!str) return str;
    return str.charAt(0).toUpperCase() + str.slice(1);
}
```

#### Array Operations
```javascript
/**
 * @function chunkArray
 * @description Splits an array into smaller chunks of specified size
 * @param {Array} array - The array to chunk
 * @param {number} size - The size of each chunk
 * @returns {Array<Array>} Array of chunks
 * @example
 * chunkArray([1, 2, 3, 4, 5], 2); // Returns: [[1, 2], [3, 4], [5]]
 * chunkArray([], 3); // Returns: []
 */
function chunkArray(array, size) {
    const chunks = [];
    for (let i = 0; i < array.length; i += size) {
        chunks.push(array.slice(i, i + size));
    }
    return chunks;
}
```

### Data Processing Functions

#### Validation Functions
```javascript
/**
 * @function validateEmail
 * @description Validates if a string is a valid email address
 * @param {string} email - The email address to validate
 * @returns {boolean} True if valid, false otherwise
 * @example
 * validateEmail('user@example.com'); // Returns: true
 * validateEmail('invalid-email'); // Returns: false
 * validateEmail(''); // Returns: false
 */
function validateEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
}
```

#### Data Transformation
```javascript
/**
 * @function transformUserData
 * @description Transforms raw user data into a standardized format
 * @param {Object} rawData - Raw user data from API
 * @param {Object} options - Transformation options
 * @param {boolean} options.includeMetadata - Whether to include metadata
 * @param {string} options.dateFormat - Date format for timestamps
 * @returns {Object} Transformed user data
 * @throws {Error} When rawData is invalid or missing required fields
 * @example
 * const user = transformUserData({
 *   id: 123,
 *   name: 'John Doe',
 *   email: 'john@example.com'
 * }, { includeMetadata: true });
 */
function transformUserData(rawData, options = {}) {
    if (!rawData || !rawData.id) {
        throw new Error('Invalid user data: missing required fields');
    }
    
    const transformed = {
        id: rawData.id,
        name: rawData.name || '',
        email: rawData.email || '',
        createdAt: new Date(rawData.created_at || Date.now())
    };
    
    if (options.includeMetadata) {
        transformed.metadata = {
            transformedAt: new Date(),
            source: 'api'
        };
    }
    
    return transformed;
}
```

### Async Functions

#### API Calls
```javascript
/**
 * @function fetchUserData
 * @description Fetches user data from the API
 * @param {string} userId - The user ID to fetch
 * @param {Object} options - Request options
 * @param {number} options.timeout - Request timeout in milliseconds
 * @param {boolean} options.cache - Whether to use cached data
 * @returns {Promise<Object>} User data object
 * @throws {Error} When the API request fails
 * @throws {Error} When the user is not found
 * @example
 * // Basic usage
 * const user = await fetchUserData('123');
 * 
 * // With options
 * const user = await fetchUserData('123', {
 *   timeout: 5000,
 *   cache: true
 * });
 */
async function fetchUserData(userId, options = {}) {
    const { timeout = 10000, cache = false } = options;
    
    try {
        const response = await fetch(`/api/users/${userId}`, {
            timeout,
            headers: {
                'Cache-Control': cache ? 'max-age=300' : 'no-cache'
            }
        });
        
        if (!response.ok) {
            if (response.status === 404) {
                throw new Error(`User ${userId} not found`);
            }
            throw new Error(`API request failed: ${response.status}`);
        }
        
        return await response.json();
    } catch (error) {
        throw new Error(`Failed to fetch user data: ${error.message}`);
    }
}
```

#### Database Operations
```javascript
/**
 * @function createUser
 * @description Creates a new user in the database
 * @param {Object} userData - User data to create
 * @param {string} userData.name - User's full name
 * @param {string} userData.email - User's email address
 * @param {string} userData.password - User's password (will be hashed)
 * @param {Object} options - Creation options
 * @param {boolean} options.validateEmail - Whether to validate email format
 * @param {boolean} options.sendWelcomeEmail - Whether to send welcome email
 * @returns {Promise<Object>} Created user object (without password)
 * @throws {ValidationError} When user data is invalid
 * @throws {DuplicateError} When email already exists
 * @example
 * const user = await createUser({
 *   name: 'John Doe',
 *   email: 'john@example.com',
 *   password: 'securepassword'
 * }, { validateEmail: true });
 */
async function createUser(userData, options = {}) {
    const { validateEmail = true, sendWelcomeEmail = false } = options;
    
    // Validation
    if (!userData.name || !userData.email || !userData.password) {
        throw new ValidationError('Missing required fields: name, email, password');
    }
    
    if (validateEmail && !validateEmail(userData.email)) {
        throw new ValidationError('Invalid email format');
    }
    
    // Check for existing user
    const existingUser = await db.users.findOne({ email: userData.email });
    if (existingUser) {
        throw new DuplicateError('User with this email already exists');
    }
    
    // Hash password
    const hashedPassword = await bcrypt.hash(userData.password, 10);
    
    // Create user
    const user = await db.users.create({
        ...userData,
        password: hashedPassword,
        createdAt: new Date()
    });
    
    // Send welcome email if requested
    if (sendWelcomeEmail) {
        await sendWelcomeEmail(user.email, user.name);
    }
    
    // Return user without password
    const { password, ...userWithoutPassword } = user;
    return userWithoutPassword;
}
```

## Error Handling Documentation

### Custom Error Classes
```javascript
/**
 * @class ValidationError
 * @description Custom error for validation failures
 * @extends Error
 * @param {string} message - Error message
 * @param {Object} details - Validation details
 * @example
 * throw new ValidationError('Invalid input', { field: 'email', value: 'invalid' });
 */
class ValidationError extends Error {
    constructor(message, details = {}) {
        super(message);
        this.name = 'ValidationError';
        this.details = details;
    }
}

/**
 * @class APIError
 * @description Custom error for API-related failures
 * @extends Error
 * @param {string} message - Error message
 * @param {number} statusCode - HTTP status code
 * @param {Object} response - API response data
 * @example
 * throw new APIError('API request failed', 500, { error: 'Internal server error' });
 */
class APIError extends Error {
    constructor(message, statusCode, response = {}) {
        super(message);
        this.name = 'APIError';
        this.statusCode = statusCode;
        this.response = response;
    }
}
```

## Testing Documentation

### Unit Test Examples
```javascript
/**
 * @function capitalizeFirstLetter
 * @description Capitalizes the first letter of a string
 * @param {string} str - The input string to capitalize
 * @returns {string} The string with the first letter capitalized
 * 
 * @test
 * describe('capitalizeFirstLetter', () => {
 *   it('should capitalize the first letter of a string', () => {
 *     expect(capitalizeFirstLetter('hello')).toBe('Hello');
 *     expect(capitalizeFirstLetter('world')).toBe('World');
 *   });
 *   
 *   it('should handle empty strings', () => {
 *     expect(capitalizeFirstLetter('')).toBe('');
 *   });
 *   
 *   it('should handle single character strings', () => {
 *     expect(capitalizeFirstLetter('a')).toBe('A');
 *   });
 *   
 *   it('should handle already capitalized strings', () => {
 *     expect(capitalizeFirstLetter('Hello')).toBe('Hello');
 *   });
 * });
 */
```

## Performance Considerations

### Optimization Notes
```javascript
/**
 * @function expensiveOperation
 * @description Performs an expensive operation with optimization notes
 * @param {Array} data - Large dataset to process
 * @param {Object} options - Processing options
 * @returns {Array} Processed data
 * 
 * @performance
 * - Time Complexity: O(n log n)
 * - Space Complexity: O(n)
 * - For datasets > 1000 items, consider using streaming
 * - Memory usage: ~2x input size
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

## Migration and Versioning

### Version History
```javascript
/**
 * @function processData
 * @description Processes data with version history
 * @param {Object} data - Data to process
 * @returns {Object} Processed data
 * 
 * @version 2.1.0
 * - Added support for new data format
 * - Improved error handling
 * - Deprecated legacy format support
 * 
 * @version 2.0.0
 * - Breaking change: changed return format
 * - Added async processing support
 * 
 * @version 1.0.0
 * - Initial implementation
 * 
 * @deprecated
 * Legacy format support will be removed in version 3.0.0
 * 
 * @example
 * // Current usage (v2.1.0)
 * const result = await processData({ format: 'new', data: [...] });
 * 
 * // Legacy usage (deprecated)
 * const result = processData(legacyData); // Will be removed in v3.0.0
 */
```

---

*This template provides comprehensive documentation patterns that can be adapted for any programming language or framework.*