# 🍳 RecipeSage - AI-Powered Culinary Assistant

RecipeSage is an intelligent web application that leverages generative AI to help users discover recipes based on available ingredients. By combining computer vision for ingredient recognition and natural language processing for recipe generation, the system aims to reduce food waste and simplify meal planning. Users can either manually input ingredients or upload images of their fridge contents to receive personalized recipe recommendations with nutritional information and allergen detection.

## ✨ Features

- **Ingredient Recognition from Images**: Upload photos of your fridge or pantry, and the AI automatically detects and lists available ingredients using Google Gemini Vision
- **Smart Recipe Generation**: Generate 5-6 creative recipes based on your ingredients, with optional location-aware and weather-based suggestions
- **Nutritional Analysis**: Get detailed nutritional breakdowns including calories, protein, carbohydrates, and fats for any recipe
- **Allergen Detection & Alerts**: Specify your allergies and receive warnings if recipes contain potential allergens
- **Visual Recipe Cards**: Each recipe is accompanied by relevant food imagery fetched from Unsplash or Google Custom Search
- **Responsive UI**: Modern, mobile-friendly interface built with Tailwind CSS and ShadCN UI components

## 🎯 Problem Statement

Managing meal planning with available ingredients while considering dietary restrictions and nutritional needs can be time-consuming. RecipeSage addresses this by:
- Automating ingredient identification from images
- Generating recipes that maximize ingredient utilization to minimize waste
- Providing instant nutritional and allergen information
- Offering location and weather-aware meal suggestions

## 🛠️ Tech Stack

### Frontend
- **Next.js 15** - React framework with App Router
- **React 18** - UI library
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first styling
- **ShadCN UI** - Pre-built accessible components

### Backend & AI
- **Google Genkit** - AI orchestration framework
- **Google Gemini** - Large language models for text and vision tasks
- **Zod** - Schema validation and type inference

### External APIs
- **Google Custom Search API** - Recipe image fetching
- **Unsplash API** - Fallback image source
- **Geolocation API** - Location-based recommendations

## 📐 Project Architecture

```
User Input (Text/Image)
         ↓
┌────────────────────────┐
│  Next.js Frontend      │
│  - Recipe UI           │
│  - Image Upload        │
│  - Form Handling       │
└────────┬───────────────┘
         ↓
┌────────────────────────┐
│  Server Actions        │
│  (lib/actions.ts)      │
└────────┬───────────────┘
         ↓
┌────────────────────────┐
│  Genkit AI Flows       │
│  - Ingredient Recog.   │
│  - Recipe Generation   │
│  - Nutrition Analysis  │
│  - Allergen Detection  │
└────────┬───────────────┘
         ↓
┌────────────────────────┐
│  Google Gemini API     │
└────────┬───────────────┘
         ↓
┌────────────────────────┐
│  Image Services        │
│  (Google/Unsplash)     │
└────────────────────────┘
         ↓
    Recipe Output
```

### Workflow
1. **Input Stage**: User provides ingredients via text or uploads an image
2. **Recognition Stage** (if image): Gemini Vision processes the image and extracts ingredient list
3. **Generation Stage**: Gemini Pro generates recipes considering ingredients, location, and weather
4. **Enhancement Stage**: System fetches relevant images and computes nutritional data
5. **Safety Check**: Allergen detection runs if user has specified allergies
6. **Display Stage**: Recipes rendered with images, instructions, and nutritional facts

## 🚀 Installation & Setup

### Prerequisites
- Node.js 20.x or higher
- npm, yarn, or pnpm package manager
- API keys for Google AI, Google Custom Search, and Unsplash

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/Vignan2659/Recipe-Sage.git
   cd Recipe-Sage-main
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment variables**
   
   Create a `.env.local` file in the root directory:
   ```env
   GOOGLE_API_KEY=your_google_ai_api_key
   GOOGLE_CUSTOM_SEARCH_CX=your_custom_search_engine_id
   UNSPLASH_ACCESS_KEY=your_unsplash_access_key
   ```

   **How to obtain API keys:**
   - **GOOGLE_API_KEY**: Get it from [Google AI Studio](https://makersuite.google.com/app/apikey)
   - **GOOGLE_CUSTOM_SEARCH_CX**: Create a custom search engine at [Google Custom Search](https://programmablesearchengine.google.com/)
   - **UNSPLASH_ACCESS_KEY**: Register at [Unsplash Developers](https://unsplash.com/developers)

4. **Run the development server**
   ```bash
   npm run dev
   ```

5. **Access the application**
   
   Open [http://localhost:9002](http://localhost:9002) in your browser

## 📖 How to Run

### Development Mode
```bash
npm run dev
```
Starts the Next.js development server with Turbopack on port 9002

### Genkit Development Mode (for AI flow testing)
```bash
npm run genkit:dev
```
Launches Genkit Developer UI for testing AI flows independently

### Production Build
```bash
npm run build
npm start
```

### Type Checking
```bash
npm run typecheck
```

## 💡 Usage

1. **Manual Ingredient Entry**: Type ingredients separated by commas or line breaks
2. **Image Upload**: Click the camera icon and upload a photo of your fridge
3. **Generate Recipes**: Click "Generate Recipes" to receive AI-powered suggestions
4. **View Details**: Click on any recipe card to see full instructions and nutritional info
5. **Check Allergens**: Input your allergies in the recipe details to get safety warnings

## 📊 Sample Output

The application generates recipe cards containing:
- Recipe name and description
- Complete ingredient list
- Step-by-step cooking instructions
- Context notes (chef tips, serving suggestions)
- High-quality food images
- Nutritional facts (calories, protein, carbs, fats)
- Allergen warnings (if applicable)

## 🧪 Technologies & Algorithms

### Computer Vision
- **Model**: Google Gemini 1.5 Vision (gemini-1.5-flash)
- **Task**: Multi-modal image analysis for ingredient detection
- **Input**: Base64-encoded image data URI
- **Output**: Structured list of detected ingredients

### Natural Language Processing
- **Model**: Google Gemini 1.5 Pro (gemini-1.5-flash)
- **Task**: Recipe generation, nutritional analysis, allergen detection
- **Techniques**: Prompt engineering with structured output schemas (Zod)
- **Context Awareness**: Location and weather data integration

### Image Retrieval
- **Primary**: Google Custom Search API with image search filters
- **Fallback**: Unsplash API for high-quality food photography

## 📁 Repository Structure

```
Recipe-Sage-main/
├── src/
│   ├── ai/                          # AI orchestration layer
│   │   ├── genkit.ts                # Genkit configuration
│   │   ├── dev.ts                   # Development entry point
│   │   └── flows/                   # AI workflow definitions
│   │       ├── generate-recipes-from-ingredients.ts
│   │       ├── ingredient-recognition-from-image.ts
│   │       ├── nutrition-facts-for-recipe.ts
│   │       ├── allergen-detection-in-recipes.ts
│   │       └── generate-recipe-image.ts
│   ├── app/                         # Next.js App Router pages
│   │   ├── layout.tsx               # Root layout
│   │   ├── page.tsx                 # Home page
│   │   └── globals.css              # Global styles
│   ├── components/                  # React components
│   │   ├── RecipeSageApp.tsx        # Main application component
│   │   ├── RecipeCard.tsx           # Recipe display card
│   │   ├── RecipeDetails.tsx        # Detailed recipe view
│   │   ├── layout/                  # Layout components
│   │   └── ui/                      # ShadCN UI components
│   ├── hooks/                       # Custom React hooks
│   ├── lib/                         # Utility libraries
│   │   ├── actions.ts               # Server actions
│   │   ├── types.ts                 # TypeScript type definitions
│   │   ├── utils.ts                 # Helper functions
│   │   └── placeholder-images.ts    # Image fallback logic
│   └── services/                    # External API integrations
│       ├── google-search.ts         # Google Custom Search wrapper
│       └── unsplash.ts              # Unsplash API wrapper
├── docs/
│   └── blueprint.md                 # Project specification
├── next.config.ts                   # Next.js configuration
├── tailwind.config.ts               # Tailwind CSS configuration
├── tsconfig.json                    # TypeScript configuration
├── package.json                     # Dependencies and scripts
└── README.md                        # Project documentation
```

### Key Files Explained

- **`src/ai/flows/`**: Contains modular AI workflows for specific tasks (recipe generation, ingredient recognition, etc.)
- **`src/lib/actions.ts`**: Server-side functions that bridge frontend and AI flows
- **`src/components/RecipeSageApp.tsx`**: Main UI component handling user interactions and state management
- **`next.config.ts`**: Configures image domains and build settings
- **`apphosting.yaml`**: Deployment configuration for Firebase App Hosting

## 👥 Contributors

This project was developed as an academic collaborative effort:

- **Vignan** - [GitHub](https://github.com/Vignan2659)
- **Contributor 2** - *(Add collaborator details)*

## 🔮 Future Enhancements

- User authentication and recipe bookmarking with Firebase
- Meal planning calendar with weekly schedules
- Dietary preference filters (vegan, keto, gluten-free)
- Recipe sharing and community ratings
- Voice input for hands-free cooking
- Integration with grocery delivery APIs

## 📄 License

This project is created for educational purposes. Please ensure you comply with the terms of service for all external APIs used (Google, Unsplash).

## 🙏 Acknowledgments

- Google Genkit team for the AI orchestration framework
- ShadCN for the beautiful UI component library
- Unsplash photographers for food imagery
- Next.js team for the robust React framework

---

**Note**: This is an academic project demonstrating the integration of generative AI with modern web technologies. API keys are required for full functionality
