# PORTAL RECETTA B2B FLUTTER

## Table of Contents

1. [Overview](#overview)
2. [Requirements](#requirements)
3. [Getting Started](#getting-started)
4. [Running the Flutter Web Application Locally](#running-the-flutter-web-application-locally)
   - [Build the Application for Web](#1-build-the-application-for-web)
   - [Install `http-server`](#2-install-http-server-if-not-already-installed)
   - [Serve the Build Directory Using `http-server`](#3-serve-the-build-directory-using-http-server)
   - [Access the Application in Your Browser](#4-access-the-application-in-your-browser)
5. [Splash Screen Setup](#splash-screen-setup)
6. [Testing](#testing)
7. [Test Coverage](#test-coverage)
8. [Debugging Widgets](#debugging-widgets)
9. [Versioning Guidelines](#versioning-guidelines)
10. [Changelog for Version 1.3.0 - 2024-10-28](#changelog-for-version-130---2024-10-28)
11. [Versioning Workflow](#versioning-workflow)
12. [Contentful Backup and Migration Guide](#contentful-backup-and-migration-guide)
13. [Credits](#credits)

---

## Overview

Welcome to the **FLUTTER B2B RECIPE PORTAL** project! This Flutter application serves as a B2B eCommerce platform for recipes.

## Requirements

- **Flutter Version:** 3.16.5
- **Tools:** Dart SDK 3.2.3 • DevTools 2.28.4

## Getting Started

Follow these steps to run the project locally:

1. **Clone the Repository:**
```sh
git clone https://GrupoNutresa@dev.azure.com/GrupoNutresa/La%20Recetta/_git/4494-portal-recetta-b2b-flutter
cd 4494-portal-recetta-b2b-flutter
```

2. **Install Dependencies:**
```bash
dart pub get
```

3. **Set up Environment Variables:**
   - Use the `.env.template` file to create a `.env` file.
   - After configuring the `.env` file, run:
```bash
dart run build_runner build --delete-conflicting-outputs
```

4. **Internationalization:**
   - Generate files for internationalization:
```bash
dart run slang
```
   - Check the folder `lib/core/constants` for the generated files.

   Example:
```dart
import 'package:portal_recetta_b2b_flutter/core/constants/generated/i18n/translations.g.dart';
final Translations t = Translations.of(context);
Text(t.title)
```

5. **Run the Application:**
```bash
flutter run
```

6. **Run with Specific Ports for Authentication Resources:**
   - Run the following for optimal configuration:
```bash
flutter run -d <device> -t lib/main.dart --web-port <port_number>
```
   - Enabled Ports: `63390`, `63858`, `62969`, `64589`

---

## Running the Flutter Web Application Locally

This guide provides steps to build and serve the Flutter web application locally with `http-server`.

### 1. **Build the Application for Web**

```bash
flutter build web --web-renderer html --no-source-maps --release
```

### 2. **Install `http-server` (If Not Already Installed)**

Install `http-server` globally with `npm`:
```bash
npm install -g http-server
```

### 3. **Serve the Build Directory Using `http-server`**

Change to `build/web` and start `http-server`:
```bash
cd build/web
http-server -p 63390 -a localhost
```

### 4. **Access the Application in Your Browser**

Open:
```
http://localhost:63390
```

---

## Splash Screen Setup

Follow these steps to set up a splash screen using `flutter_native_splash`:

1. **Install `flutter_native_splash`:**
   ```yaml
   dependencies:
     flutter_native_splash: ^2.0.0
   ```

2. **Create Configuration File:**
   Create `flutter_native_splash.yaml` in the root directory:
   ```yaml
   flutter_native_splash:
     color: "#FFFFFF"
     image: assets/gifs/loading.gif
     android: true
     ios: true
     web: true
     web_image_mode: center
   ```

3. **Generate Splash Screen:**
```bash
dart run flutter_native_splash:create --path=flutter_native_splash.yaml
```

---

## Testing

Run widget tests:
```bash
flutter test
```

## Test Coverage

To assess test coverage:

1. **Install LCOV:**
```bash
brew install lcov
```

2. **Generate Coverage Data:**
```bash
flutter test --coverage
```

3. **Generate HTML Reports:**
```bash
genhtml coverage/lcov.info -o coverage/html
```

4. **View Coverage Reports:**
```bash
open coverage/html/index.html
```

---

## Debugging Widgets

To effectively debug Flutter widgets:

1. **Run in Debug Mode:**
```bash
flutter run
```

2. **Inspect Widgets:**
```bash
flutter pub global run devtools
```

3. **Hot Reload:**
   Press `R` in the terminal to reload changes.

4. **Print Statements and Breakpoints:**
   Use `print` statements and breakpoints for debugging.

---

## Versioning Guidelines

This application uses **Semantic Versioning** (MAJOR.MINOR.PATCH):
- **MAJOR**: Breaking changes
- **MINOR**: New, backward-compatible features
- **PATCH**: Backward-compatible bug fixes

---

## Changelog example for Version X.X.X - XXXX-XX-XX

### Improvements
- Fixed multiple bugs for enhanced stability.

### New Features
- New feature
- Refactor feature and major changed

### Interface & UX Updates
- Resolved UI/UX bugs for a smoother experience.

---

## Versioning Workflow

1. **Branching Strategy:**
   - **Main**: Latest stable release.
   - **Development**: Ongoing feature integration.

2. **Releases:**
   - **Pre-releases** (e.g., `X.X.X-beta`) for internal testing.
   - **Hotfixes** (e.g., `X.X.X`) for urgent production bugs.

3. **Tagging and Documentation:**
   - Each release is tagged and documented in the changelog.

## Contentful Backup and Migration Guide

This guide explains how to:
1. Generate a backup of a Contentful environment.
2. Migrate data from `dev` to `qa`.
3. Migrate data from `qa` to `master`.
4. Handle model deletion during migration.

---

## Prerequisites

1. Install the Contentful CLI:
   ```bash
   npm install -g contentful-cli
   ```
2. Authenticate with your Contentful account:
   ```bash
   contentful login
   ```
3. Replace placeholders like `<SPACE_ID>` with your actual values.
4. Ensure you have appropriate permissions for the environments.

---

## Step 1: Generate a Backup of an Environment

To back up a specific environment:

```bash
contentful space export \
  --space-id <SPACE_ID> \
  --environment-id <ENVIRONMENT_ID> \
  --content-file backup-<ENVIRONMENT_ID>.json \
  --download-assets
```

### Example:
Export data from the `qa` environment:
```bash
contentful space export \
  --space-id oqtvq54l01dm \
  --environment-id qa \
  --content-file backup-qa.json \
  --download-assets
```

- **`--content-file`**: Specifies the name of the exported file.
- **`--download-assets`**: Ensures all associated assets are downloaded.

---

## Step 2: Migrate Data from `dev` to `qa`

### 1. Export Data from `dev`
```bash
contentful space export \
  --space-id <SPACE_ID> \
  --environment-id dev \
  --content-file dev-data.json \
  --download-assets
```

### 2. Import Data into `qa`
```bash
contentful space import \
  --space-id <SPACE_ID> \
  --environment-id qa \
  --content-file dev-data.json \
  --retry-limit 10 \
  --rate-limit 5
```

- **`--retry-limit`**: Specifies the maximum number of retries for rate limit errors.
- **`--rate-limit`**: Controls the number of requests per second (default: 5).

---

## Step 3: Migrate Data from `qa` to `master`

### 1. Export Data from `qa`
```bash
contentful space export \
  --space-id <SPACE_ID> \
  --environment-id qa \
  --content-file qa-data.json \
  --download-assets
```

### 2. Import Data into `master`
```bash
contentful space import \
  --space-id <SPACE_ID> \
  --environment-id master \
  --content-file qa-data.json \
  --retry-limit 10 \
  --rate-limit 5
```

---

## Step 4: Handle Model Deletion During Migration

When migrating data between environments, the `export` and `import` commands do not automatically delete content types (models) in the target environment. Follow these steps to ensure unwanted models are removed:

### 1. Identify Models to Delete
- Review the models in the target environment that should no longer exist.
- Compare them against the source environment to identify obsolete models.

### 2. Delete Models Manually
- Go to the Contentful web interface.
- Navigate to the *Content Types* section in the target environment.
- Delete the unwanted models manually.

### 3. Delete Models via CLI (Optional)
Use the following command to delete a model programmatically:
```bash
contentful space delete-content-type \
  --space-id <SPACE_ID> \
  --environment-id <ENVIRONMENT_ID> \
  --id <CONTENT_TYPE_ID>
```

### 4. Export and Import Data
After cleaning up the target environment, proceed with the `export` and `import` steps as outlined above.

---

## Additional Tips

1. **Verify Imported Data:** After importing, ensure all entries and assets are correctly migrated:
   ```bash
   contentful entry list --space-id <SPACE_ID> --environment-id <ENVIRONMENT_ID>
   contentful asset list --space-id <SPACE_ID> --environment-id <ENVIRONMENT_ID>
   ```

2. **Handle Large Datasets:** If you encounter rate limit issues:
   - Increase the `--retry-limit`.
   - Reduce the `--rate-limit`.

3. **Split Large Files:** If the exported JSON file is too large, consider splitting it into smaller parts using tools like `jq`.

4. **Monitor API Limits:** Contentful enforces [rate limits](https://www.contentful.com/developers/docs/references/content-management-api/#/reference/rate-limits). Adjust settings accordingly.

---

## Troubleshooting

### Rate Limit Errors:
If you see the error:
```
⚠ Rate limit error occurred. Waiting for <time> ms before retrying...
```
- Increase the retry limit using `--retry-limit`.
- Reduce the request rate using `--rate-limit`.

### API Errors:
Check the error logs and ensure the data being imported doesn’t conflict with existing entries or assets in the target environment.

---

This document should help streamline the process of backing up and migrating environments in Contentful. For further assistance, refer to the [Contentful CLI Documentation](https://www.contentful.com/developers/docs/tutorials/cli/).

---

## Credits

Developed and maintained by:  
**Santiago Arango Gutierrez**  
Email: santiago.arango@experimentality.co  

All rights reserved © Experimentality Labs

---