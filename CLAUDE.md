# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

TabX is a Chrome extension for tab management, inspired by OneTab. It's built with TypeScript, React, and Recoil for state management. The extension allows users to save their open tabs and manage them with features like fuzzy search, dark mode, and import/export capabilities.

## Common Commands

### Development
- `npm install` - Install dependencies
- `npm run dev` - Start development mode with hot reload
- `npm run build` - Build production extension
- `npm run test` - Run Jest tests
- `npm run lint` - Run ESLint
- `npm run lint:fix` - Auto-fix linting issues
- `npm run lint:css` - Run Stylelint on styled-components

### Testing
- Tests are located in `src/test/`
- Run a specific test file: `npm run test -- src/test/unit/core/services/tabService.spec.ts`
- Tests use Jest with TypeScript support via ts-jest
- Mocks for Chrome API are in `src/test/__mocks__/chromeMock.ts`

## Code Architecture

### Extension Structure
- **Background Script**: `src/background.ts` - Handles browser action clicks and manages tab storage
- **Main UI**: `src/ui/` - React application for tab management interface
- **Core Logic**: `src/core/` - Business logic organized in layers:
  - `services/` - Core business logic (tabService, chromeActionService)
  - `useCase/` - Application use cases
  - `repos/` - Storage layer using Chrome storage API
  - `factory/` - Entity creation factories
  - `errors/` - Custom error types

### State Management
- Uses Recoil for state management (`src/ui/stores/`)
- Key atoms: tabLists, tabs, colorTheme, lang
- State is persisted using Chrome storage API

### Key Dependencies
- React 17 with TypeScript
- Recoil for state management
- Styled-components for styling
- Fuse.js for fuzzy search
- i18next for internationalization (English and Japanese)
- Webpack for bundling

### Build Output
- Development build: Extension files are output to `dist/` directory
- The manifest.json is copied from `src/manifest.json`
- Background script and UI are built as separate bundles

### Chrome Extension Permissions
- `storage` - For persisting tab data
- `tabs` - For accessing and managing browser tabs

### Import Aliases
- `~/` maps to `src/` directory (configured in TypeScript and Jest)

## Extension Loading
After building, load the extension in Chrome:
1. Go to chrome://extensions/
2. Enable Developer mode
3. Click "Load unpacked"
4. Select the `dist` directory