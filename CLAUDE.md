# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is a React Native monorepo containing three standalone applications:
- **RepackApp**: Main application using @callstack/repack for webpack-based bundling
- **MicroApp1**: Micro application 1 (React Native)
- **MicroApp2**: Micro application 2 (React Native)

## Technology Stack

All three applications share the same technology stack:
- **React Native**: 0.81.5
- **TypeScript**: 5.8.3
- **@callstack/repack**: 5.2.2 (webpack-based bundler for React Native)
- **Rspack**: 1.3.4 (Rust-based bundler alternative)
- **Metro**: React Native's default JavaScript bundler
- **Jest**: 29.6.3 (testing framework)
- **ESLint**: 8.19.0 (with @react-native config)
- **Prettier**: 2.8.8 (code formatting)

## Common Development Commands

All three applications have identical npm scripts. Run these from each app's directory:

```bash
# Start the Metro bundler
npm start

# Run on Android
npm run android

# Run on iOS
npm run ios

# Run linting
npm run lint

# Run tests
npm test
```

### Testing

Tests are located in `__tests__/App.test.tsx` in each app. To run a single test file:

```bash
npm test App.test.tsx
```

## Architecture & Configuration

### Bundling Strategy

Each app supports multiple bundling approaches:

1. **Metro** (default React Native bundler)
   - Config: `metro.config.js`
   - Use when running `npm start`

2. **Rspack with Re.Pack** (webpack-based bundler)
   - Config: `rspack.config.mjs`
   - Uses `@callstack/repack` for React Native compatibility
   - SWC loader for faster transpilation

### Key Configuration Files

Each application contains:

- **metro.config.js**: Metro bundler configuration
- **rspack.config.mjs**: Rspack bundler configuration with Re.Pack defaults
- **jest.config.js**: Jest testing preset (uses `react-native` preset)
- **.eslintrc.js**: ESLint configuration (extends @react-native)
- **.prettierrc.js**: Prettier configuration
- **react-native.config.js**: React Native CLI configuration
- **babel.config.js**: Babel transpiler configuration
- **tsconfig.json**: TypeScript configuration

### Test Configuration

All apps use Jest with the `react-native` preset:

```javascript
module.exports = {
  preset: 'react-native',
};
```

Tests use React Test Renderer and follow the pattern:

```typescript
import React from 'react';
import ReactTestRenderer from 'react-test-renderer';
import App from '../App';

test('renders correctly', async () => {
  await ReactTestRenderer.act(() => {
    ReactTestRenderer.create(<App />);
  });
});
```

### Code Structure

Each app follows React Native's standard structure:
- `App.tsx`: Main application component
- `__tests__/App.test.tsx`: Main app tests
- `index.js`: Application entry point
- Native platform folders: `android/`, `ios/`
- Configuration files at root level

### Requirements

- **Node.js**: >= 20
- **Ruby** (for iOS): Required for CocoaPods (use `bundle install` and `bundle exec pod install`)
- **Platform-specific setup**: Follow [React Native environment setup](https://reactnative.dev/docs/set-up-your-environment)

## Development Notes

- Each app is completely independent with its own `node_modules`
- All three apps use identical dependencies and configuration
- The repository uses React Native's standard CLI commands
- Fast Refresh is enabled for hot reloading during development
- Code follows React Native's standard patterns and conventions
