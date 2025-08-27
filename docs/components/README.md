# Component Documentation

This section contains documentation for all UI components and reusable components.

## React Components

### Form Components

#### `<Button />`

A reusable button component with multiple variants and states.

**Props:**
- `variant` (string, optional): Button style variant
  - `'primary'` (default): Primary button style
  - `'secondary'`: Secondary button style
  - `'outline'`: Outlined button style
  - `'ghost'`: Ghost button style
  - `'danger'`: Danger/destructive action style
- `size` (string, optional): Button size
  - `'small'`: Small button (32px height)
  - `'medium'` (default): Medium button (40px height)
  - `'large'`: Large button (48px height)
- `disabled` (boolean, optional): Whether button is disabled (default: false)
- `loading` (boolean, optional): Whether button is in loading state (default: false)
- `fullWidth` (boolean, optional): Whether button takes full width (default: false)
- `icon` (ReactNode, optional): Icon to display in button
- `iconPosition` (string, optional): Icon position ('left' | 'right', default: 'left')
- `onClick` (function, optional): Click event handler
- `type` (string, optional): Button type ('button' | 'submit' | 'reset', default: 'button')
- `children` (ReactNode): Button content

**Example Usage:**
```jsx
import { Button } from './components/Button';
import { PlusIcon, LoadingIcon } from './components/icons';

// Basic usage
<Button onClick={() => console.log('clicked')}>
  Click me
</Button>

// Primary button with icon
<Button variant="primary" icon={<PlusIcon />}>
  Add Item
</Button>

// Loading state
<Button loading disabled>
  Saving...
</Button>

// Danger button
<Button variant="danger" onClick={handleDelete}>
  Delete
</Button>

// Full width button
<Button variant="primary" fullWidth>
  Submit Form
</Button>

// Different sizes
<Button size="small">Small</Button>
<Button size="medium">Medium</Button>
<Button size="large">Large</Button>
```

**Styling:**
```css
/* Custom CSS variables for theming */
.button {
  --button-primary-bg: #007bff;
  --button-primary-hover: #0056b3;
  --button-secondary-bg: #6c757d;
  --button-outline-border: #007bff;
  --button-danger-bg: #dc3545;
}
```

#### `<Input />`

A reusable input component with validation and various types.

**Props:**
- `type` (string, optional): Input type ('text', 'email', 'password', 'number', etc.)
- `value` (string): Controlled input value
- `onChange` (function): Change event handler
- `placeholder` (string, optional): Placeholder text
- `label` (string, optional): Input label
- `error` (string, optional): Error message to display
- `helperText` (string, optional): Helper text below input
- `required` (boolean, optional): Whether input is required
- `disabled` (boolean, optional): Whether input is disabled
- `fullWidth` (boolean, optional): Whether input takes full width
- `startIcon` (ReactNode, optional): Icon at start of input
- `endIcon` (ReactNode, optional): Icon at end of input
- `maxLength` (number, optional): Maximum character length
- `autoComplete` (string, optional): Autocomplete attribute
- `onFocus` (function, optional): Focus event handler
- `onBlur` (function, optional): Blur event handler

**Example Usage:**
```jsx
import { Input } from './components/Input';
import { EmailIcon, EyeIcon, EyeOffIcon } from './components/icons';

// Basic text input
<Input
  label="Full Name"
  value={name}
  onChange={(e) => setName(e.target.value)}
  placeholder="Enter your full name"
  required
/>

// Email input with icon
<Input
  type="email"
  label="Email Address"
  value={email}
  onChange={(e) => setEmail(e.target.value)}
  startIcon={<EmailIcon />}
  error={emailError}
  autoComplete="email"
/>

// Password input with toggle visibility
<Input
  type={showPassword ? 'text' : 'password'}
  label="Password"
  value={password}
  onChange={(e) => setPassword(e.target.value)}
  endIcon={
    <button onClick={() => setShowPassword(!showPassword)}>
      {showPassword ? <EyeOffIcon /> : <EyeIcon />}
    </button>
  }
  helperText="Password must be at least 8 characters"
/>

// Number input with validation
<Input
  type="number"
  label="Age"
  value={age}
  onChange={(e) => setAge(e.target.value)}
  error={ageError}
  min="0"
  max="120"
/>
```

#### `<Select />`

A dropdown select component with search functionality.

**Props:**
- `options` (Array): Array of option objects `{ value, label, disabled? }`
- `value` (string | Array): Selected value(s)
- `onChange` (function): Change event handler
- `placeholder` (string, optional): Placeholder text
- `label` (string, optional): Select label
- `error` (string, optional): Error message
- `multiple` (boolean, optional): Allow multiple selections
- `searchable` (boolean, optional): Enable search functionality
- `clearable` (boolean, optional): Show clear button
- `disabled` (boolean, optional): Whether select is disabled
- `loading` (boolean, optional): Show loading state
- `onSearch` (function, optional): Search event handler for async options

**Example Usage:**
```jsx
import { Select } from './components/Select';

const countryOptions = [
  { value: 'us', label: 'United States' },
  { value: 'ca', label: 'Canada' },
  { value: 'uk', label: 'United Kingdom' },
  { value: 'de', label: 'Germany', disabled: true }
];

// Basic select
<Select
  label="Country"
  options={countryOptions}
  value={selectedCountry}
  onChange={(value) => setSelectedCountry(value)}
  placeholder="Select a country"
/>

// Multi-select with search
<Select
  label="Skills"
  options={skillOptions}
  value={selectedSkills}
  onChange={(values) => setSelectedSkills(values)}
  multiple
  searchable
  clearable
  placeholder="Select your skills"
/>

// Async select with search
<Select
  label="City"
  options={cityOptions}
  value={selectedCity}
  onChange={(value) => setSelectedCity(value)}
  searchable
  loading={loadingCities}
  onSearch={(query) => fetchCities(query)}
  placeholder="Search for a city"
/>
```

### Layout Components

#### `<Card />`

A flexible card container component.

**Props:**
- `variant` (string, optional): Card style variant ('default', 'outlined', 'elevated')
- `padding` (string, optional): Padding size ('none', 'small', 'medium', 'large')
- `hoverable` (boolean, optional): Add hover effects
- `clickable` (boolean, optional): Make card clickable
- `onClick` (function, optional): Click event handler
- `header` (ReactNode, optional): Card header content
- `footer` (ReactNode, optional): Card footer content
- `children` (ReactNode): Card body content

**Example Usage:**
```jsx
import { Card } from './components/Card';

// Basic card
<Card>
  <h3>Card Title</h3>
  <p>Card content goes here.</p>
</Card>

// Card with header and footer
<Card
  header={
    <div className="flex justify-between items-center">
      <h3>User Profile</h3>
      <button>Edit</button>
    </div>
  }
  footer={
    <div className="flex justify-end space-x-2">
      <Button variant="outline">Cancel</Button>
      <Button variant="primary">Save</Button>
    </div>
  }
>
  <div className="space-y-4">
    <Input label="Name" value={name} onChange={setName} />
    <Input label="Email" value={email} onChange={setEmail} />
  </div>
</Card>

// Clickable card
<Card
  variant="outlined"
  hoverable
  clickable
  onClick={() => navigate('/profile')}
>
  <h4>Go to Profile</h4>
  <p>Click to view your profile settings</p>
</Card>
```

#### `<Modal />`

A modal dialog component with overlay and focus management.

**Props:**
- `isOpen` (boolean): Whether modal is open
- `onClose` (function): Close event handler
- `title` (string, optional): Modal title
- `size` (string, optional): Modal size ('small', 'medium', 'large', 'fullscreen')
- `closeOnOverlayClick` (boolean, optional): Close when clicking overlay (default: true)
- `closeOnEscape` (boolean, optional): Close when pressing Escape (default: true)
- `showCloseButton` (boolean, optional): Show close button (default: true)
- `children` (ReactNode): Modal content

**Example Usage:**
```jsx
import { Modal } from './components/Modal';
import { useState } from 'react';

function App() {
  const [isModalOpen, setIsModalOpen] = useState(false);

  return (
    <>
      <Button onClick={() => setIsModalOpen(true)}>
        Open Modal
      </Button>

      <Modal
        isOpen={isModalOpen}
        onClose={() => setIsModalOpen(false)}
        title="Confirm Action"
        size="medium"
      >
        <div className="space-y-4">
          <p>Are you sure you want to delete this item?</p>
          <div className="flex justify-end space-x-2">
            <Button
              variant="outline"
              onClick={() => setIsModalOpen(false)}
            >
              Cancel
            </Button>
            <Button
              variant="danger"
              onClick={() => {
                handleDelete();
                setIsModalOpen(false);
              }}
            >
              Delete
            </Button>
          </div>
        </div>
      </Modal>
    </>
  );
}
```

### Data Display Components

#### `<Table />`

A flexible table component with sorting, filtering, and pagination.

**Props:**
- `data` (Array): Array of row objects
- `columns` (Array): Array of column definitions
- `loading` (boolean, optional): Show loading state
- `sortable` (boolean, optional): Enable column sorting
- `filterable` (boolean, optional): Enable column filtering
- `pagination` (Object, optional): Pagination configuration
- `onSort` (function, optional): Sort event handler
- `onFilter` (function, optional): Filter event handler
- `onPageChange` (function, optional): Page change handler
- `rowSelection` (Object, optional): Row selection configuration
- `onRowClick` (function, optional): Row click handler

**Column Definition:**
```typescript
interface Column {
  key: string;
  title: string;
  dataIndex: string;
  width?: number;
  sortable?: boolean;
  filterable?: boolean;
  render?: (value: any, row: any, index: number) => ReactNode;
  align?: 'left' | 'center' | 'right';
}
```

**Example Usage:**
```jsx
import { Table } from './components/Table';

const columns = [
  {
    key: 'name',
    title: 'Name',
    dataIndex: 'name',
    sortable: true,
    filterable: true
  },
  {
    key: 'email',
    title: 'Email',
    dataIndex: 'email',
    sortable: true
  },
  {
    key: 'status',
    title: 'Status',
    dataIndex: 'status',
    render: (status) => (
      <span className={`badge ${status === 'active' ? 'badge-success' : 'badge-warning'}`}>
        {status}
      </span>
    )
  },
  {
    key: 'actions',
    title: 'Actions',
    render: (_, row) => (
      <div className="space-x-2">
        <Button size="small" onClick={() => editUser(row.id)}>Edit</Button>
        <Button size="small" variant="danger" onClick={() => deleteUser(row.id)}>Delete</Button>
      </div>
    )
  }
];

const users = [
  { id: 1, name: 'John Doe', email: 'john@example.com', status: 'active' },
  { id: 2, name: 'Jane Smith', email: 'jane@example.com', status: 'inactive' }
];

<Table
  data={users}
  columns={columns}
  loading={loading}
  sortable
  filterable
  pagination={{
    current: currentPage,
    pageSize: 10,
    total: totalUsers,
    showSizeChanger: true
  }}
  onSort={(field, order) => handleSort(field, order)}
  onFilter={(filters) => handleFilter(filters)}
  onPageChange={(page, pageSize) => handlePageChange(page, pageSize)}
  rowSelection={{
    selectedRowKeys: selectedRows,
    onChange: (keys) => setSelectedRows(keys)
  }}
/>
```

## Vue.js Components

### Form Components

#### `<VButton />`

A Vue.js button component with slots and events.

**Props:**
- `variant` (String): Button variant ('primary', 'secondary', 'outline', 'ghost', 'danger')
- `size` (String): Button size ('small', 'medium', 'large')
- `disabled` (Boolean): Disabled state
- `loading` (Boolean): Loading state
- `fullWidth` (Boolean): Full width button
- `type` (String): Button type ('button', 'submit', 'reset')

**Events:**
- `@click`: Click event
- `@focus`: Focus event
- `@blur`: Blur event

**Slots:**
- `default`: Button content
- `icon`: Button icon

**Example Usage:**
```vue
<template>
  <div>
    <!-- Basic button -->
    <VButton @click="handleClick">
      Click me
    </VButton>

    <!-- Button with icon slot -->
    <VButton variant="primary">
      <template #icon>
        <PlusIcon />
      </template>
      Add Item
    </VButton>

    <!-- Loading button -->
    <VButton :loading="isSubmitting" :disabled="isSubmitting" @click="submit">
      {{ isSubmitting ? 'Saving...' : 'Save' }}
    </VButton>
  </div>
</template>

<script>
import { VButton } from './components/VButton.vue';
import { PlusIcon } from './components/icons';

export default {
  components: { VButton, PlusIcon },
  data() {
    return {
      isSubmitting: false
    };
  },
  methods: {
    handleClick() {
      console.log('Button clicked');
    },
    async submit() {
      this.isSubmitting = true;
      try {
        await this.saveData();
      } finally {
        this.isSubmitting = false;
      }
    }
  }
};
</script>
```

## Angular Components

### Form Components

#### `<app-input>`

An Angular input component with reactive forms integration.

**Inputs:**
- `@Input() label: string` - Input label
- `@Input() placeholder: string` - Placeholder text
- `@Input() type: string` - Input type (default: 'text')
- `@Input() required: boolean` - Required field
- `@Input() disabled: boolean` - Disabled state
- `@Input() error: string` - Error message
- `@Input() helperText: string` - Helper text

**Outputs:**
- `@Output() valueChange: EventEmitter<string>` - Value change event
- `@Output() focus: EventEmitter<FocusEvent>` - Focus event
- `@Output() blur: EventEmitter<FocusEvent>` - Blur event

**Example Usage:**
```typescript
// component.ts
import { Component } from '@angular/core';
import { FormBuilder, FormGroup, Validators } from '@angular/forms';

@Component({
  selector: 'app-user-form',
  template: `
    <form [formGroup]="userForm" (ngSubmit)="onSubmit()">
      <app-input
        label="Full Name"
        placeholder="Enter your full name"
        [required]="true"
        formControlName="name"
        [error]="getFieldError('name')">
      </app-input>

      <app-input
        type="email"
        label="Email"
        placeholder="Enter your email"
        [required]="true"
        formControlName="email"
        [error]="getFieldError('email')">
      </app-input>

      <app-input
        type="password"
        label="Password"
        [required]="true"
        formControlName="password"
        helperText="Password must be at least 8 characters"
        [error]="getFieldError('password')">
      </app-input>

      <button type="submit" [disabled]="userForm.invalid">
        Submit
      </button>
    </form>
  `
})
export class UserFormComponent {
  userForm: FormGroup;

  constructor(private fb: FormBuilder) {
    this.userForm = this.fb.group({
      name: ['', [Validators.required, Validators.minLength(2)]],
      email: ['', [Validators.required, Validators.email]],
      password: ['', [Validators.required, Validators.minLength(8)]]
    });
  }

  getFieldError(fieldName: string): string {
    const field = this.userForm.get(fieldName);
    if (field?.errors && field.touched) {
      if (field.errors['required']) return `${fieldName} is required`;
      if (field.errors['email']) return 'Please enter a valid email';
      if (field.errors['minlength']) return `${fieldName} is too short`;
    }
    return '';
  }

  onSubmit() {
    if (this.userForm.valid) {
      console.log('Form submitted:', this.userForm.value);
    }
  }
}
```

## Web Components

### Custom Elements

#### `<custom-button>`

A native Web Component button element.

**Attributes:**
- `variant` (string): Button variant
- `size` (string): Button size
- `disabled` (boolean): Disabled state
- `loading` (boolean): Loading state

**Properties:**
- `variant: string` - Button variant
- `size: string` - Button size
- `disabled: boolean` - Disabled state
- `loading: boolean` - Loading state

**Events:**
- `button-click`: Custom click event

**Example Usage:**
```html
<!-- HTML usage -->
<custom-button variant="primary" size="large">
  Click me
</custom-button>

<custom-button variant="danger" disabled>
  Disabled Button
</custom-button>

<!-- JavaScript usage -->
<script>
  const button = document.querySelector('custom-button');
  
  // Set properties
  button.variant = 'secondary';
  button.loading = true;
  
  // Listen to events
  button.addEventListener('button-click', (event) => {
    console.log('Custom button clicked:', event.detail);
  });
  
  // Call methods
  button.focus();
</script>
```

**Implementation:**
```javascript
class CustomButton extends HTMLElement {
  static get observedAttributes() {
    return ['variant', 'size', 'disabled', 'loading'];
  }

  constructor() {
    super();
    this.attachShadow({ mode: 'open' });
    this.render();
    this.setupEventListeners();
  }

  attributeChangedCallback(name, oldValue, newValue) {
    if (oldValue !== newValue) {
      this.render();
    }
  }

  get variant() {
    return this.getAttribute('variant') || 'default';
  }

  set variant(value) {
    this.setAttribute('variant', value);
  }

  get disabled() {
    return this.hasAttribute('disabled');
  }

  set disabled(value) {
    if (value) {
      this.setAttribute('disabled', '');
    } else {
      this.removeAttribute('disabled');
    }
  }

  render() {
    this.shadowRoot.innerHTML = `
      <style>
        :host {
          display: inline-block;
        }
        
        button {
          padding: 8px 16px;
          border: none;
          border-radius: 4px;
          cursor: pointer;
          font-family: inherit;
          transition: all 0.2s;
        }
        
        button:disabled {
          opacity: 0.6;
          cursor: not-allowed;
        }
        
        .primary {
          background-color: #007bff;
          color: white;
        }
        
        .primary:hover:not(:disabled) {
          background-color: #0056b3;
        }
      </style>
      
      <button 
        class="${this.variant}"
        ?disabled="${this.disabled}"
        ?loading="${this.loading}">
        <slot></slot>
      </button>
    `;
  }

  setupEventListeners() {
    this.shadowRoot.querySelector('button').addEventListener('click', (e) => {
      if (!this.disabled && !this.loading) {
        this.dispatchEvent(new CustomEvent('button-click', {
          detail: { originalEvent: e },
          bubbles: true
        }));
      }
    });
  }
}

customElements.define('custom-button', CustomButton);
```

## Component Testing

### React Component Testing

```jsx
// Button.test.jsx
import { render, screen, fireEvent } from '@testing-library/react';
import { Button } from './Button';

describe('Button', () => {
  test('renders button with text', () => {
    render(<Button>Click me</Button>);
    expect(screen.getByRole('button', { name: 'Click me' })).toBeInTheDocument();
  });

  test('calls onClick when clicked', () => {
    const handleClick = jest.fn();
    render(<Button onClick={handleClick}>Click me</Button>);
    
    fireEvent.click(screen.getByRole('button'));
    expect(handleClick).toHaveBeenCalledTimes(1);
  });

  test('is disabled when disabled prop is true', () => {
    render(<Button disabled>Disabled</Button>);
    expect(screen.getByRole('button')).toBeDisabled();
  });

  test('shows loading state', () => {
    render(<Button loading>Loading</Button>);
    expect(screen.getByRole('button')).toBeDisabled();
    expect(screen.getByText('Loading')).toBeInTheDocument();
  });
});
```

### Vue Component Testing

```javascript
// VButton.spec.js
import { mount } from '@vue/test-utils';
import VButton from './VButton.vue';

describe('VButton', () => {
  test('renders button with slot content', () => {
    const wrapper = mount(VButton, {
      slots: {
        default: 'Click me'
      }
    });
    
    expect(wrapper.text()).toContain('Click me');
  });

  test('emits click event when clicked', async () => {
    const wrapper = mount(VButton);
    
    await wrapper.trigger('click');
    expect(wrapper.emitted('click')).toBeTruthy();
  });

  test('applies variant class', () => {
    const wrapper = mount(VButton, {
      props: { variant: 'primary' }
    });
    
    expect(wrapper.classes()).toContain('btn-primary');
  });
});
```

## Accessibility Guidelines

### ARIA Labels and Roles
```jsx
// Good accessibility practices
<Button
  aria-label="Close dialog"
  aria-describedby="close-help"
  onClick={onClose}
>
  ×
</Button>

<Input
  label="Email"
  aria-required="true"
  aria-invalid={hasError}
  aria-describedby={hasError ? "email-error" : "email-help"}
/>

<div id="email-error" role="alert" aria-live="polite">
  {errorMessage}
</div>
```

### Keyboard Navigation
- Ensure all interactive elements are focusable
- Implement proper tab order
- Support keyboard shortcuts (Enter, Space, Escape)
- Provide visible focus indicators

### Screen Reader Support
- Use semantic HTML elements
- Provide descriptive labels and help text
- Announce dynamic content changes
- Use proper heading hierarchy

## Performance Optimization

### Code Splitting
```jsx
// Lazy load components
const Modal = lazy(() => import('./Modal'));
const DataTable = lazy(() => import('./DataTable'));

function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <Modal />
      <DataTable />
    </Suspense>
  );
}
```

### Memoization
```jsx
// Memoize expensive components
const ExpensiveComponent = memo(({ data, onUpdate }) => {
  const processedData = useMemo(() => {
    return data.map(item => ({ ...item, processed: true }));
  }, [data]);

  const handleUpdate = useCallback((id) => {
    onUpdate(id);
  }, [onUpdate]);

  return (
    <div>
      {processedData.map(item => (
        <div key={item.id} onClick={() => handleUpdate(item.id)}>
          {item.name}
        </div>
      ))}
    </div>
  );
});
```

### Bundle Size Optimization
- Use tree shaking to eliminate unused code
- Implement proper code splitting
- Optimize images and assets
- Use production builds for deployment