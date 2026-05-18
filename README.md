# Hastakala Shop

Hastakala Shop is a native Android application for managing a small artisan marketplace. It is built with Kotlin and Jetpack Compose and provides product management, billing, order history, sales summaries, and a simple assistant-style chat experience for shop insights.

The app is designed around handmade craft businesses such as pottery, textiles, paintings, jewelry, and other artisan products. It works as a lightweight shop dashboard where products can be added, edited, billed, tracked, and reviewed from a mobile-first interface.

## Table of Contents

- [Project Overview](#project-overview)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Screens and Modules](#screens-and-modules)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Setup Instructions](#setup-instructions)
- [Build and Run](#build-and-run)
- [Testing](#testing)
- [Data Storage](#data-storage)
- [Important Files](#important-files)
- [Customization Guide](#customization-guide)
- [Known Notes](#known-notes)
- [Future Enhancements](#future-enhancements)

## Project Overview

Hastakala Shop helps artisans or shop administrators handle day-to-day store tasks from one Android app. The app includes a dashboard for business metrics, a product catalog, billing workflow, order history, and a basic AI-style helper named Kala AI.

The application currently uses local device storage only. Products and orders are stored in `SharedPreferences`, so the app can preserve data between launches without requiring a backend server or internet connection.

## Key Features

- Splash screen with branded marketplace presentation.
- Bottom navigation with five main tabs:
  - Home
  - Products
  - Billing
  - Khata / order history
  - AI Chat
- Dashboard summary for:
  - Total sales
  - Total orders
  - Customer count
  - Weekly sales chart
  - Monthly revenue chart
  - Inventory and ratings cards
- Product catalog management:
  - Seed products on first launch
  - Add new products
  - Edit existing products
  - Delete products
  - Search products
  - Filter products by category
  - Low-stock indicators
- Billing workflow:
  - Select product quantities
  - Enter customer name
  - Calculate subtotal
  - Add 5 percent GST
  - Generate paid or unpaid orders
  - Automatically reduce product stock after billing
- Order history:
  - View generated orders
  - See customer name, items, totals, status, and timestamp
  - Highlight unpaid orders through the bottom navigation badge
- Kala AI chat:
  - Answers simple business questions from local order and product data
  - Supports weekly sales, best seller, and restock alert prompts
- Local persistence:
  - Products, orders, IDs, and order lines are saved locally using JSON in `SharedPreferences`.

## Tech Stack

| Area | Technology |
| --- | --- |
| Language | Kotlin |
| UI | Jetpack Compose |
| Design System | Material 3 |
| Android Gradle Plugin | 8.7.3 |
| Kotlin Plugin | 2.0.21 |
| Gradle Wrapper | 9.0.0 |
| Compile SDK | 35 |
| Target SDK | 35 |
| Minimum SDK | 24 |
| Java Version | 17 |
| Local Storage | Android `SharedPreferences` with JSON |
| Tests | JUnit, AndroidX Test, Espresso, Compose UI Test dependencies |

## Screens and Modules

### Home Dashboard

The home screen gives a quick overview of shop performance. It displays total sales, order count, customer count, weekly sales bars, monthly revenue line chart, and small administrative cards for inventory and ratings.

Main functions:

- `HomeDashboard`
- `DashboardHero`
- `SummaryCard`
- `WeeklyBarChart`
- `MonthlyLineChart`

### Products

The products screen works as the marketplace inventory manager. It supports searching, filtering, adding, editing, and deleting products. Each product has a name, category, price, stock count, description, and generated category color.

Main functions:

- `ProductsScreen`
- `MarketplaceProductCard`
- `ProductEditorDialog`
- `AddProductDialog`
- `ProductArtwork`

### Billing

The billing screen lets the user select product quantities, enter a customer name, and generate an order. It calculates subtotal, GST, and total amount. After billing, product stock is reduced.

Main functions:

- `BillingScreen`
- `ProductBillingRow`
- `BillSummaryCard`
- `SummaryLine`

### Khata / Order History

The history screen lists generated orders. It separates paid and unpaid order information visually and keeps the shop owner aware of pending payments.

Main functions:

- `OrderHistoryScreen`
- `OrderCard`
- `EmptyOrders`

### Kala AI

Kala AI is a rule-based local assistant. It does not call an external AI service. It reads current app data and responds to supported queries such as weekly sales, best seller, and stock alerts.

Main functions:

- `KalaAiScreen`
- `ChatBubble`
- `CraftStore.answerFor`

## Project Structure

```text
hastakalashop/
├── app/
│   ├── build.gradle.kts
│   ├── proguard-rules.pro
│   └── src/
│       └── main/
│           ├── AndroidManifest.xml
│           ├── java/
│           │   └── com/
│           │       └── hastakalashop/
│           │           └── app/
│           │               └── MainActivity.kt
│           └── res/
│               ├── drawable/
│               ├── mipmap-anydpi-v26/
│               ├── values/
│               └── xml/
├── gradle/
│   └── wrapper/
│       ├── gradle-wrapper.jar
│       └── gradle-wrapper.properties
├── Internship_Report_Output/
├── template_assets/
├── build.gradle.kts
├── settings.gradle.kts
├── gradle.properties
├── gradlew
├── gradlew.bat
├── create_template_report.js
└── README.md
```

## Requirements

Before running this project, install:

- Android Studio
- JDK 17
- Android SDK 35
- Android emulator or physical Android device
- Gradle is optional because the project includes the Gradle Wrapper

Recommended Android Studio setup:

- Use a recent stable Android Studio version.
- Install Android SDK Platform 35.
- Install Android SDK Build Tools compatible with Android Gradle Plugin 8.7.3.
- Enable Kotlin and Jetpack Compose support.

## Setup Instructions

1. Clone or open the project folder.

   ```bash
   cd hastakalashop
   ```

2. Open the folder in Android Studio.

3. Let Android Studio sync Gradle.

4. Confirm that `local.properties` points to your Android SDK location.

   Example:

   ```properties
   sdk.dir=C\:\\Users\\YourName\\AppData\\Local\\Android\\Sdk
   ```

5. Select an emulator or connect a physical Android device.

6. Run the `app` configuration.

## Build and Run

### Windows

Build a debug APK:

```powershell
.\gradlew.bat assembleDebug
```

Install on a connected device:

```powershell
.\gradlew.bat installDebug
```

Build a release APK:

```powershell
.\gradlew.bat assembleRelease
```

### macOS / Linux

Build a debug APK:

```bash
./gradlew assembleDebug
```

Install on a connected device:

```bash
./gradlew installDebug
```

Build a release APK:

```bash
./gradlew assembleRelease
```

## Testing

Run local unit tests:

```powershell
.\gradlew.bat test
```

Run Android instrumented tests:

```powershell
.\gradlew.bat connectedAndroidTest
```

Run a full verification build:

```powershell
.\gradlew.bat build
```

The project already includes dependencies for JUnit, AndroidX Test, Espresso, and Compose UI testing. Test source files are not currently present, so these dependencies are ready for future test coverage.

## Data Storage

The app stores data locally through the `CraftStore` class.

Storage details:

- Preference file name: `hasta_kala_shop_v2`
- Product data key: `products`
- Order data key: `orders`
- Product ID counter key: `nextProductId`
- Order ID counter key: `nextOrderId`

Stored product fields:

- `id`
- `name`
- `category`
- `price`
- `stock`
- `description`
- `color`

Stored order fields:

- `id`
- `customerName`
- `items`
- `subtotal`
- `gst`
- `total`
- `paid`
- `timestamp`

Because the data is local, uninstalling the app or clearing app storage will remove saved products and orders.

## Important Files

| File | Purpose |
| --- | --- |
| `app/src/main/java/com/hastakalashop/app/MainActivity.kt` | Main application code, Compose UI, models, local store, charts, billing, and chat logic |
| `app/build.gradle.kts` | Android app module configuration and dependencies |
| `build.gradle.kts` | Root Gradle plugin configuration |
| `settings.gradle.kts` | Project name, repositories, and module includes |
| `app/src/main/AndroidManifest.xml` | Android app declaration and launcher activity |
| `app/src/main/res/values/strings.xml` | App name resource |
| `app/src/main/res/values/themes.xml` | Android system theme settings |
| `gradle/wrapper/gradle-wrapper.properties` | Gradle Wrapper distribution configuration |
| `create_template_report.js` | Script for generating the internship report template output |
| `Internship_Report_Output/` | Generated internship report files and notes |
| `template_assets/` | Assets used by the report-generation script |

## Customization Guide

### Change App Name

Update:

```xml
app/src/main/res/values/strings.xml
```

```xml
<string name="app_name">Hastakala Shop</string>
```

### Change Package Name

Update these places:

- `namespace` in `app/build.gradle.kts`
- `applicationId` in `app/build.gradle.kts`
- Kotlin package declaration in `MainActivity.kt`
- Folder path under `app/src/main/java/`

### Change Theme Colors

Most Compose colors are defined at the top of `MainActivity.kt`:

```kotlin
private val Terracotta = Color(0xFFC1440E)
private val Cream = Color(0xFFFFF8F0)
private val DeepBrown = Color(0xFF3E1F00)
private val Gold = Color(0xFFD4A017)
```

The Android system status and navigation bar colors are defined in:

```text
app/src/main/res/values/themes.xml
```

### Add Default Products

Edit the `seedProducts` function inside `CraftStore`:

```kotlin
private fun seedProducts() {
    listOf(
        ProductDraft("Terracotta Clay Pot", "Pottery", 650.0, 12, "Hand-shaped clay pot with natural finish"),
        ProductDraft("Banana Fiber Tote", "Textiles", 850.0, 9, "Eco-friendly handwoven utility bag")
    ).forEach { addProduct(it) }
}
```

### Change GST Rate

The GST calculation is currently inside `generateBill`:

```kotlin
val gst = subtotal * 0.05
```

Change `0.05` to the required tax rate.

## Known Notes

- The app is currently local-first and does not use a backend database.
- Kala AI is rule-based and does not connect to an external AI API.
- The main app code is currently kept in a single Kotlin file.
- The repository includes report-generation files related to an internship report. These are separate from the Android app runtime.
- Generated build folders such as `build/`, `.gradle/`, and `app/build/` should normally not be committed to version control.

## Future Enhancements

Possible improvements:

- Move models, UI screens, and storage logic into separate Kotlin files.
- Add ViewModel-based state management.
- Replace `SharedPreferences` with Room Database or DataStore.
- Add invoice export as PDF.
- Add product image upload.
- Add customer management.
- Add payment status editing after order creation.
- Add real authentication for shop owners.
- Add cloud sync with Firebase or a custom backend.
- Add real AI integration for product suggestions and analytics.
- Add unit tests for `CraftStore`.
- Add Compose UI tests for product, billing, and history flows.

## License




## Screenshots
<img width="1856" height="1017" alt="Screenshot 2026-05-06 175202" src="https://github.com/user-attachments/assets/3e494acb-4162-4b94-a0e0-ce3b8c3afbf7" />
<img width="720" height="1600" alt="WhatsApp Image 2026-05-08 at 9 50 38 PM (2)" src="https://github.com/user-attachments/assets/92090a73-88f7-4c52-8701-5571c1417111" />
<img width="720" height="1600" alt="WhatsApp Image 2026-05-08 at 9 50 38 PM (6)" src="https://github.com/user-attachments/assets/e6c520d0-c736-442c-82f5-04972d99597f" />
<img width="720" height="1600" alt="WhatsApp Image 2026-05-08 at 9 50 38 PM (3)" src="https://github.com/user-attachments/assets/1f3255c6-b490-45b0-8baa-a7276d2a0b3e" />

<img width="720" height="1600" alt="WhatsApp Image 2026-05-08 at 9 50 38 PM (5)" src="https://github.com/user-attachments/assets/79cc2207-2962-4411-97d1-4ed25bf2a5d3" />

<img width="720" height="1600" alt="WhatsApp Image 2026-05-08 at 9 50 38 PM (7)" src="https://github.com/user-attachments/assets/d8685ec6-bc65-4aa1-9899-b1b2b6ddfeb2" />


## Installation
1. Clone repository
2. Open in Android Studio
3. Sync Gradle
4. Run app

## Developed By
DEIVA M
