# Contributing to NEXATHON 2025

Thank you for your interest in contributing to NEXATHON 2025! This document provides guidelines and instructions for contributing to the project.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Component Guidelines](#component-guidelines)
- [Commit Messages](#commit-messages)
- [Pull Request Process](#pull-request-process)
- [Reporting Bugs](#reporting-bugs)
- [Feature Requests](#feature-requests)

## Code of Conduct

This project adheres to a code of conduct. By participating, you are expected to uphold this code. Please be respectful and professional in all interactions.

## Getting Started

1. **Fork the repository** on GitHub
2. **Clone your fork** locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/Nexathon-26.git
   cd Nexathon-26
   ```
3. **Install dependencies**:
   ```bash
   pnpm install
   ```
4. **Create a branch** for your feature or fix:
   ```bash
   git checkout -b feature/your-feature-name
   ```

## Development Workflow

### Running the Development Server

```bash
pnpm dev
```

The site will be available at `http://localhost:3000`.

### Building for Production

```bash
pnpm build
```

### Running the Linter

```bash
pnpm lint
```

### Testing Changes

Before submitting a pull request:

1. Test your changes thoroughly in development mode
2. Build the project and verify it compiles without errors
3. Check that all existing functionality still works
4. Ensure the site is responsive across different screen sizes
5. Test with reduced motion preferences enabled

## Coding Standards

### TypeScript

- Use TypeScript for all new components
- Define proper types/interfaces for props
- Avoid using `any` type
- Use type inference where appropriate

```tsx
// Good
interface ButtonProps {
  label: string
  onClick: () => void
  variant?: 'primary' | 'secondary'
}

export default function Button({ label, onClick, variant = 'primary' }: ButtonProps) {
  // implementation
}

// Avoid
export default function Button(props: any) {
  // implementation
}
```

### React Components

- Use functional components with hooks
- Keep components focused and single-purpose
- Extract reusable logic into custom hooks
- Use meaningful component and variable names

```tsx
// Good structure
"use client" // Add only if needed

import { useState, useEffect } from "react"
import { SomeIcon } from "lucide-react"

interface MyComponentProps {
  title: string
}

export default function MyComponent({ title }: MyComponentProps) {
  const [state, setState] = useState(initialValue)

  useEffect(() => {
    // side effects
  }, [])

  return (
    <div>
      {/* JSX */}
    </div>
  )
}
```

### Styling

- Use Tailwind CSS utility classes
- Follow the existing color scheme and design system
- Use CSS variables defined in `app/globals.css` for colors
- Maintain responsive design with Tailwind breakpoints

```tsx
// Good
<div className="bg-background text-foreground rounded-lg p-4 hover:bg-accent transition-colors">
  Content
</div>

// Avoid inline styles unless absolutely necessary
<div style={{ backgroundColor: '#000' }}>
  Content
</div>
```

### File Organization

Place files in the appropriate directory:

```
components/
├── layout/           # Navigation, footer, providers
├── sections/         # Page sections (hero, about, etc.)
├── features/         # Reusable features (animations, cards)
└── ui/               # Base UI components
```

## Component Guidelines

### Creating a New Section Component

1. Create file in `components/sections/`
2. Follow naming convention: `section-name.tsx`
3. Use "use client" if it needs client-side features
4. Import shared components from features:

```tsx
"use client"

import SectionHeader from "@/components/features/section-header"
import ScrollAnimation from "@/components/features/scroll-animation"
import TiltCard from "@/components/features/tilt-card"

export default function MySection() {
  return (
    <section id="my-section" className="py-20 px-4">
      <ScrollAnimation>
        <SectionHeader
          title="Section Title"
          subtitle="Section subtitle"
          gradient
        />
        {/* Section content */}
      </ScrollAnimation>
    </section>
  )
}
```

### Creating a Reusable Feature Component

1. Create file in `components/features/`
2. Make it flexible and reusable
3. Document props with TypeScript interfaces

```tsx
interface FeatureProps {
  /**
   * The main title of the feature
   */
  title: string
  /**
   * Optional description
   */
  description?: string
  /**
   * Additional CSS classes
   */
  className?: string
}

export default function Feature({ title, description, className }: FeatureProps) {
  // implementation
}
```

## Commit Messages

Follow the conventional commits specification:

```
<type>(<scope>): <description>

[optional body]

[optional footer]
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, semicolons, etc.)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `chore`: Build process or auxiliary tool changes

### Examples

```
feat(hero): add animated particle background

fix(navbar): resolve mobile menu scroll issue

docs(readme): update installation instructions

style(components): format code with prettier

refactor(sections): extract common logic to hooks
```

## Pull Request Process

1. **Update your branch** with the latest main:
   ```bash
   git fetch origin
   git rebase origin/main
   ```

2. **Ensure your changes**:
   - Build successfully (`pnpm build`)
   - Pass linting (`pnpm lint`)
   - Are well-tested
   - Include necessary documentation updates

3. **Create a Pull Request**:
   - Use a clear, descriptive title
   - Reference any related issues
   - Provide a detailed description of changes
   - Include screenshots for UI changes
   - List any breaking changes

4. **PR Template**:
   ```markdown
   ## Description
   Brief description of changes

   ## Type of Change
   - [ ] Bug fix
   - [ ] New feature
   - [ ] Breaking change
   - [ ] Documentation update

   ## Testing
   How has this been tested?

   ## Screenshots (if applicable)
   Add screenshots here

   ## Checklist
   - [ ] Code builds successfully
   - [ ] Linting passes
   - [ ] Responsive design maintained
   - [ ] Accessibility considered
   - [ ] Documentation updated
   ```

5. **Code Review**:
   - Address reviewer feedback promptly
   - Make requested changes in new commits
   - Squash commits before merging if requested

## Reporting Bugs

When reporting bugs, please include:

1. **Description**: Clear description of the bug
2. **Steps to Reproduce**: Detailed steps to reproduce the issue
3. **Expected Behavior**: What you expected to happen
4. **Actual Behavior**: What actually happened
5. **Screenshots**: If applicable
6. **Environment**:
   - OS and version
   - Browser and version
   - Node.js version
7. **Additional Context**: Any other relevant information

Use the GitHub issue template when available.

## Feature Requests

We welcome feature requests! Please:

1. Check existing issues to avoid duplicates
2. Provide a clear use case
3. Describe the proposed solution
4. Consider implementation challenges
5. Be open to discussion and alternatives

## Questions?

If you have questions about contributing:

- Open a GitHub issue with the "question" label
- Check existing documentation in HANDOVER.md
- Review closed issues and pull requests

## License

By contributing, you agree that your contributions will be licensed under the same license as the project.

---

Thank you for contributing to NEXATHON 2025! 🚀
