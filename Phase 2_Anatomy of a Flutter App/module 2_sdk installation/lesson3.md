
# Lesson 3: Setting Up Flutter SDK on Linux

- **Overview**: Steps to install Flutter SDK on Linux.
- **Key Concepts**:
  - Downloading Flutter SDK for Linux 🐧
  - Setting Up Environment Variables ⚙️
  - Verifying Installation ✅

# Downloading Flutter SDK for Linux 🐧

1. **Download Flutter SDK**: Go to the [Flutter website](https://flutter.dev) and download the latest version of the Flutter SDK for Linux.
2. **Extract the TAR file**: Extract the downloaded file to an appropriate location on your system.

  ```bash
  tar xf flutter_linux_v1.22.6-stable.tar.xz
  ```

## Setting Up Environment Variables ⚙️

Open your terminal.
Add Flutter to PATH:

```bash

export PATH="$PATH:`pwd`/flutter/bin"
```

Verifying Installation ✅
Run the following command:

```bash
flutter doctor
```

Ensure all checks are green.
