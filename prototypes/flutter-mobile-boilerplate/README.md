# AI-Native Flutter Mobile Boilerplate

A comprehensive AI-powered cross-platform mobile app boilerplate built with Flutter for rapid prototyping and development of intelligent iOS and Android applications.

## Overview

This boilerplate provides a solid foundation for building **AI-native cross-platform mobile applications** with Flutter. It includes essential AI service integrations, secure credential management, and a well-structured architecture specifically designed for intelligent applications.

## AI-First Features

- **Large Language Model (LLM) Integration**: OpenAI, Anthropic, Google AI, Azure OpenAI
- **Voice AI**: Speech-to-text, text-to-speech, real-time voice processing
- **Computer Vision**: Image analysis, object detection, OCR capabilities
- **On-Device AI**: TensorFlow Lite, Google ML Kit integration
- **Vector Databases**: Pinecone, Weaviate, Supabase Vector support
- **Real-time AI Chat**: Streaming responses, conversation memory
- **AI-Powered Content Generation**: Text, images, code generation
- **Intelligent Data Processing**: Document analysis, data extraction
- **Offline AI Capabilities**: On-device model inference
- **Biometric AI**: Face recognition, voice authentication

## Core Features

- **Cross-Platform**: Single codebase for both iOS and Android
- **AI-Native Architecture**: Built specifically for AI-powered applications
- **Secure Credential Management**: Comprehensive .env configuration
- **State Management**: Provider pattern with AI-specific state handling
- **Navigation**: Declarative routing with go_router
- **Responsive Design**: Adaptive UI components optimized for AI interfaces
- **Development Tools**: Pre-configured debugging and testing setup for AI features

## Prerequisites

Before you begin, ensure you have the following installed:

### Core Development Tools
- **Flutter SDK** (3.24.5 or later)
- **Dart** (3.5.4 or later)
- **Android Studio** (for Android development)
- **Xcode** (for iOS development, macOS only)
- **Visual Studio Code** (recommended editor with Flutter extensions)

### AI Development Requirements
- **Python** (3.8 or later) for AI model integration and data processing
- **Node.js** (16.x or later) for backend AI services
- **Git** for version control
- **Docker** (optional, for containerized AI services)

### Virtual Environment Setup
This boilerplate supports multiple virtual environment configurations:

#### Python Virtual Environment (for AI scripts)
```bash
# Create Python virtual environment
python -m venv ai_env

# Activate virtual environment
# On macOS/Linux:
source ai_env/bin/activate
# On Windows:
ai_env\Scripts\activate

# Install AI dependencies
pip install -r requirements.txt
```

#### Flutter Environment Management
```bash
# Use Flutter Version Management (FVM) for consistent Flutter versions
dart pub global activate fvm
fvm install 3.24.5
fvm use 3.24.5
```

## Quick Start

1. **Clone the repository**:
   ```bash
   git clone <repository-url>
   cd flutter-mobile-boilerplate
   ```

2. **Set up virtual environment**:
   ```bash
   # Create and activate Python virtual environment
   python -m venv ai_env
   source ai_env/bin/activate  # On Windows: ai_env\Scripts\activate
   
   # Install Python AI dependencies
   pip install -r requirements.txt
   
   # Set up Flutter environment (optional but recommended)
   dart pub global activate fvm
   fvm use 3.24.5
   ```

3. **Configure environment variables**:
   ```bash
   # Copy the example environment file
   cp .env.example .env
   
   # Edit .env file with your actual API keys and credentials
   # IMPORTANT: Never commit .env files to version control!
   ```

4. **Install Flutter dependencies**:
   ```bash
   flutter pub get
   ```

5. **Run the app**:
   ```bash
   # For development with hot reload
   flutter run
   
   # For specific platform
   flutter run -d ios
   flutter run -d android
   
   # For release build
   flutter run --release
   ```

## Project Structure

```
lib/
├── main.dart                 # Application entry point
├── app/
│   ├── app.dart             # Main app configuration
│   └── routes.dart          # Route definitions
├── core/
│   ├── constants/           # App constants
│   ├── themes/              # Theme configurations
│   └── utils/               # Utility functions
├── features/
│   ├── home/                # Home feature module
│   │   ├── models/
│   │   ├── providers/
│   │   ├── screens/
│   │   └── widgets/
│   └── shared/              # Shared components
│       ├── models/
│       ├── providers/
│       └── widgets/
└── services/
    ├── api/                 # API service layer
    ├── storage/             # Local storage
    └── navigation/          # Navigation service
```

## Key Dependencies

| Package | Purpose | Version |
|---------|---------|---------|
| `provider` | State management | ^6.1.2 |
| `go_router` | Declarative routing | ^14.2.7 |
| `shared_preferences` | Local storage | ^2.3.2 |
| `http` | HTTP client | ^1.2.2 |
| `flutter_svg` | SVG support | ^2.0.10+1 |

## Development Guidelines

### State Management

This boilerplate uses the Provider pattern for state management:

```dart
class CounterProvider extends ChangeNotifier {
  int _count = 0;
  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}
```

### Navigation

Routes are defined using go_router:

```dart
final router = GoRouter(
  routes: [
    GoRoute(
      path: '/',
      builder: (context, state) => const HomeScreen(),
    ),
  ],
);
```

### Theming

The app supports both light and dark themes:

```dart
ThemeData lightTheme = ThemeData(
  brightness: Brightness.light,
  primarySwatch: Colors.blue,
);
```

## Building for Production

### Android

```bash
flutter build apk --release
# or for app bundle
flutter build appbundle --release
```

### iOS

```bash
flutter build ios --release
```

## Testing

Run tests with:

```bash
# Unit tests
flutter test

# Integration tests
flutter test integration_test/
```

## Customization

### Adding New Features

1. Create a new directory under `lib/features/`
2. Follow the established structure (models, providers, screens, widgets)
3. Register providers in `main.dart`
4. Add routes in `app/routes.dart`

### Styling

- Modify `core/themes/` for global theme changes
- Use consistent spacing and colors defined in constants
- Follow Material Design guidelines

## Performance Optimization

- Use `const` constructors where possible
- Implement lazy loading for large lists
- Optimize images and assets
- Profile your app regularly with Flutter DevTools

## Deployment

### Android Play Store

1. Configure signing in `android/app/build.gradle`
2. Build release APK or App Bundle
3. Upload to Google Play Console

### iOS App Store

1. Configure signing in Xcode
2. Build for release
3. Upload via Xcode or Application Loader

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## Resources

- [Flutter Documentation](https://docs.flutter.dev/)
- [Dart Language Tour](https://dart.dev/guides/language/language-tour)
- [Provider Package](https://pub.dev/packages/provider)
- [Go Router Package](https://pub.dev/packages/go_router)

## License

This project is licensed under the MIT License - see the LICENSE file for details.

---

**Happy Coding!** 🚀

This boilerplate is designed to get you up and running quickly with Flutter mobile development. Customize it according to your project needs and start building amazing cross-platform applications.
