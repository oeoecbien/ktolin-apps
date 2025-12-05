# TipTime

A tip calculator application built with Jetpack Compose. This app demonstrates user input handling, real-time calculations, and advanced state management in modern Android development.

## Overview

TipTime is an Android application that calculates tip amounts based on bill totals and customizable tip percentages. It features real-time calculation updates, currency formatting, and an optional round-up feature.

## Features

- **Bill Amount Input**: Enter the total bill amount with numeric keyboard
- **Customizable Tip Percentage**: Set any tip percentage (e.g., 15%, 18%, 20%)
- **Round-Up Option**: Toggle to round up the tip to the nearest dollar
- **Real-Time Calculation**: Tip amount updates automatically as you type
- **Currency Formatting**: Displays tip amount in local currency format
- **Material Design 3**: Modern UI with TextField, Switch, and Icon components
- **Edge-to-Edge**: Modern edge-to-edge display support
- **Accessibility**: Proper content descriptions and keyboard navigation

## Technologies

- **Language**: Kotlin
- **UI Framework**: Jetpack Compose
- **Design System**: Material Design 3
- **Minimum SDK**: 24
- **Target SDK**: 35
- **Compile SDK**: 35
- **Java Version**: 17

## Key Concepts Demonstrated

This project teaches the following Jetpack Compose concepts:

1. **User Input Handling**
   - `TextField` composable for text input
   - Keyboard options (numeric input, IME actions)
   - Input validation and parsing
   - Leading icons in text fields

2. **State Management**
   - Multiple state variables for different inputs
   - Real-time state updates
   - Derived state calculations
   - Boolean state for toggle switches

3. **Material Design 3 Components**
   - `TextField` with custom styling
   - `Switch` component for boolean options
   - `Icon` composable for visual elements
   - Material 3 typography

4. **Layout and Composition**
   - `Column` for vertical layout
   - `Row` for horizontal layout
   - `Spacer` for spacing
   - `verticalScroll` for scrollable content
   - Safe area padding

5. **Data Formatting**
   - Currency formatting with `NumberFormat`
   - Number parsing with `toDoubleOrNull()`
   - Mathematical calculations

## Project Structure

```
TipTime/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/tiptime/
│   │   │   │   ├── MainActivity.kt          # Main activity and composables
│   │   │   │   └── ui/theme/                # Theme configuration
│   │   │   ├── res/
│   │   │   │   ├── drawable/                # Icons (money, percent)
│   │   │   │   ├── values/
│   │   │   │   │   ├── strings.xml           # String resources
│   │   │   │   │   └── colors.xml            # Color definitions
│   │   │   └── AndroidManifest.xml
│   │   ├── test/                             # Unit tests
│   │   └── androidTest/                      # Instrumented tests
│   └── build.gradle.kts
├── build.gradle.kts
├── settings.gradle.kts
└── LICENSE
```

## Getting Started

### Prerequisites

- Android Studio (latest version)
- JDK 17 or higher
- Android SDK with API level 24+
- Experience with Kotlin syntax
- Understanding of Compose basics (from previous projects)

### Installation

1. Open the project in Android Studio
2. Sync Gradle dependencies
3. Run the app on an emulator or physical device

### Building

```bash
./gradlew assembleDebug
```

### Running Tests

```bash
./gradlew test              # Unit tests
./gradlew connectedAndroidTest  # Instrumented tests
```

## Code Highlights

### State Management

The app manages multiple input states:

```kotlin
@Composable
fun TipTimeLayout() {
    var amountInput by remember { mutableStateOf("") }
    var tipInput by remember { mutableStateOf("") }
    var roundUp by remember { mutableStateOf(false) }
    
    val amount = amountInput.toDoubleOrNull() ?: 0.0
    val tipPercent = tipInput.toDoubleOrNull() ?: 0.0
    val tip = calculateTip(amount, tipPercent, roundUp)
}
```

### TextField with Icon

Custom text field with leading icon:

```kotlin
@Composable
fun EditNumberField(
    @StringRes label: Int,
    @DrawableRes leadingIcon: Int,
    keyboardOptions: KeyboardOptions,
    value: String,
    onValueChanged: (String) -> Unit,
    modifier: Modifier = Modifier
) {
    TextField(
        value = value,
        singleLine = true,
        leadingIcon = { Icon(painter = painterResource(id = leadingIcon), null) },
        modifier = modifier,
        onValueChange = onValueChanged,
        label = { Text(stringResource(label)) },
        keyboardOptions = keyboardOptions
    )
}
```

### Tip Calculation

Currency-formatted tip calculation:

```kotlin
private fun calculateTip(amount: Double, tipPercent: Double = 15.0, roundUp: Boolean): String {
    var tip = tipPercent / 100 * amount
    if (roundUp) {
        tip = kotlin.math.ceil(tip)
    }
    return NumberFormat.getCurrencyInstance().format(tip)
}
```

## Dependencies

- `androidx.activity:activity-compose:1.9.3`
- `androidx.compose.material3:material3`
- `androidx.compose.ui:ui`
- `androidx.compose.ui:ui-tooling`
- `androidx.compose.ui:ui-tooling-preview`
- `androidx.core:core-ktx:1.15.0`
- `androidx.lifecycle:lifecycle-runtime-ktx:2.8.7`
- `junit:junit:4.13.2`
- Compose BOM: `2024.12.01`

## UI Components

### Input Fields

1. **Bill Amount Field**
   - Leading icon: Money icon
   - Keyboard type: Number
   - IME action: Next

2. **Tip Percentage Field**
   - Leading icon: Percent icon
   - Keyboard type: Number
   - IME action: Done

### Controls

- **Round Up Switch**: Toggle to round tip to nearest dollar
- **Calculate Button**: Implicit calculation (updates in real-time)

### Output

- **Tip Amount Display**: Large, formatted currency display

## Learning Outcomes

After completing or studying this project, you should understand:

- How to handle user input with TextField
- How to configure keyboard options and IME actions
- How to parse and validate numeric input
- How to perform real-time calculations based on state
- How to format currency values
- How to use Switch components for boolean options
- How to create custom composables with parameters
- How to implement scrollable layouts
- How to handle safe area padding for edge-to-edge displays

## Usage Example

1. Enter bill amount: `100.00`
2. Enter tip percentage: `18`
3. Toggle "Round up tip?" if desired
4. View calculated tip amount (e.g., "$18.00" or "$19.00" if rounded)

## Future Enhancements

Potential improvements:
- Split bill functionality
- Tip percentage quick-select buttons (15%, 18%, 20%, 25%)
- Bill splitting between multiple people
- Tip history/log
- Different currency support
- Dark mode optimizations
- Animation effects
- Save favorite tip percentages

## License

This project is licensed under the Apache License 2.0. See the LICENSE file for details.

## Related Resources

This project is part of the [Android Basics with Compose](https://developer.android.com/courses/android-basics-compose/course) course. It builds upon concepts learned in:
- DiceRoller (basic state management)
- HappyBirthday (layout composition)
- Lemonade (multi-step state management)
