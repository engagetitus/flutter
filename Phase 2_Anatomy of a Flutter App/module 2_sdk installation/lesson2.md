# Lesson 2: Setting Up Flutter SDK on macOS

- **Overview**: Steps to install Flutter SDK on macOS.
- **Key Concepts**:
  - Downloading Flutter SDK for macOS 🍎
  - Setting Up Environment Variables ⚙️
  - Verifying Installation ✅

## Downloading Flutter SDK for macOS 🍎

1. **Download Flutter SDK**: Go to the [Flutter website](https://flutter.dev) and download the latest version of the Flutter SDK for macOS.
2. **Extract the ZIP file**: Extract the downloaded file to an appropriate location on your system.

## Setting Up Environment Variables ⚙️

1. **Open your terminal**.
2. **Add Flutter to PATH**:

  ```bash
  export PATH="$PATH:`pwd`/flutter/bin"
```

Verifying Installation ✅
Run the following command:

```bash

flutter doctor
```

Ensure all checks are green.
