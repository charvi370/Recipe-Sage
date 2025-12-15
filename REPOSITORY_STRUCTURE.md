# 📁 Repository Structure - RecipeSage

## Overview
RecipeSage follows a modular Next.js App Router architecture with clear separation between AI logic, UI components, and service integrations.

---

## Root Level Files

| File/Folder | Purpose |
|-------------|---------|
| `package.json` | Project dependencies and npm scripts |
| `next.config.ts` | Next.js configuration (image domains, build settings) |
| `tsconfig.json` | TypeScript compiler configuration |
| `tailwind.config.ts` | Tailwind CSS theme and plugin configuration |
| `postcss.config.mjs` | PostCSS plugins for CSS processing |
| `components.json` | ShadCN UI component configuration |
| `apphosting.yaml` | Firebase App Hosting deployment settings |
| `.gitignore` | Git ignore rules for node_modules, env files, etc. |
| `README.md` | Project documentation (this file) |

---

## `src/` - Source Code Directory

### `src/app/` - Next.js Pages (App Router)
- **`layout.tsx`**: Root layout with metadata and global structure
- **`page.tsx`**: Home page that renders the main RecipeSageApp component
- **`globals.css`**: Global CSS styles and Tailwind imports

### `src/ai/` - AI Orchestration Layer
Contains all Genkit-based AI workflows and configuration.

- **`genkit.ts`**: Genkit initialization and AI model configuration
- **`dev.ts`**: Development server entry point for testing AI flows
- **`flows/`**: Modular AI workflow definitions
  - `generate-recipes-from-ingredients.ts` - Main recipe generation flow
  - `ingredient-recognition-from-image.ts` - Computer vision ingredient detection
  - `nutrition-facts-for-recipe.ts` - Nutritional analysis
  - `allergen-detection-in-recipes.ts` - Allergen safety checking
  - `generate-recipe-image.ts` - Image fetching orchestration

### `src/components/` - React Components
All UI components organized by function.

#### Core Application Components
- **`RecipeSageApp.tsx`**: Main application component with state management
- **`RecipeCard.tsx`**: Individual recipe display card
- **`RecipeDetails.tsx`**: Detailed recipe view with nutrition and allergen info

#### `layout/` - Layout Components
- `Header.tsx` - Application header with navigation
- `Logo.tsx` - Brand logo component

#### `ui/` - ShadCN UI Components
Pre-built accessible components (20+ components):
- Form components: `input.tsx`, `textarea.tsx`, `button.tsx`, `checkbox.tsx`, `select.tsx`
- Display components: `card.tsx`, `badge.tsx`, `avatar.tsx`, `skeleton.tsx`
- Feedback components: `alert.tsx`, `toast.tsx`, `progress.tsx`
- Layout components: `dialog.tsx`, `sheet.tsx`, `tabs.tsx`, `accordion.tsx`
- Navigation components: `dropdown-menu.tsx`, `menubar.tsx`

### `src/hooks/` - Custom React Hooks
- **`use-toast.ts`**: Toast notification hook
- **`use-mobile.tsx`**: Mobile device detection hook

### `src/lib/` - Utility Libraries
Shared utilities and type definitions.

- **`actions.ts`**: Next.js Server Actions that call AI flows
- **`types.ts`**: TypeScript type definitions (Recipe, NutritionFacts, AllergenInfo)
- **`utils.ts`**: Helper functions (className merging, etc.)
- **`placeholder-images.ts`**: Fallback image logic
- **`placeholder-images.json`**: Placeholder image URLs

### `src/services/` - External API Integrations
Wrappers for third-party services.

- **`google-search.ts`**: Google Custom Search API integration for recipe images
- **`unsplash.ts`**: Unsplash API client for fallback food photography

---

## `docs/` - Documentation
- **`blueprint.md`**: Original project specification and design guidelines

---

## `workspace/` - Workspace Files
Contains additional workspace-related documentation.

---

## Key Architectural Patterns

### 1. **Separation of Concerns**
- **Frontend** (`src/app`, `src/components`): User interface and interactions
- **Backend** (`src/lib/actions.ts`): Server-side logic
- **AI Layer** (`src/ai/flows`): Isolated AI workflows
- **Services** (`src/services`): External API integrations

### 2. **Type Safety**
- Zod schemas in AI flows ensure structured outputs
- TypeScript types in `src/lib/types.ts` provide compile-time safety

### 3. **Modular AI Flows**
Each AI task is a separate, testable flow that can be developed and debugged independently using Genkit Dev UI.

### 4. **Component Reusability**
ShadCN UI provides a consistent, accessible component library that can be customized via Tailwind.

---

## Data Flow Example

```
User uploads image
    ↓
RecipeSageApp.tsx (handleImageUpload)
    ↓
lib/actions.ts (handleRecognizeIngredients)
    ↓
ai/flows/ingredient-recognition-from-image.ts
    ↓
Google Gemini Vision API
    ↓
Returns ingredient list
    ↓
Updates UI state in RecipeSageApp.tsx
```

---

## Development Workflow

1. **Frontend Development**: Edit components in `src/components/`
2. **AI Flow Development**: Test flows independently using `npm run genkit:dev`
3. **Integration**: Connect flows via Server Actions in `src/lib/actions.ts`
4. **Styling**: Customize Tailwind classes or modify `globals.css`
5. **Testing**: Run the full app with `npm run dev` on port 9002

---

## Adding New Features

### To add a new AI capability:
1. Create a new flow in `src/ai/flows/your-new-flow.ts`
2. Define input/output schemas with Zod
3. Add Server Action in `src/lib/actions.ts`
4. Call from frontend component

### To add a new UI component:
1. Use ShadCN CLI: `npx shadcn@latest add [component-name]`
2. Component will be added to `src/components/ui/`
3. Import and use in your pages/components

---

**Note**: This structure supports scalability while maintaining clear boundaries between concerns. Each folder has a single responsibility, making the codebase easy to navigate and maintain.
