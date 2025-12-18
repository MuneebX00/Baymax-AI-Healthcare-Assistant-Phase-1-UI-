# Baymax – AI Healthcare Assistant Documentation

## Table of Contents
1. [Project Overview](#project-overview)
2. [Tech Stack](#tech-stack)
3. [Project Structure](#project-structure)
4. [Getting Started](#getting-started)
5. [Component Architecture](#component-architecture)
6. [API Routes](#api-routes)
7. [Type System](#type-system)
8. [Styling & UI](#styling--ui)
9. [Development Workflow](#development-workflow)
10. [Deployment](#deployment)
11. [Contributing Guidelines](#contributing-guidelines)

---

## Project Overview

Baymax is an AI-powered healthcare assistant web application built with modern web technologies. It provides users with interactive chat-based medical guidance, symptom checking, and health-related Q&A through an intuitive conversational interface.

### Key Features
- **Real-time Chat Interface**: Interactive messaging with instant responses
- **Quick Actions**: Pre-built healthcare question suggestions
- **Emergency Detection**: System capable of identifying and flagging urgent health concerns
- **Responsive Design**: Mobile-friendly interface that works across all devices
- **Message History**: Persistent conversation tracking with timestamps
- **Loading States**: Visual feedback during AI processing

---

## Tech Stack

### Frontend
- **Framework**: [Next.js 16.0.10](https://nextjs.org) - React-based full-stack framework
- **React**: 19.2.1 - UI library
- **TypeScript**: 5.x - Type-safe JavaScript
- **Styling**:
  - **Tailwind CSS**: 4.x - Utility-first CSS framework
  - **PostCSS**: 4.x - CSS processing
- **Animations**: [Framer Motion 12.23.26](https://www.framer.com/motion/) - Advanced animations
- **Icons**: [Lucide React 0.561.0](https://lucide.dev) - Beautiful SVG icons

### Backend
- **API Routes**: Next.js API routes in `src/app/api/`
- **Chat Endpoint**: `/api/chat` - Handles AI conversations

### Development Tools
- **ESLint**: 9.x - Code linting and formatting
- **Utilities**: clsx, tailwind-merge - CSS utility helpers

---

## Project Structure

```
Baymax – AI Healthcare Assistant/
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   └── chat/
│   │   │       └── route.ts          # Chat API endpoint
│   │   ├── layout.tsx                # Root layout component
│   │   ├── page.tsx                  # Home page
│   │   └── globals.css               # Global styles
│   ├── components/
│   │   ├── ChatContainer.tsx         # Main chat interface container
│   │   ├── ChatInput.tsx             # Message input component
│   │   ├── MessageBubble.tsx         # Individual message display
│   │   ├── Header.tsx                # Top navigation/header
│   │   └── Footer.tsx                # Bottom footer
│   ├── lib/
│   │   └── utils.ts                  # Utility functions (cn, etc.)
│   └── types/
│       └── chat.ts                   # TypeScript interfaces
├── public/                            # Static assets
├── eslint.config.mjs                 # ESLint configuration
├── next.config.ts                    # Next.js configuration
├── tsconfig.json                     # TypeScript configuration
├── postcss.config.mjs                # PostCSS configuration
├── package.json                      # Dependencies and scripts
├── README.md                         # Quick start guide
└── DOCUMENTATION.md                  # This file
```

### Directory Descriptions

| Directory | Purpose |
|-----------|---------|
| `src/app` | Next.js App Router - pages and API routes |
| `src/components` | Reusable React components |
| `src/lib` | Utility functions and helpers |
| `src/types` | TypeScript type definitions and interfaces |
| `public` | Static files (images, fonts, etc.) |

---

## Getting Started

### Prerequisites
- **Node.js**: 18.17 or later
- **npm** or **yarn** or **pnpm** or **bun**

### Installation

1. **Clone the repository** (or download the project)
   ```bash
   cd "e:/substance/Baymax – AI Healthcare Assistant"
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   # or
   pnpm install
   # or
   bun install
   ```

3. **Set up environment variables** (if needed)
   Create a `.env.local` file in the root directory:
   ```env
   # Add any API keys or configuration here
   NEXT_PUBLIC_API_URL=http://localhost:3000
   ```

### Running Development Server

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser. The application will hot-reload as you make changes.

---

## Component Architecture

### Component Hierarchy

```
layout.tsx (Root Layout)
└── page.tsx (Home Page)
    ├── Header.tsx
    ├── ChatContainer.tsx
    │   ├── MessageBubble.tsx (multiple)
    │   └── Quick Actions Display
    └── ChatInput.tsx
└── Footer.tsx
```

### Core Components

#### **ChatContainer.tsx**
- **Purpose**: Main chat interface wrapper
- **Props**: 
  - `messages: Message[]` - Array of chat messages
  - `isLoading: boolean` - Loading state indicator
  - `onSendMessage: (text: string) => void` - Callback for message submission
- **Features**:
  - Auto-scrolling to latest messages
  - Quick action buttons for common health questions
  - Animated message transitions
  - Emergency banner display
  - Conversation context notice

#### **ChatInput.tsx**
- **Purpose**: Message input field and send button
- **Features**:
  - Text input with send functionality
  - Keyboard handling (Enter to send)
  - Disabled state during loading
  - Visual feedback during message sending

#### **MessageBubble.tsx**
- **Purpose**: Display individual messages
- **Props**: `message: Message`
- **Styling**:
  - User messages: Right-aligned, styled differently from AI responses
  - AI (Baymax) messages: Left-aligned with bot indicator
  - Emergency messages: Special highlighting

#### **Header.tsx**
- **Purpose**: Top navigation and branding
- **Includes**: Logo, title, and navigation elements

#### **Footer.tsx**
- **Purpose**: Application footer
- **Includes**: Links, copyright, or additional information

---

## API Routes

### Chat API Endpoint

**Route**: `POST /api/chat`

**Purpose**: Handles AI-powered responses to user healthcare queries

**Request Body**:
```typescript
{
  message: string;        // User's message
  conversationId?: string; // Optional conversation ID for context
}
```

**Response**:
```typescript
{
  reply: string;          // AI response
  isEmergency?: boolean;  // Flag if emergency detected
  conversationId: string; // Conversation tracking ID
}
```

**Implementation**: See [src/app/api/chat/route.ts](src/app/api/chat/route.ts)

---

## Type System

### Chat Types

**File**: [src/types/chat.ts](src/types/chat.ts)

```typescript
export interface Message {
    id: string;                 // Unique message identifier
    text: string;              // Message content
    sender: 'user' | 'baymax'; // Message originator
    timestamp: Date;            // When message was created
    isEmergency?: boolean;      // Flag for urgent health concerns
}
```

---

## Styling & UI

### Tailwind CSS
The project uses **Tailwind CSS 4.x** for styling with a utility-first approach.

### Global Styles
- **Location**: [src/app/globals.css](src/app/globals.css)
- **Includes**: Base styles, custom utilities, and theme configuration

### Component Styling
- All components use Tailwind utility classes
- `cn()` utility (from `clsx` and `tailwind-merge`) for conditional class merging
- Responsive design with mobile-first approach

### Icons
- Lucide React provides beautiful SVG icons
- Used for visual indicators in quick actions and UI elements

### Animations
- **Framer Motion** handles component animations
- Smooth transitions on message entry/exit
- Quick action hover effects

---

## Development Workflow

### Code Editing
1. Edit files in `src/`
2. Changes automatically reflect in the browser (hot reload)
3. TypeScript provides real-time type checking

### Building
```bash
npm run build
# Compiles TypeScript and optimizes for production
```

### Linting
```bash
npm run lint
# Runs ESLint to check code quality
```

### Project Scripts

| Script | Purpose |
|--------|---------|
| `npm run dev` | Start development server |
| `npm run build` | Create optimized production build |
| `npm start` | Run production server |
| `npm run lint` | Check code with ESLint |

---

## Deployment

### Deploy on Vercel

The easiest way to deploy Baymax is using **Vercel** (creators of Next.js):

1. **Push code to GitHub**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin <your-github-repo>
   git push -u origin main
   ```

2. **Connect to Vercel**
   - Visit [vercel.com/new](https://vercel.com/new)
   - Select your GitHub repository
   - Vercel auto-detects Next.js and sets up build settings
   - Click Deploy

3. **Environment Variables**
   - Add any `.env.local` variables in Vercel project settings
   - Redeploy if variables change

### Alternative Deployment Options
- **Docker**: Containerize with Dockerfile
- **Self-hosted**: Use `npm run build` and `npm start`
- **Other Platforms**: Netlify, AWS, Google Cloud, etc.

**Documentation**: [Next.js Deployment Docs](https://nextjs.org/docs/app/building-your-application/deploying)

---

## Contributing Guidelines

### Code Style
- Use **TypeScript** for type safety
- Follow ESLint rules
- Use Tailwind CSS for styling
- Keep components small and focused

### File Organization
- One component per file (when possible)
- Group related utilities in `lib/`
- Keep types organized in `types/`
- API routes follow file-based routing in `app/api/`

### Component Development
1. Create component file in `src/components/`
2. Define TypeScript interfaces for props
3. Use functional components with hooks
4. Export component as default
5. Add component to parent as needed

### Git Workflow
```bash
# Create feature branch
git checkout -b feature/feature-name

# Make changes and commit
git add .
git commit -m "Description of changes"

# Push and create pull request
git push origin feature/feature-name
```

### Testing
- Test locally before pushing: `npm run build && npm start`
- Check console for TypeScript errors
- Verify responsive design on mobile

---

## Troubleshooting

### Common Issues

**Issue**: Port 3000 already in use
```bash
npm run dev -- -p 3001  # Use different port
```

**Issue**: Module not found errors
```bash
rm -rf node_modules package-lock.json
npm install  # Reinstall dependencies
```

**Issue**: TypeScript errors
```bash
npx tsc --noEmit  # Check for type errors
```

---

## Additional Resources

- **Next.js Documentation**: https://nextjs.org/docs
- **React Documentation**: https://react.dev
- **Tailwind CSS**: https://tailwindcss.com
- **TypeScript**: https://www.typescriptlang.org
- **Framer Motion**: https://www.framer.com/motion/

---

## License

This project is part of the Baymax AI Healthcare Assistant suite.

---

**Last Updated**: December 18, 2025
