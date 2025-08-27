# Documentation Style Guide

This style guide ensures consistency and quality across all project documentation.

## General Principles

### 1. Clarity First
- Write for your audience (developers, end-users, contributors)
- Use simple, direct language
- Avoid jargon unless necessary (and define it when used)
- Structure information logically

### 2. Consistency
- Use consistent formatting throughout
- Follow established patterns and templates
- Maintain the same tone and style
- Use standardized terminology

### 3. Completeness
- Include all necessary information
- Provide working examples
- Cover edge cases and error scenarios
- Link to related documentation

### 4. Maintainability
- Keep documentation up-to-date with code changes
- Use version control for documentation
- Review and update regularly
- Remove outdated information

## Writing Style

### Tone and Voice
- **Professional but approachable**: Formal enough to be credible, friendly enough to be accessible
- **Active voice**: "Use this function to..." instead of "This function can be used to..."
- **Present tense**: "The API returns..." instead of "The API will return..."
- **Direct and concise**: Get to the point quickly

### Language Guidelines

#### Use Simple Language
```markdown
✅ Good: "This function sorts an array of numbers."
❌ Bad: "This function facilitates the organization of numerical data structures."
```

#### Be Specific
```markdown
✅ Good: "The timeout is 5 seconds."
❌ Bad: "The timeout is a reasonable amount of time."
```

#### Use Active Voice
```markdown
✅ Good: "The server processes the request."
❌ Bad: "The request is processed by the server."
```

#### Avoid Assumptions
```markdown
✅ Good: "Install Node.js version 16 or higher."
❌ Bad: "Obviously, you'll need Node.js installed."
```

## Formatting Standards

### Headers
Use descriptive, hierarchical headers:

```markdown
# Main Title (H1) - Only one per document
## Major Section (H2)
### Subsection (H3)
#### Minor Section (H4)
##### Detail Section (H5)
###### Smallest Section (H6)
```

### Code Formatting

#### Inline Code
Use backticks for:
- Function names: `getUserById()`
- Variable names: `userEmail`
- File names: `config.json`
- Short code snippets: `const user = await User.findById(id)`

#### Code Blocks
Use fenced code blocks with language specification:

```javascript
// Good: Specify language
function getUserById(id) {
  return users.find(user => user.id === id);
}
```

```markdown
// Bad: No language specified
function getUserById(id) {
  return users.find(user => user.id === id);
}
```

#### Code Examples
- Always use complete, working examples
- Include necessary imports and setup
- Show both input and expected output
- Handle common error cases

```javascript
// Complete example with imports
const express = require('express');
const { validateUser } = require('./utils');

const app = express();

app.post('/users', async (req, res) => {
  try {
    const user = await validateUser(req.body);
    // Handle success
    res.status(201).json({ user });
  } catch (error) {
    // Handle error
    res.status(400).json({ error: error.message });
  }
});
```

### Lists

#### Unordered Lists
Use consistent bullet points:
- First item
- Second item
  - Nested item
  - Another nested item
- Third item

#### Ordered Lists
Use for sequential steps:
1. First step
2. Second step
3. Third step

#### Definition Lists
For parameters and properties:
- `parameter` (type): Description of the parameter
- `anotherParam` (type, optional): Description with default value

### Tables
Use tables for structured data:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `id` | number | Yes | User identifier |
| `name` | string | Yes | User's full name |
| `email` | string | No | User's email address |

### Links
- Use descriptive link text: [API Documentation](./api/README.md)
- Avoid generic text like "click here" or "read more"
- Use relative paths for internal links
- Use absolute URLs for external links

### Emphasis
- **Bold** for important terms or UI elements
- *Italic* for emphasis or introducing new concepts
- `Code formatting` for technical terms
- > Blockquotes for important notes or warnings

## Content Structure

### Document Organization

#### Standard Document Structure
1. **Title**: Clear, descriptive title
2. **Overview**: Brief description of purpose
3. **Prerequisites**: What users need before starting
4. **Main Content**: Organized in logical sections
5. **Examples**: Practical usage examples
6. **Reference**: Detailed parameter/option lists
7. **Troubleshooting**: Common issues and solutions
8. **Related Links**: Links to related documentation

#### API Documentation Structure
1. **Overview**: What the API does
2. **Authentication**: How to authenticate
3. **Base URL**: API base URL
4. **Endpoints**: Organized by resource
5. **Error Handling**: Error codes and responses
6. **Rate Limiting**: Usage limits
7. **SDKs**: Available client libraries
8. **Examples**: Complete usage examples

#### Function Documentation Structure
1. **Purpose**: What the function does
2. **Syntax**: Function signature
3. **Parameters**: Input parameters
4. **Return Value**: What it returns
5. **Exceptions**: What errors it might throw
6. **Examples**: Usage examples
7. **Notes**: Important considerations

### Section Guidelines

#### Overview Sections
- Start with the most important information
- Answer "what" and "why" before "how"
- Keep it concise but comprehensive
- Include a simple example if helpful

#### Parameter Documentation
Always include:
- Parameter name and type
- Whether it's required or optional
- Default value (if any)
- Description of what it does
- Valid values or constraints
- Example values

```markdown
### Parameters
- `userId` (string, required): Unique identifier for the user
- `includeProfile` (boolean, optional, default: false): Whether to include user profile data
- `fields` (array of strings, optional): Specific fields to return. Valid values: 'id', 'name', 'email'
```

#### Example Sections
- Provide multiple examples showing different use cases
- Start with the simplest example
- Show both successful and error cases
- Include complete, runnable code
- Explain what each example demonstrates

## Visual Elements

### Callouts and Admonitions
Use consistent formatting for different types of callouts:

> **Note**: General information that might be helpful.

> **Warning**: Important information that could prevent errors.

> **Danger**: Critical information about potential data loss or security issues.

> **Tip**: Helpful suggestions or best practices.

### Diagrams and Images
- Use clear, readable diagrams
- Include alt text for accessibility
- Keep file sizes reasonable
- Use consistent styling across diagrams
- Place images close to relevant text

## Language-Specific Guidelines

### JavaScript/TypeScript
```javascript
// Use modern JavaScript syntax
const users = await User.findAll();

// Show TypeScript types when relevant
interface User {
  id: number;
  name: string;
  email?: string;
}

// Include error handling
try {
  const user = await createUser(userData);
  return user;
} catch (error) {
  console.error('Failed to create user:', error);
  throw error;
}
```

### Python
```python
# Use type hints when helpful
def get_user(user_id: int) -> Optional[User]:
    """Get a user by ID.
    
    Args:
        user_id: The unique identifier for the user
        
    Returns:
        User object if found, None otherwise
        
    Raises:
        ValueError: If user_id is invalid
    """
    if user_id <= 0:
        raise ValueError("user_id must be positive")
    
    return User.objects.filter(id=user_id).first()
```

### Go
```go
// Include package and imports
package main

import (
    "fmt"
    "net/http"
)

// Document function behavior clearly
// GetUser retrieves a user by ID from the database.
// Returns an error if the user is not found or if there's a database error.
func GetUser(id int) (*User, error) {
    if id <= 0 {
        return nil, fmt.Errorf("invalid user ID: %d", id)
    }
    
    // Implementation here
    return user, nil
}
```

## Documentation Maintenance

### Version Control
- Track documentation changes in version control
- Use meaningful commit messages for doc changes
- Tag documentation versions with code releases
- Review documentation in pull requests

### Review Process
1. **Technical Review**: Ensure accuracy and completeness
2. **Editorial Review**: Check grammar, style, and clarity
3. **User Testing**: Verify examples work as described
4. **Accessibility Review**: Ensure content is accessible

### Update Schedule
- **Code Changes**: Update docs immediately with code changes
- **Regular Review**: Monthly review for accuracy and relevance
- **Major Releases**: Comprehensive documentation review
- **User Feedback**: Address documentation issues promptly

### Deprecation Guidelines
When features are deprecated:
1. Mark as deprecated in documentation
2. Explain what to use instead
3. Provide migration guide
4. Include timeline for removal
5. Keep deprecated docs until removal

```markdown
> **Deprecated**: This function is deprecated as of v2.0. Use `newFunction()` instead.
> See the [migration guide](./migration.md) for details. This function will be removed in v3.0.
```

## Accessibility Guidelines

### Writing for Accessibility
- Use clear, simple language
- Provide alternative text for images
- Use descriptive link text
- Structure content with proper headings
- Ensure good color contrast in diagrams

### Screen Reader Considerations
- Use semantic HTML in markdown
- Provide context for code examples
- Describe visual elements in text
- Use lists for related items

## Quality Checklist

Before publishing documentation, verify:

### Content Quality
- [ ] Information is accurate and up-to-date
- [ ] Examples work as described
- [ ] All links function correctly
- [ ] Content is complete and comprehensive
- [ ] Tone is consistent throughout

### Technical Quality
- [ ] Code examples use correct syntax
- [ ] All parameters are documented
- [ ] Error cases are covered
- [ ] Prerequisites are listed
- [ ] Dependencies are specified

### Style and Formatting
- [ ] Headers follow hierarchy rules
- [ ] Code is properly formatted
- [ ] Lists are consistently formatted
- [ ] Tables are well-structured
- [ ] Images have alt text

### User Experience
- [ ] Content is easy to scan
- [ ] Information is logically organized
- [ ] Navigation is clear
- [ ] Examples are practical and relevant
- [ ] Common use cases are covered

## Tools and Resources

### Recommended Tools
- **Markdown Linters**: markdownlint, remark-lint
- **Grammar Checkers**: Grammarly, Hemingway Editor
- **Diagram Tools**: Mermaid, Draw.io, Lucidchart
- **Screenshot Tools**: Consistent screenshot tools for UI documentation

### Useful Resources
- [Markdown Guide](https://www.markdownguide.org/)
- [Writing inclusive documentation](https://developers.google.com/style/inclusive-documentation)
- [Technical writing courses](https://developers.google.com/tech-writing)
- [API documentation best practices](https://swagger.io/resources/articles/best-practices-in-api-documentation/)

By following this style guide, we ensure that all documentation is consistent, professional, and helpful to users at all skill levels.