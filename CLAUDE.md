# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Flutter application (package name: `weiflutter`) currently at version 1.0.0+1. The project uses Flutter SDK 3.9.2+ and follows the standard Flutter application structure with support for multiple platforms (Android, iOS, Web, Linux, macOS, Windows).

### Project Goal
A medium-scale AI chat application featuring:
- **AI Chat**: Real-time streaming (SSE/WebSocket) with AI conversation
- **WebRTC**: Video/audio calling with AI digital humans
- **3D Integration**: Advanced 3D rendering using Three.js/Unity for digital avatars
- **Learning Project**: Teaching Flutter to a developer with React/Vue/H5 background

## Development Commands

### Running the Application
```bash
# Run on default device
flutter run

# Run on specific device
flutter devices  # List available devices
flutter run -d <device-id>

# Run with hot reload (default in debug mode)
# Press 'r' to hot reload, 'R' to hot restart
```

### Testing
```bash
# Run all tests
flutter test

# Run a specific test file
flutter test test/widget_test.dart

# Run with coverage
flutter test --coverage
```

### Code Quality
```bash
# Analyze code for issues
flutter analyze

# Format code
dart format lib/ test/

# Format specific file
dart format lib/main.dart
```

### Building
```bash
# Build for Android
flutter build apk          # Debug APK
flutter build apk --release  # Release APK
flutter build appbundle    # App bundle for Play Store

# Build for iOS (requires macOS)
flutter build ios

# Build for Web
flutter build web

# Build for desktop platforms
flutter build macos
flutter build linux
flutter build windows
```

### Dependency Management
```bash
# Install dependencies
flutter pub get

# Update dependencies
flutter pub upgrade

# Check for outdated packages
flutter pub outdated

# Clean build artifacts
flutter clean
```

## Architecture

### Current State
This is a minimal Flutter starter project with a single-file application (lib/main.dart) containing:
- `MyApp`: Root MaterialApp widget
- `MyHomePage`: Stateful widget demonstrating counter functionality
- Basic Material Design theming with ColorScheme

### Project Structure
- `lib/`: Main application code (currently only main.dart)
- `test/`: Widget and unit tests
- `android/`, `ios/`, `web/`, `linux/`, `macos/`, `windows/`: Platform-specific code and configuration
- `pubspec.yaml`: Dependencies and Flutter configuration
- `analysis_options.yaml`: Linter rules (uses package:flutter_lints/flutter.yaml)

### Dependencies
- Core: Flutter SDK
- UI: cupertino_icons (^1.0.8) for iOS-style icons
- Dev: flutter_test, flutter_lints (^5.0.0)

## Important Notes

- The project uses Material Design by default with `useMaterialDesign: true`
- Linting is configured via `flutter_lints` package with standard Flutter recommendations
- The app is currently not published (`publish_to: 'none'`)
- Supports Dart SDK version ^3.9.2

## Learning Path: From React/Vue to Flutter

### Phase 1: Flutter Basics (Week 1-2)
**Goal**: Understand Flutter's core concepts using React/Vue analogies

#### 1.1 Dart Language Fundamentals
**React/Vue → Flutter Mapping**:
- JavaScript/TypeScript → Dart (strongly typed, similar to TypeScript)
- `const`/`let` → `final`/`var`/`const`
- Arrow functions → Arrow syntax in Dart
- Async/await → Same in Dart (Future/async/await)
- Promises → Future
- Array methods (map, filter) → List methods

**Key Dart Concepts**:
```dart
// Variables (like TypeScript)
String name = 'Wei';           // Explicit type
var age = 25;                  // Type inference
final id = '123';              // Runtime constant (like const in JS)
const PI = 3.14;               // Compile-time constant

// Functions (similar to TypeScript)
String greet(String name) => 'Hello $name';  // Arrow function
void onClick() { }                           // Regular function

// Null safety (like TypeScript strict mode)
String? nullable;              // Can be null
String nonNull = 'value';      // Cannot be null
```

#### 1.2 Widget Concepts (React Components)
**React → Flutter**:
- JSX → Widget tree
- Components → Widgets
- `<div>` → `Container`, `SizedBox`, `Column`, `Row`
- Props → Constructor parameters
- State (useState) → StatefulWidget + setState
- Functional Components → StatelessWidget
- Class Components → StatefulWidget

**Example Comparison**:
```dart
// React Functional Component
// const MyButton = ({ title, onPress }) => (
//   <button onClick={onPress}>{title}</button>
// );

// Flutter StatelessWidget (equivalent)
class MyButton extends StatelessWidget {
  final String title;
  final VoidCallback onPress;

  const MyButton({
    required this.title,
    required this.onPress,
  });

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: onPress,
      child: Text(title),
    );
  }
}
```

#### 1.3 Layout System
**CSS Flexbox/Grid → Flutter Layout**:
- `display: flex; flex-direction: column` → `Column`
- `display: flex; flex-direction: row` → `Row`
- `justify-content` → `mainAxisAlignment`
- `align-items` → `crossAxisAlignment`
- `flex: 1` → `Expanded(flex: 1)`
- Absolute positioning → `Stack` + `Positioned`
- `padding` → `Padding` widget
- `margin` → Container's `margin`

**Example**:
```dart
// CSS: display: flex; flex-direction: column; justify-content: center;
Column(
  mainAxisAlignment: MainAxisAlignment.center,  // justify-content
  crossAxisAlignment: CrossAxisAlignment.start, // align-items
  children: [
    Text('Item 1'),
    Text('Item 2'),
  ],
)
```

### Phase 2: State Management (Week 3-4)
**Goal**: Master Flutter state management patterns

**React/Vue → Flutter State Management**:
- `useState` → `setState` (simple state)
- Context API → `InheritedWidget` (rare)
- Redux/Vuex → **Provider** (recommended)
- Redux Toolkit → **Riverpod** (modern choice)
- React Query → **Riverpod with AsyncNotifier**
- Zustand → **GetX** (simple, but opinionated)

**Recommended Stack for This Project**:
- **Riverpod 2.x**: Best for complex state, similar to Redux Toolkit + React Query
- **flutter_bloc**: Alternative (like Redux with more structure)

**Phase 2 Tasks**:
1. Local state with StatefulWidget
2. Provider basics (lifting state up)
3. Riverpod fundamentals (providers, consumers)
4. Async state management with Riverpod

### Phase 3: Navigation & Routing (Week 4)
**React Router/Vue Router → Flutter Navigation**:
- `<Route>` → `MaterialPageRoute`
- `useNavigate()` / `router.push()` → `Navigator.push()`
- Named routes → `Navigator.pushNamed()`
- Route parameters → Constructor parameters or arguments
- **go_router** package → Similar to React Router v6

**Key Concepts**:
```dart
// Push new screen (like router.push('/details'))
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => DetailScreen()),
);

// Pop back (like router.back())
Navigator.pop(context);

// Named routes (like Vue Router)
Navigator.pushNamed(context, '/details', arguments: {'id': 123});
```

### Phase 4: Network & API (Week 5)
**Fetch/Axios → Flutter HTTP**:
- `fetch()` → `http` package or `dio`
- Interceptors → `dio` interceptors
- WebSocket → `web_socket_channel`
- SSE → `sse_client` or custom implementation

**Recommended Packages**:
- **dio**: Like Axios (interceptors, retry, etc.)
- **retrofit**: Type-safe REST client (like TypeScript + Axios)
- **web_socket_channel**: WebSocket support
- **flutter_sse**: Server-Sent Events

**Example**:
```dart
// Fetch API → dio
final dio = Dio();
final response = await dio.get('https://api.example.com/data');
```

### Phase 5: Advanced Features (Week 6-8)

#### 5.1 Real-time Chat (SSE/WebSocket)
**Concepts**:
- Stream-based architecture (like RxJS Observables)
- `Stream` ≈ Observable in RxJS
- `StreamBuilder` ≈ React hooks with observables
- WebSocket ≈ Socket.io client

**Key Packages**:
- `web_socket_channel`: WebSocket
- `stream_channel`: Stream utilities
- Custom SSE implementation

#### 5.2 WebRTC Video Calling
**WebRTC in Flutter**:
- `flutter_webrtc`: WebRTC implementation
- Similar concepts to browser WebRTC API
- PeerConnection, MediaStream, etc.

**Key Packages**:
- **flutter_webrtc**: Core WebRTC
- **agora_rtc_engine**: Commercial solution (easier)
- **janus_client**: Open-source signaling

#### 5.3 3D Rendering
**Three.js/Unity → Flutter 3D**:
- **flutter_gl**: OpenGL ES bindings
- **three_dart**: Three.js port to Dart
- **flutter_unity_widget**: Embed Unity scenes
- **model_viewer**: glTF/GLB 3D model viewer
- Platform views for web Three.js

**Approach for Digital Humans**:
1. Use `flutter_unity_widget` for complex 3D avatars
2. Or `three_dart` for web-based 3D
3. Or platform-specific WebView with Three.js

### Phase 6: Project Architecture (Week 8-10)
**Recommended Structure**:
```
lib/
├── core/               # Core utilities (like utils/ in React)
│   ├── constants/
│   ├── theme/
│   └── utils/
├── data/              # Data layer (like services/ in Vue)
│   ├── models/
│   ├── repositories/
│   └── datasources/
├── domain/            # Business logic (optional, Clean Architecture)
│   ├── entities/
│   └── usecases/
├── presentation/      # UI layer (like components/ + pages/)
│   ├── screens/      # Pages
│   ├── widgets/      # Reusable components
│   └── providers/    # State management
├── services/          # External services (API, WebRTC, etc.)
└── main.dart
```

**Architecture Pattern**:
- **MVVM** (like Vue) - Recommended for beginners
- **Clean Architecture** - For scalability (advanced)
- **Feature-first** - Group by feature (like Next.js app router)

### Key Dependencies for Your Project
```yaml
dependencies:
  # State Management
  flutter_riverpod: ^2.5.1          # State management

  # Navigation
  go_router: ^14.0.0                 # Declarative routing

  # Network
  dio: ^5.4.0                        # HTTP client (like Axios)
  retrofit: ^4.1.0                   # Type-safe API client

  # WebSocket & SSE
  web_socket_channel: ^2.4.0         # WebSocket
  sse_client: ^1.0.0                 # Server-Sent Events

  # WebRTC
  flutter_webrtc: ^0.11.0           # WebRTC for video calls

  # 3D Rendering
  flutter_unity_widget: ^2022.2.0   # Unity integration
  three_dart: ^0.0.17               # Three.js port
  model_viewer_plus: ^1.7.0         # 3D model viewer

  # UI
  flutter_svg: ^2.0.9               # SVG support
  cached_network_image: ^3.3.1      # Image caching

  # Utilities
  logger: ^2.0.2                    # Logging
  shared_preferences: ^2.2.2        # Local storage (like localStorage)

dev_dependencies:
  build_runner: ^2.4.8              # Code generation
  retrofit_generator: ^8.1.0        # API generation
  riverpod_generator: ^2.3.9        # Riverpod codegen
```

### Learning Resources
1. **Official Docs**: https://docs.flutter.dev
2. **DartPad**: https://dartpad.dev (online playground)
3. **Widget Catalog**: https://docs.flutter.dev/ui/widgets
4. **Riverpod Docs**: https://riverpod.dev
5. **WebRTC Example**: https://github.com/flutter-webrtc/flutter-webrtc-demo

### React/Vue vs Flutter Quick Reference

| Concept | React/Vue | Flutter |
|---------|-----------|---------|
| Component | Functional Component | StatelessWidget |
| Stateful Component | useState/data() | StatefulWidget |
| Props | props | Constructor params |
| Event Handlers | onClick, onChange | onPressed, onChanged |
| Conditional Render | `{condition && <div>}` | `if (condition) Widget()` |
| List Render | `.map()` | `.map().toList()` |
| Lifecycle | useEffect/mounted | initState/dispose |
| Context | useContext/inject | Provider/Riverpod |
| Styling | CSS/styled-components | Widget properties |
| Async | async/await | async/await + Future |
| Reactive Data | useState/ref | ValueNotifier/Stream |