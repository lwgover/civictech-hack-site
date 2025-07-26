# FedReg Design System

A modern, civic-oriented design system for making federal regulation clear and accessible.

## Design Principles

- **Clean & Modern**: Minimal, focused design that prioritizes content
- **Civic-Oriented**: Professional yet approachable, building trust in government transparency
- **Accessible**: High contrast, readable typography, and keyboard navigation
- **Responsive**: Works seamlessly across all device sizes

## Color Palette

### Primary Colors
- **Gradient Start**: `#db5f5aff` (muted red)
- **Gradient End**: `#544d8fbe` (muted blue)
- **Primary Blue**: `#3b82f6` (for CTAs and links)
- **Success Green**: `#10b981`
- **Warning Orange**: `#f59e0b`
- **Error Red**: `#ef4444`

### Neutral Colors
- **Gray 900**: `#111827` (headings)
- **Gray 700**: `#374151` (body text)
- **Gray 500**: `#6b7280` (muted text)
- **Gray 100**: `#f3f4f6` (backgrounds)
- **White**: `#ffffff`

## Typography

### Fonts
- **Raleway**: Headings (bold, airy, modern)
- **Inter**: Body text (clear, highly legible)

### Font Weights
- **Raleway**: 400, 500, 600, 700, 800, 900
- **Inter**: 300, 400, 500, 600, 700

### Type Scale
- **Hero Title**: `text-5xl md:text-7xl` (Raleway, bold)
- **Page Title**: `text-4xl md:text-5xl` (Raleway, bold)
- **Section Title**: `text-3xl` (Raleway, bold)
- **Card Title**: `text-xl` (Raleway, bold)
- **Body Large**: `text-xl` (Inter, regular)
- **Body**: `text-base` (Inter, regular)
- **Small**: `text-sm` (Inter, regular)

## Component Library

### Core Components

#### Button (`$lib/components/Button.svelte`)
```svelte
<Button 
  variant="primary|secondary|outline" 
  size="small|medium|large"
  href="/optional-link"
>
  Button Text
</Button>
```

**Variants:**
- `primary`: White background, dark text, shadow
- `secondary`: Transparent with white border, white text
- `outline`: Transparent with gray border, gray text

**Sizes:**
- `small`: `px-4 py-2 text-sm`
- `medium`: `px-6 py-3 text-base`
- `large`: `px-8 py-4 text-lg`

#### Card (`$lib/components/Card.svelte`)
```svelte
<Card 
  title="Card Title"
  description="Card description text"
  href="/optional-link"
  variant="default|elevated|outline"
>
  <!-- Additional content -->
</Card>
```

**Variants:**
- `default`: White background, subtle shadow
- `elevated`: White background, stronger shadow
- `outline`: Transparent with border

#### Icon (`$lib/components/Icon.svelte`)
```svelte
<Icon 
  name="document|timeline|comment|gavel|arrow"
  size="sm|md|lg|xl"
  color="current|blue-600|white"
/>
```

**Available Icons:**
- `document`: Document/paper icon
- `timeline`: Clock/timeline icon
- `comment`: Speech bubble icon
- `gavel`: Gavel/justice icon
- `arrow`: Right arrow icon

#### Header (`$lib/components/Header.svelte`)
Fixed header with navigation and mobile menu.

#### Footer (`$lib/components/Footer.svelte`)
Site footer with links and branding.

## Layout Patterns

### Page Structure
```svelte
<script>
  import Header from '$lib/components/Header.svelte';
  import Footer from '$lib/components/Footer.svelte';
  // Import other components as needed
</script>

<svelte:head>
  <title>Page Title - FedReg</title>
  <meta name="description" content="Page description" />
</svelte:head>

<Header />

<!-- Page Header Section -->
<section class="pt-24 pb-12 bg-gradient-to-br from-gray-50 to-blue-50">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="text-center">
      <h1 class="text-4xl md:text-5xl font-bold text-gray-900 font-raleway mb-4">
        Page Title
      </h1>
      <p class="text-xl text-gray-600 font-inter max-w-2xl mx-auto">
        Page description
      </p>
    </div>
  </div>
</section>

<!-- Content Sections -->
<section class="py-20 bg-white">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <!-- Content here -->
  </div>
</section>

<Footer />
```

### Section Patterns

#### Hero Section
```svelte
<section class="relative min-h-screen flex items-center justify-center overflow-hidden">
  <div class="absolute inset-0 bg-gradient-to-br from-[#db5f5aff] to-[#544d8fbe]"></div>
  <div class="relative z-10 text-center px-4 sm:px-6 lg:px-8 max-w-4xl mx-auto">
    <h1 class="text-5xl md:text-7xl font-bold text-white font-raleway mb-6">
      Hero Title
    </h1>
    <p class="text-xl md:text-2xl text-white/90 font-inter mb-8">
      Hero subtitle
    </p>
    <Button href="/cta-link" variant="primary" size="large">
      Call to Action
    </Button>
  </div>
</section>
```

#### Content Grid
```svelte
<section class="py-20 bg-white">
  <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
    <div class="text-center mb-16">
      <h2 class="text-4xl font-bold text-gray-900 font-raleway mb-4">
        Section Title
      </h2>
      <p class="text-xl text-gray-600 font-inter max-w-2xl mx-auto">
        Section description
      </p>
    </div>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      <!-- Grid items -->
    </div>
  </div>
</section>
```

## Building New Pages

### 1. Create the Page File
Create a new `.svelte` file in the appropriate directory under `src/routes/`.

### 2. Import Components
```svelte
<script>
  import Header from '$lib/components/Header.svelte';
  import Footer from '$lib/components/Footer.svelte';
  import Button from '$lib/components/Button.svelte';
  import Card from '$lib/components/Card.svelte';
  import Icon from '$lib/components/Icon.svelte';
</script>
```

### 3. Add Page Metadata
```svelte
<svelte:head>
  <title>Page Title - FedReg</title>
  <meta name="description" content="Page description for SEO" />
</svelte:head>
```

### 4. Use the Layout Pattern
Follow the standard page structure with Header, content sections, and Footer.

### 5. Leverage Existing Components
Use the component library to maintain consistency:
- Use `Button` for all CTAs
- Use `Card` for content containers
- Use `Icon` for consistent iconography
- Follow the typography scale

## Responsive Design

### Breakpoints
- **Mobile**: `< 768px`
- **Tablet**: `768px - 1024px`
- **Desktop**: `> 1024px`

### Responsive Utilities
- `text-responsive-xl`: `clamp(2rem, 5vw, 4rem)`
- `text-responsive-lg`: `clamp(1.5rem, 3vw, 2.5rem)`
- Grid columns: `grid-cols-1 md:grid-cols-2 lg:grid-cols-3`

## Accessibility

### Standards
- WCAG 2.1 AA compliance
- Keyboard navigation support
- Screen reader compatibility
- High contrast ratios
- Focus indicators

### Implementation
- Use semantic HTML elements
- Include proper ARIA labels
- Ensure color contrast meets standards
- Test with keyboard navigation
- Use descriptive alt text for images

## Performance

### Optimization
- Lazy load images and components
- Use Tailwind's purge to remove unused CSS
- Optimize font loading with preconnect
- Minimize JavaScript bundle size
- Use Svelte's built-in optimizations

## Development Workflow

### Adding New Components
1. Create component in `$lib/components/`
2. Follow naming convention: `PascalCase.svelte`
3. Export props with default values
4. Include TypeScript types if needed
5. Add to this documentation

### Styling Guidelines
- Use Tailwind CSS classes
- Follow the design system color palette
- Use the established typography scale
- Maintain consistent spacing with Tailwind's spacing scale
- Use the component variants for consistency

### Testing
- Test on multiple devices and screen sizes
- Verify accessibility with screen readers
- Check keyboard navigation
- Validate HTML and CSS
- Test performance with Lighthouse

## File Structure

```
src/
├── lib/
│   └── components/
│       ├── Button.svelte
│       ├── Card.svelte
│       ├── Icon.svelte
│       ├── Header.svelte
│       └── Footer.svelte
├── routes/
│   ├── +layout.svelte
│   ├── +page.svelte
│   ├── about/
│   │   └── +page.svelte
│   └── rules/
│       └── +page.svelte
├── app.css
└── app.html
```

This design system provides a solid foundation for building consistent, accessible, and maintainable pages for the FedReg platform. 