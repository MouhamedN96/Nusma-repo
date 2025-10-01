# AI-Native React Native Web Boilerplate

A comprehensive AI-powered mobile and web app boilerplate using React Native with React Native for Web, designed specifically for building intelligent applications with maximum code sharing between platforms.

## Overview

This boilerplate demonstrates how to build **AI-native applications** that run on both mobile (iOS/Android) and web platforms using a shared codebase. It combines the power of React Native for mobile development with React Native for Web to create truly universal AI-powered applications with built-in support for:

- **Large Language Model (LLM) Integration**
- **Real-time AI Chat Interfaces**
- **Voice AI and Speech Recognition**
- **Computer Vision and Image Analysis**
- **AI-powered Content Generation**
- **Intelligent Data Processing**
- **Machine Learning Model Integration**

## Architecture

The project is structured to maximize code reuse while allowing platform-specific optimizations:

```
react-native-web-boilerplate/
├── mobile-web-app/          # Web application (React + React Native for Web)
├── mobile-native-app/       # React Native mobile application
├── shared/                  # Shared components and logic
│   ├── components/          # Reusable UI components
│   ├── hooks/              # Custom hooks
│   ├── services/           # API and business logic
│   ├── utils/              # Utility functions
│   └── types/              # TypeScript type definitions
├── docs/                   # Documentation
└── scripts/                # Build and deployment scripts
```

## Features

- **Universal Components**: Shared UI components that work on both web and mobile
- **Responsive Design**: Adaptive layouts for different screen sizes
- **State Management**: Redux Toolkit for predictable state management
- **Navigation**: React Navigation for mobile, React Router for web
- **API Integration**: Shared API layer with platform-specific optimizations
- **Testing**: Comprehensive test suite for both platforms
- **Development Tools**: Hot reloading, debugging, and profiling tools

## Technology Stack

### Core Technologies
- **React Native**: Mobile app framework
- **React Native for Web**: Web compatibility layer
- **React**: Web application library
- **TypeScript**: Type-safe development
- **Expo**: Development platform and tools

### State Management
- **Redux Toolkit**: Modern Redux with less boilerplate
- **React Query**: Server state management and caching

### Navigation
- **React Navigation**: Mobile navigation
- **React Router**: Web routing

### UI & Styling
- **Styled Components**: CSS-in-JS styling
- **React Native Elements**: Cross-platform UI components
- **Tailwind CSS**: Utility-first CSS framework (web)

### Development Tools
- **Metro**: JavaScript bundler for React Native
- **Vite**: Fast build tool for web
- **ESLint**: Code linting
- **Prettier**: Code formatting
- **Jest**: Testing framework

## Getting Started

### Prerequisites

- **Node.js** (16.x or later)
- **npm** or **yarn**
- **React Native CLI**
- **Expo CLI** (optional but recommended)
- **Android Studio** (for Android development)
- **Xcode** (for iOS development, macOS only)

### Installation

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd react-native-web-boilerplate
   ```

2. **Install dependencies**:
   ```bash
   # Install shared dependencies
   npm install
   
   # Install web app dependencies
   cd mobile-web-app
   npm install
   cd ..
   
   # Install mobile app dependencies
   cd mobile-native-app
   npm install
   cd ..
   ```

3. **Start development servers**:
   
   **Web Application**:
   ```bash
   cd mobile-web-app
   npm run dev
   ```
   
   **Mobile Application**:
   ```bash
   cd mobile-native-app
   npm start
   # Then press 'i' for iOS simulator or 'a' for Android emulator
   ```

## Development Workflow

### Shared Components

Create components in the `shared/components` directory that work across platforms:

```typescript
// shared/components/Button.tsx
import React from 'react';
import { TouchableOpacity, Text, StyleSheet } from 'react-native';

interface ButtonProps {
  title: string;
  onPress: () => void;
  variant?: 'primary' | 'secondary';
}

export const Button: React.FC<ButtonProps> = ({ title, onPress, variant = 'primary' }) => {
  return (
    <TouchableOpacity style={[styles.button, styles[variant]]} onPress={onPress}>
      <Text style={[styles.text, styles[`${variant}Text`]]}>{title}</Text>
    </TouchableOpacity>
  );
};

const styles = StyleSheet.create({
  button: {
    paddingHorizontal: 20,
    paddingVertical: 12,
    borderRadius: 8,
    alignItems: 'center',
  },
  primary: {
    backgroundColor: '#007AFF',
  },
  secondary: {
    backgroundColor: '#F2F2F7',
    borderWidth: 1,
    borderColor: '#C7C7CC',
  },
  text: {
    fontSize: 16,
    fontWeight: '600',
  },
  primaryText: {
    color: '#FFFFFF',
  },
  secondaryText: {
    color: '#007AFF',
  },
});
```

### Platform-Specific Code

Use platform-specific extensions for platform-specific implementations:

```typescript
// shared/services/storage.native.ts (for mobile)
import AsyncStorage from '@react-native-async-storage/async-storage';

export const storage = {
  getItem: AsyncStorage.getItem,
  setItem: AsyncStorage.setItem,
  removeItem: AsyncStorage.removeItem,
};

// shared/services/storage.web.ts (for web)
export const storage = {
  getItem: (key: string) => Promise.resolve(localStorage.getItem(key)),
  setItem: (key: string, value: string) => Promise.resolve(localStorage.setItem(key, value)),
  removeItem: (key: string) => Promise.resolve(localStorage.removeItem(key)),
};
```

### State Management

Use Redux Toolkit for shared state management:

```typescript
// shared/store/slices/userSlice.ts
import { createSlice, PayloadAction } from '@reduxjs/toolkit';

interface UserState {
  id: string | null;
  name: string | null;
  email: string | null;
  isAuthenticated: boolean;
}

const initialState: UserState = {
  id: null,
  name: null,
  email: null,
  isAuthenticated: false,
};

const userSlice = createSlice({
  name: 'user',
  initialState,
  reducers: {
    setUser: (state, action: PayloadAction<Omit<UserState, 'isAuthenticated'>>) => {
      state.id = action.payload.id;
      state.name = action.payload.name;
      state.email = action.payload.email;
      state.isAuthenticated = true;
    },
    clearUser: (state) => {
      state.id = null;
      state.name = null;
      state.email = null;
      state.isAuthenticated = false;
    },
  },
});

export const { setUser, clearUser } = userSlice.actions;
export default userSlice.reducer;
```

## Code Sharing Strategy

### What to Share

- **Business Logic**: API calls, data processing, validation
- **State Management**: Redux stores, actions, reducers
- **Utility Functions**: Date formatting, calculations, helpers
- **Type Definitions**: TypeScript interfaces and types
- **Constants**: API endpoints, configuration values

### Platform-Specific Considerations

- **Navigation**: Different navigation patterns for web vs mobile
- **Styling**: Responsive design for web, adaptive design for mobile
- **Interactions**: Mouse/keyboard vs touch interactions
- **Performance**: Different optimization strategies per platform

## Testing

### Unit Tests

```bash
# Run all tests
npm test

# Run tests for specific platform
npm run test:web
npm run test:mobile
```

### Integration Tests

```bash
# Run integration tests
npm run test:integration
```

### E2E Tests

```bash
# Web E2E tests
npm run test:e2e:web

# Mobile E2E tests
npm run test:e2e:mobile
```

## Building for Production

### Web Application

```bash
cd mobile-web-app
npm run build
```

### Mobile Application

**Android**:
```bash
cd mobile-native-app
npx react-native run-android --variant=release
```

**iOS**:
```bash
cd mobile-native-app
npx react-native run-ios --configuration Release
```

## Deployment

### Web Deployment

The web application can be deployed to any static hosting service:

- **Vercel**: `vercel deploy`
- **Netlify**: `netlify deploy`
- **AWS S3**: Upload build folder to S3 bucket

### Mobile Deployment

**Android**:
1. Generate signed APK or AAB
2. Upload to Google Play Console

**iOS**:
1. Archive in Xcode
2. Upload to App Store Connect

## Performance Optimization

### Code Splitting

Use dynamic imports for code splitting:

```typescript
const LazyComponent = React.lazy(() => import('./LazyComponent'));
```

### Bundle Analysis

Analyze bundle sizes:

```bash
# Web bundle analysis
cd mobile-web-app
npm run analyze

# Mobile bundle analysis
cd mobile-native-app
npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android-release.bundle --assets-dest android-release
```

## Best Practices

### Component Design

- Create platform-agnostic components when possible
- Use platform-specific components only when necessary
- Follow consistent naming conventions
- Implement proper TypeScript typing

### State Management

- Keep shared state minimal and focused
- Use local state for UI-specific data
- Implement proper error handling
- Use middleware for side effects

### Performance

- Optimize images for different screen densities
- Implement lazy loading for large lists
- Use memoization for expensive calculations
- Profile regularly on both platforms

## Troubleshooting

### Common Issues

1. **Metro bundler conflicts**: Clear cache with `npx react-native start --reset-cache`
2. **Web build issues**: Clear node_modules and reinstall dependencies
3. **Platform-specific bugs**: Use platform-specific code when necessary

### Debugging

- **Web**: Use browser developer tools
- **Mobile**: Use React Native Debugger or Flipper
- **Shared**: Use console.log and breakpoints

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass
6. Submit a pull request

## Resources

- [React Native Documentation](https://reactnative.dev/)
- [React Native for Web](https://necolas.github.io/react-native-web/)
- [Redux Toolkit](https://redux-toolkit.js.org/)
- [React Navigation](https://reactnavigation.org/)
- [Expo Documentation](https://docs.expo.dev/)

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

**Start Building Universal Apps!** 🚀

This boilerplate provides everything you need to build applications that work seamlessly across web and mobile platforms with maximum code reuse and optimal user experience on each platform.
