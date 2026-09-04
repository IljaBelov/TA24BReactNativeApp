# React Native: First Testable App in VS Code

This guide creates a React Native application with **Expo**, the simplest
recommended setup for a first project. Expo runs on Android, iOS, and the web
and lets you test on a physical phone without installing a full native
development environment.

## 1. Install the prerequisites

Install these applications:

1. **Node.js LTS** from [nodejs.org](https://nodejs.org/).
2. **Visual Studio Code** from [code.visualstudio.com](https://code.visualstudio.com/).
3. **Git** from [git-scm.com](https://git-scm.com/), if it is not already installed.
4. **Expo Go** from the Google Play Store or Apple App Store on a physical
   Android or iOS phone.

Open a terminal and confirm that Node and npm are available:

```powershell
node --version
npm --version
```

For Android emulator testing, install **Android Studio**, the Android SDK, and
an Android Virtual Device. For iOS simulator testing, use a Mac with Xcode;
the iOS simulator cannot run on Windows.

## 2. Create the project

In VS Code, select **File > Open Folder**, choose the parent directory where
the project should live, and open the integrated terminal with
**Terminal > New Terminal**.

Run:

```powershell
npx create-expo-app@latest MyFirstApp
cd MyFirstApp
code .
```

If prompted to choose a template, select the default blank TypeScript
template. The command creates the project and installs its dependencies.

## 3. Start the development server

In the VS Code terminal, run:

```powershell
npm start
```

Expo displays a QR code and interactive commands in the terminal:

- Press `w` to open the app in a web browser.
- Press `a` to open it in an Android emulator (Android Studio must be running).
- Press `i` to open it in the iOS simulator (macOS and Xcode required).
- Scan the QR code with **Expo Go** to open it on a physical phone.

The computer and phone normally need to be on the same Wi-Fi network. If the
phone cannot connect, start Expo using a tunnel:

```powershell
npx expo start --tunnel
```

## 4. Make the first screen

Open the main screen file created by the template. Depending on the selected
template, it is usually `app/(tabs)/index.tsx` or `app/index.tsx`.

Replace its contents with:

```tsx
import { Pressable, StyleSheet, Text, View } from 'react-native';
import { useState } from 'react';

export default function HomeScreen() {
  const [count, setCount] = useState(0);

  return (
    <View style={styles.container}>
      <Text style={styles.title}>My first React Native app</Text>
      <Text>You pressed the button {count} times.</Text>
      <Pressable style={styles.button} onPress={() => setCount(count + 1)}>
        <Text style={styles.buttonText}>Press me</Text>
      </Pressable>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
    gap: 16,
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
  },
  button: {
    borderRadius: 8,
    backgroundColor: '#2563eb',
    paddingHorizontal: 20,
    paddingVertical: 12,
  },
  buttonText: {
    color: '#ffffff',
    fontWeight: 'bold',
  },
});
```

Save the file. Expo's Fast Refresh should update the running application
automatically. If it does not, press `r` in the Expo terminal or reload the
app in Expo Go.

## 5. Test the application

Verify that:

1. The title and button are visible.
2. Pressing **Press me** increases the displayed counter.
3. The same screen works in the browser, emulator, or Expo Go.

To stop the development server, focus the terminal and press `Ctrl+C`.

## 6. Useful VS Code setup

Open the Extensions view (`Ctrl+Shift+X`) and install:

- **ESLint**, if the project includes ESLint configuration.
- **Prettier - Code formatter**.
- **React Native Tools** for debugging and React Native commands.

The project can be run again later with:

```powershell
cd MyFirstApp
npm start
```

Commit the generated project to Git when it is in a working state:

```powershell
git init
git add .
git commit -m "Create first React Native app"
```

For production builds and app-store distribution, use an Expo development
build and **EAS Build** rather than Expo Go.
