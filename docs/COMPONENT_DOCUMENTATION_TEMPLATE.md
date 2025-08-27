# Component Documentation Template

This template provides comprehensive documentation patterns for UI components across different frontend frameworks.

## Component Documentation Structure

### React Component Documentation

```jsx
/**
 * @component ComponentName
 * @description Brief description of what the component does
 * @example
 * <ComponentName
 *   title="My Component"
 *   isVisible={true}
 *   onAction={(data) => console.log(data)}
 * >
 *   <div>Child content</div>
 * </ComponentName>
 */
import React from 'react';
import PropTypes from 'prop-types';

/**
 * ComponentName - A reusable UI component
 * 
 * This component provides [specific functionality] and can be customized
 * through various props and themes. It supports accessibility features
 * and is fully responsive.
 * 
 * @param {Object} props - Component props
 * @param {string} props.title - The title to display
 * @param {boolean} props.isVisible - Whether the component is visible
 * @param {Function} props.onAction - Callback when action is triggered
 * @param {React.ReactNode} props.children - Child elements to render
 * @param {string} props.className - Additional CSS classes
 * @param {Object} props.style - Inline styles
 * @param {string} props.variant - Visual variant ('primary', 'secondary', 'danger')
 * @param {boolean} props.disabled - Whether the component is disabled
 * @param {string} props.size - Size variant ('small', 'medium', 'large')
 * 
 * @example
 * // Basic usage
 * <ComponentName title="Hello World" />
 * 
 * // With all props
 * <ComponentName
 *   title="Advanced Example"
 *   isVisible={true}
 *   variant="primary"
 *   size="large"
 *   disabled={false}
 *   className="custom-class"
 *   style={{ marginTop: '10px' }}
 *   onAction={(data) => handleAction(data)}
 * >
 *   <p>Custom content here</p>
 * </ComponentName>
 * 
 * @accessibility
 * - Supports ARIA labels and roles
 * - Keyboard navigation enabled
 * - Screen reader friendly
 * - High contrast mode support
 * 
 * @performance
 * - Memoized to prevent unnecessary re-renders
 * - Lazy loading support for large content
 * - Optimized bundle size
 * 
 * @since 1.0.0
 * @author Your Name
 */
const ComponentName = ({
  title,
  isVisible = true,
  onAction,
  children,
  className = '',
  style = {},
  variant = 'primary',
  disabled = false,
  size = 'medium',
  ...otherProps
}) => {
  // Component implementation
  return (
    <div
      className={`component-name component-name--${variant} component-name--${size} ${className}`}
      style={style}
      {...otherProps}
    >
      {isVisible && (
        <>
          <h2 className="component-name__title">{title}</h2>
          <div className="component-name__content">
            {children}
          </div>
          <button
            className="component-name__action"
            disabled={disabled}
            onClick={onAction}
          >
            Action
          </button>
        </>
      )}
    </div>
  );
};

ComponentName.propTypes = {
  /** The title to display */
  title: PropTypes.string.isRequired,
  /** Whether the component is visible */
  isVisible: PropTypes.bool,
  /** Callback when action is triggered */
  onAction: PropTypes.func,
  /** Child elements to render */
  children: PropTypes.node,
  /** Additional CSS classes */
  className: PropTypes.string,
  /** Inline styles */
  style: PropTypes.object,
  /** Visual variant */
  variant: PropTypes.oneOf(['primary', 'secondary', 'danger']),
  /** Whether the component is disabled */
  disabled: PropTypes.bool,
  /** Size variant */
  size: PropTypes.oneOf(['small', 'medium', 'large'])
};

ComponentName.defaultProps = {
  isVisible: true,
  variant: 'primary',
  disabled: false,
  size: 'medium'
};

export default ComponentName;
```

### Vue Component Documentation

```vue
<template>
  <div
    :class="componentClasses"
    :style="componentStyles"
    v-show="isVisible"
  >
    <h2 class="component-name__title">{{ title }}</h2>
    <div class="component-name__content">
      <slot />
    </div>
    <button
      class="component-name__action"
      :disabled="disabled"
      @click="handleAction"
    >
      Action
    </button>
  </div>
</template>

<script>
/**
 * ComponentName - A reusable Vue component
 * 
 * This component provides [specific functionality] and can be customized
 * through various props and themes. It supports accessibility features
 * and is fully responsive.
 * 
 * @example
 * <!-- Basic usage -->
 * <ComponentName title="Hello World" />
 * 
 * <!-- With all props -->
 * <ComponentName
 *   title="Advanced Example"
 *   :is-visible="true"
 *   variant="primary"
 *   size="large"
 *   :disabled="false"
 *   class="custom-class"
 *   :style="{ marginTop: '10px' }"
 *   @action="handleAction"
 * >
 *   <p>Custom content here</p>
 * </ComponentName>
 * 
 * @accessibility
 * - Supports ARIA labels and roles
 * - Keyboard navigation enabled
 * - Screen reader friendly
 * - High contrast mode support
 * 
 * @performance
 * - Computed properties for optimal reactivity
 * - Lazy loading support for large content
 * - Optimized bundle size
 * 
 * @since 1.0.0
 * @author Your Name
 */
export default {
  name: 'ComponentName',
  
  props: {
    /** The title to display */
    title: {
      type: String,
      required: true
    },
    /** Whether the component is visible */
    isVisible: {
      type: Boolean,
      default: true
    },
    /** Visual variant */
    variant: {
      type: String,
      default: 'primary',
      validator: value => ['primary', 'secondary', 'danger'].includes(value)
    },
    /** Whether the component is disabled */
    disabled: {
      type: Boolean,
      default: false
    },
    /** Size variant */
    size: {
      type: String,
      default: 'medium',
      validator: value => ['small', 'medium', 'large'].includes(value)
    },
    /** Additional CSS classes */
    className: {
      type: String,
      default: ''
    },
    /** Inline styles */
    componentStyles: {
      type: Object,
      default: () => ({})
    }
  },

  emits: ['action'],

  computed: {
    componentClasses() {
      return [
        'component-name',
        `component-name--${this.variant}`,
        `component-name--${this.size}`,
        this.className
      ].filter(Boolean);
    }
  },

  methods: {
    handleAction() {
      if (!this.disabled) {
        this.$emit('action', { timestamp: Date.now() });
      }
    }
  }
};
</script>

<style scoped>
.component-name {
  /* Base styles */
}

.component-name--primary {
  /* Primary variant styles */
}

.component-name--secondary {
  /* Secondary variant styles */
}

.component-name--danger {
  /* Danger variant styles */
}

.component-name--small {
  /* Small size styles */
}

.component-name--medium {
  /* Medium size styles */
}

.component-name--large {
  /* Large size styles */
}
</style>
```

### Angular Component Documentation

```typescript
/**
 * ComponentName - A reusable Angular component
 * 
 * This component provides [specific functionality] and can be customized
 * through various inputs and themes. It supports accessibility features
 * and is fully responsive.
 * 
 * @example
 * <!-- Basic usage -->
 * <app-component-name title="Hello World"></app-component-name>
 * 
 * <!-- With all inputs -->
 * <app-component-name
 *   title="Advanced Example"
 *   [isVisible]="true"
 *   variant="primary"
 *   size="large"
 *   [disabled]="false"
 *   class="custom-class"
 *   [style]="{ marginTop: '10px' }"
 *   (action)="handleAction($event)"
 * >
 *   <p>Custom content here</p>
 * </app-component-name>
 * 
 * @accessibility
 * - Supports ARIA labels and roles
 * - Keyboard navigation enabled
 * - Screen reader friendly
 * - High contrast mode support
 * 
 * @performance
 * - OnPush change detection strategy
 * - Lazy loading support for large content
 * - Optimized bundle size
 * 
 * @since 1.0.0
 * @author Your Name
 */
import { Component, Input, Output, EventEmitter, ChangeDetectionStrategy } from '@angular/core';

export type ComponentVariant = 'primary' | 'secondary' | 'danger';
export type ComponentSize = 'small' | 'medium' | 'large';

export interface ActionEvent {
  timestamp: number;
  componentId: string;
}

@Component({
  selector: 'app-component-name',
  templateUrl: './component-name.component.html',
  styleUrls: ['./component-name.component.scss'],
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class ComponentNameComponent {
  /** The title to display */
  @Input() title!: string;
  
  /** Whether the component is visible */
  @Input() isVisible = true;
  
  /** Visual variant */
  @Input() variant: ComponentVariant = 'primary';
  
  /** Whether the component is disabled */
  @Input() disabled = false;
  
  /** Size variant */
  @Input() size: ComponentSize = 'medium';
  
  /** Additional CSS classes */
  @Input() className = '';
  
  /** Inline styles */
  @Input() componentStyles: { [key: string]: string } = {};
  
  /** Event emitted when action is triggered */
  @Output() action = new EventEmitter<ActionEvent>();

  get componentClasses(): string {
    return [
      'component-name',
      `component-name--${this.variant}`,
      `component-name--${this.size}`,
      this.className
    ].filter(Boolean).join(' ');
  }

  handleAction(): void {
    if (!this.disabled) {
      this.action.emit({
        timestamp: Date.now(),
        componentId: this.title
      });
    }
  }
}
```

## Component Categories

### Form Components

#### Input Component
```jsx
/**
 * @component Input
 * @description A reusable input component with validation and styling
 * 
 * @param {Object} props - Component props
 * @param {string} props.type - Input type (text, email, password, etc.)
 * @param {string} props.value - Current input value
 * @param {Function} props.onChange - Change handler
 * @param {string} props.placeholder - Placeholder text
 * @param {string} props.label - Input label
 * @param {boolean} props.required - Whether the field is required
 * @param {string} props.error - Error message to display
 * @param {boolean} props.disabled - Whether the input is disabled
 * @param {string} props.size - Size variant ('small', 'medium', 'large')
 * 
 * @example
 * // Basic usage
 * <Input
 *   type="text"
 *   value={value}
 *   onChange={setValue}
 *   placeholder="Enter your name"
 * />
 * 
 * // With validation
 * <Input
 *   type="email"
 *   value={email}
 *   onChange={setEmail}
 *   label="Email Address"
 *   required
 *   error={emailError}
 * />
 * 
 * @accessibility
 * - Proper label association
 * - ARIA attributes for validation states
 * - Keyboard navigation support
 * - Screen reader announcements for errors
 */
```

#### Button Component
```jsx
/**
 * @component Button
 * @description A customizable button component with multiple variants
 * 
 * @param {Object} props - Component props
 * @param {string} props.variant - Visual variant ('primary', 'secondary', 'outline', 'ghost')
 * @param {string} props.size - Size variant ('small', 'medium', 'large')
 * @param {boolean} props.loading - Whether to show loading state
 * @param {boolean} props.disabled - Whether the button is disabled
 * @param {Function} props.onClick - Click handler
 * @param {React.ReactNode} props.children - Button content
 * @param {string} props.type - Button type ('button', 'submit', 'reset')
 * 
 * @example
 * // Primary button
 * <Button variant="primary" onClick={handleClick}>
 *   Click Me
 * </Button>
 * 
 * // Loading state
 * <Button variant="primary" loading>
 *   Processing...
 * </Button>
 * 
 * // Submit button
 * <Button type="submit" variant="primary">
 *   Submit Form
 * </Button>
 * 
 * @accessibility
 * - Proper button semantics
 * - Loading state announcements
 * - Keyboard activation support
 * - Focus management
 */
```

### Layout Components

#### Card Component
```jsx
/**
 * @component Card
 * @description A container component for grouping related content
 * 
 * @param {Object} props - Component props
 * @param {string} props.title - Card title
 * @param {React.ReactNode} props.children - Card content
 * @param {string} props.variant - Visual variant ('default', 'elevated', 'outlined')
 * @param {boolean} props.clickable - Whether the card is clickable
 * @param {Function} props.onClick - Click handler for clickable cards
 * @param {React.ReactNode} props.header - Custom header content
 * @param {React.ReactNode} props.footer - Custom footer content
 * 
 * @example
 * // Basic card
 * <Card title="User Profile">
 *   <p>User information goes here</p>
 * </Card>
 * 
 * // Clickable card
 * <Card
 *   title="Clickable Card"
 *   clickable
 *   onClick={() => console.log('Card clicked')}
 * >
 *   <p>This card can be clicked</p>
 * </Card>
 * 
 * // Custom header and footer
 * <Card
 *   header={<div>Custom Header</div>}
 *   footer={<div>Custom Footer</div>}
 * >
 *   <p>Card content</p>
 * </Card>
 * 
 * @accessibility
 * - Proper heading structure
 * - Clickable state announcements
 * - Keyboard navigation support
 * - Focus management for interactive cards
 */
```

#### Modal Component
```jsx
/**
 * @component Modal
 * @description A modal dialog component with backdrop and focus management
 * 
 * @param {Object} props - Component props
 * @param {boolean} props.isOpen - Whether the modal is open
 * @param {Function} props.onClose - Close handler
 * @param {string} props.title - Modal title
 * @param {React.ReactNode} props.children - Modal content
 * @param {string} props.size - Size variant ('small', 'medium', 'large', 'full')
 * @param {boolean} props.closeOnBackdrop - Whether clicking backdrop closes modal
 * @param {boolean} props.closeOnEscape - Whether pressing Escape closes modal
 * @param {React.ReactNode} props.footer - Custom footer content
 * 
 * @example
 * // Basic modal
 * <Modal
 *   isOpen={isModalOpen}
 *   onClose={() => setIsModalOpen(false)}
 *   title="Confirmation"
 * >
 *   <p>Are you sure you want to proceed?</p>
 * </Modal>
 * 
 * // Modal with custom footer
 * <Modal
 *   isOpen={isModalOpen}
 *   onClose={() => setIsModalOpen(false)}
 *   title="User Details"
 *   footer={
 *     <div>
 *       <Button onClick={() => setIsModalOpen(false)}>Cancel</Button>
 *       <Button variant="primary">Save</Button>
 *     </div>
 *   }
 * >
 *   <form>Form content here</form>
 * </Modal>
 * 
 * @accessibility
 * - ARIA modal attributes
 * - Focus trap within modal
 * - Escape key handling
 * - Backdrop click handling
 * - Screen reader announcements
 * - Return focus to trigger element
 */
```

## CSS Architecture

### BEM Methodology
```scss
// Component base
.component-name {
  // Base styles
  
  // Modifiers
  &--primary {
    // Primary variant styles
  }
  
  &--secondary {
    // Secondary variant styles
  }
  
  &--danger {
    // Danger variant styles
  }
  
  &--small {
    // Small size styles
  }
  
  &--medium {
    // Medium size styles
  }
  
  &--large {
    // Large size styles
  }
  
  // Elements
  &__title {
    // Title element styles
  }
  
  &__content {
    // Content element styles
  }
  
  &__action {
    // Action button styles
    
    &:disabled {
      // Disabled state
    }
    
    &:hover {
      // Hover state
    }
    
    &:focus {
      // Focus state
    }
  }
}

// Responsive variants
@media (max-width: 768px) {
  .component-name {
    // Mobile styles
  }
}

// Dark theme support
@media (prefers-color-scheme: dark) {
  .component-name {
    // Dark theme styles
  }
}
```

## Testing Documentation

### Unit Test Examples
```javascript
/**
 * @test ComponentName
 * @description Unit tests for ComponentName component
 */
import { render, screen, fireEvent } from '@testing-library/react';
import ComponentName from './ComponentName';

describe('ComponentName', () => {
  it('renders with title', () => {
    render(<ComponentName title="Test Title" />);
    expect(screen.getByText('Test Title')).toBeInTheDocument();
  });

  it('calls onAction when action button is clicked', () => {
    const mockOnAction = jest.fn();
    render(<ComponentName title="Test" onAction={mockOnAction} />);
    
    fireEvent.click(screen.getByText('Action'));
    expect(mockOnAction).toHaveBeenCalled();
  });

  it('does not render when isVisible is false', () => {
    render(<ComponentName title="Test" isVisible={false} />);
    expect(screen.queryByText('Test')).not.toBeInTheDocument();
  });

  it('applies variant classes correctly', () => {
    render(<ComponentName title="Test" variant="danger" />);
    const component = screen.getByText('Test').closest('.component-name');
    expect(component).toHaveClass('component-name--danger');
  });

  it('disables action button when disabled prop is true', () => {
    render(<ComponentName title="Test" disabled />);
    expect(screen.getByText('Action')).toBeDisabled();
  });
});
```

## Storybook Documentation

### Story Examples
```javascript
/**
 * @story ComponentName
 * @description Storybook stories for ComponentName component
 */
import ComponentName from './ComponentName';

export default {
  title: 'Components/ComponentName',
  component: ComponentName,
  parameters: {
    docs: {
      description: {
        component: 'A reusable component that provides [specific functionality].'
      }
    }
  },
  argTypes: {
    title: {
      description: 'The title to display',
      control: 'text'
    },
    variant: {
      description: 'Visual variant',
      control: 'select',
      options: ['primary', 'secondary', 'danger']
    },
    size: {
      description: 'Size variant',
      control: 'select',
      options: ['small', 'medium', 'large']
    },
    disabled: {
      description: 'Whether the component is disabled',
      control: 'boolean'
    }
  }
};

// Default story
export const Default = {
  args: {
    title: 'Default Component',
    variant: 'primary',
    size: 'medium',
    disabled: false
  }
};

// Primary variant
export const Primary = {
  args: {
    title: 'Primary Component',
    variant: 'primary'
  }
};

// Secondary variant
export const Secondary = {
  args: {
    title: 'Secondary Component',
    variant: 'secondary'
  }
};

// Danger variant
export const Danger = {
  args: {
    title: 'Danger Component',
    variant: 'danger'
  }
};

// Disabled state
export const Disabled = {
  args: {
    title: 'Disabled Component',
    disabled: true
  }
};

// With children
export const WithChildren = {
  args: {
    title: 'Component with Children',
    children: <p>This is some custom content inside the component.</p>
  }
};
```

## Performance Considerations

### Optimization Techniques
```jsx
/**
 * @component OptimizedComponent
 * @description Example of performance optimizations
 */
import React, { memo, useCallback, useMemo } from 'react';

const OptimizedComponent = memo(({ data, onAction, config }) => {
  // Memoize expensive calculations
  const processedData = useMemo(() => {
    return data.map(item => ({
      ...item,
      processed: item.value * config.multiplier
    }));
  }, [data, config.multiplier]);

  // Memoize event handlers
  const handleAction = useCallback((item) => {
    onAction(item);
  }, [onAction]);

  return (
    <div>
      {processedData.map(item => (
        <div key={item.id} onClick={() => handleAction(item)}>
          {item.name}
        </div>
      ))}
    </div>
  );
});

OptimizedComponent.displayName = 'OptimizedComponent';
```

---

*This template provides comprehensive documentation patterns for UI components that can be adapted for any frontend framework.*