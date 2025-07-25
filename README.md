# Astro Modular Website Template

## Overview

This template provides a modular component system for building websites with Astro, React, and Tailwind CSS. It includes a component registry system to track all available components and prevent duplicates.

## Tech Stack

- **Astro 5.11.0** - Static site generator
- **React 18.2.0** - Interactive components
- **Tailwind CSS 3.4.1** - Utility-first CSS framework
- **Framer Motion 11.0.3** - Animation library
- **Lucide React 0.312.0** - Icon library
- **TypeScript** - Type safety

## Quick Start

1. **Clone/Copy this template:**
   ```bash
   # Copy the ASTRO-TEMPLATE folder to your project location
   cp -r ASTRO-TEMPLATE your-project-name
   cd your-project-name
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Start development server:**
   ```bash
   npm run dev
   ```

4. **Build for production:**
   ```bash
   npm run build
   ```

## Component Registry System

### How It Works

The component registry (`src/components/componentRegistry.ts`) serves as a central index of all components. Before creating any new component, **always check the registry first** to avoid duplicates.

### Component Organization

```
src/components/
├── componentRegistry.ts    # Central component index
├── ui/                    # Reusable UI components
├── sections/              # Page sections
├── lib/                   # Utility functions
└── components/            # General components
```

### Before Creating a Component

1. **Check the registry:** Open `src/components/componentRegistry.ts`
2. **Search for similar components:** Look through all categories
3. **If component exists:** Use the existing component or extend it
4. **If component is new:** Create it and add to registry

### Adding New Components

1. **Create the component file:**
   ```typescript
   // src/components/ui/NewComponent.tsx
   interface NewComponentProps {
     title: string;
     description?: string;
   }

   export default function NewComponent({ title, description }: NewComponentProps) {
     return (
       <div className="glass-card">
         <h2>{title}</h2>
         {description && <p>{description}</p>}
       </div>
     );
   }
   ```

2. **Add to registry:**
   ```typescript
   // In componentRegistry.ts
   ui: {
     // ... existing components
     NewComponent: {
       path: '@components/ui/NewComponent',
       description: 'Brief description of what it does',
       props: ['title', 'description?']
     }
   }
   ```

3. **Keep files under 1000 lines:**
   - If a component gets too large, split it into smaller components
   - Extract reusable logic into utility functions
   - Consider creating sub-components

## File Size Guidelines

- **Maximum 1000 lines per file**
- **When approaching limit:**
  - Split into multiple smaller files
  - Extract utility functions to `src/components/lib/`
  - Create sub-components
  - Move types to separate `.types.ts` files

## Creating Pages

### Step 1: Check Available Components
```bash
# Review the component registry
cat src/components/componentRegistry.ts
```

### Step 2: Create Page Structure
```astro
---
// src/pages/example.astro
import BaseLayout from '@layouts/BaseLayout.astro';
import Hero from '@components/sections/Hero.astro';
import Services from '@components/sections/Services.astro';
import ContactForm from '@components/sections/ContactForm.astro';
---

<BaseLayout title="Example Page" description="Example page description">
  <Hero />
  <Services />
  <ContactForm />
</BaseLayout>
```

### Step 3: Mix and Match Components
- Use existing components from the registry
- Create new components only when needed
- Update registry after adding new components

## Blog Setup

The template includes a pre-configured blog system:

- **Content location:** `src/content/blog/`
- **Blog posts:** Markdown files with frontmatter
- **Blog schema:** Defined in `src/content/config.ts`

### Creating Blog Posts

1. **Create markdown file:**
   ```markdown
   ---
   title: "Your Blog Post Title"
   description: "Brief description of the post"
   pubDate: 2025-01-15
   author: "Author Name"
   tags: ["tag1", "tag2"]
   readTime: "5 min read"
   ---

   # Your Blog Post

   Content goes here...
   ```

2. **Add to blog index:** Posts automatically appear in blog listings

## Project Structure

```
ASTRO-TEMPLATE/
├── README.md                    # This file
├── SETUP-GUIDE.md              # Detailed setup instructions
├── package.json                # Dependencies
├── astro.config.mjs            # Astro configuration
├── tailwind.config.mjs         # Tailwind configuration
├── tsconfig.json               # TypeScript configuration
├── src/
│   ├── components/
│   │   ├── componentRegistry.ts # Component index
│   │   ├── ui/                 # UI components
│   │   ├── sections/           # Page sections
│   │   ├── lib/               # Utilities
│   │   └── components/        # General components
│   ├── content/
│   │   ├── config.ts          # Content collections
│   │   └── blog/              # Blog posts
│   ├── layouts/
│   │   ├── BaseLayout.astro   # Base layout
│   │   └── BlogLayout.astro   # Blog layout
│   ├── pages/
│   │   ├── index.astro        # Homepage
│   │   ├── blog/              # Blog pages
│   │   └── [...more pages]
│   └── styles/
│       └── global.css         # Global styles
├── public/
│   └── images/                # Static images
└── docs/
    └── COMPONENT-GUIDE.md     # Component creation guide
```

## Development Workflow

1. **Check component registry** before creating anything new
2. **Create modular components** that can be reused
3. **Update registry** when adding new components
4. **Keep files under 1000 lines**
5. **Test components** in isolation before using in pages
6. **Document component props** in registry

## Best Practices

- **Always check registry first** - Avoid duplicate components
- **Write modular code** - Components should be reusable
- **Use TypeScript** - Define proper interfaces
- **Follow naming conventions** - PascalCase for components
- **Keep components small** - Single responsibility principle
- **Document everything** - Update registry with new components

## Available Scripts

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run check` - Run Astro type checking
- `npm run lint` - Run ESLint code checking
- `npm run analyze` - Analyze component usage and file sizes
- `npm run astro` - Run Astro CLI commands

## Deployment

This template is ready for deployment to Netlify, Vercel, or any static hosting service.

### Quick Deploy to Netlify:

1. **Push to GitHub:**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/yourusername/your-repo.git
   git push -u origin main
   ```

2. **Deploy on Netlify:**
   - Connect your GitHub repository
   - Build command: `npm run build`
   - Publish directory: `dist`
   - Deploy!

3. **Set Environment Variables:**
   - `SITE_URL=https://your-site.netlify.app`
   - Update other values from `.env.example`

For detailed deployment instructions, see `DEPLOYMENT.md`.

## Next Steps

1. Read `SETUP-GUIDE.md` for detailed setup instructions
2. Review `docs/COMPONENT-GUIDE.md` for component creation guidelines
3. Explore the component registry to understand available components
4. Start building your site using existing components
5. Add new components to the registry as needed
6. Deploy to Netlify following `DEPLOYMENT.md`

---

**Remember:** Always check the component registry before creating new components to maintain a clean, non-duplicate codebase.
#   A s t r o - W e b - T e m p l a t e  
 #   D i n e  
 