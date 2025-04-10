[![Pub Version](https://img.shields.io/pub/v/flex_color_picker?label=flex_color_picker&labelColor=333940&logo=dart)](https://pub.dev/packages/flex_color_picker) ![Test](https://github.com/rydmike/flex_color_picker/workflows/Test/badge.svg) [![codecov](https://codecov.io/gh/rydmike/flex_color_picker/graph/badge.svg?token=6GEGK5XEOP)](https://codecov.io/gh/rydmike/flex_color_picker) [![License](https://img.shields.io/badge/License-BSD%203--Clause-blue.svg)](https://opensource.org/licenses/BSD-3-Clause)

# FlexColorPicker

FlexColorPicker is a customizable color picker for Flutter. The `ColorPicker` can show six different types of color 
pickers, three of which are used for the standard Flutter Material Design 2 colors and their shades.
The size and style used for the pick items can be customized.

The picker can optionally also generate Material Design 3 color system
accurate tonal palettes, using any selected color in the picker, as key color to generate
the tonal palette. A color from the generated tonal palette can then be picked as well.
See the [Material 3 Design Guide website](https://m3.material.io/styles/color/the-color-system/key-colors-tones)
for more information about the Material 3 color system and tonal palettes.


The picker is Windows, Mac, Linux and Web desktop compatible. It has desktop focus handling plus optional menus 
and buttons for handling COPY-PASTE of colors from and to the picker, including desktop platform-aware COPY-PASTE keyboard shortcuts.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/ColorPickerAllSize50-upper.png?raw=true" alt="ColorPicker variations upper"/>

## Contents
- [FlexColorPicker](#flexcolorpicker)
    - [Contents](#contents)
    - [Color Picker Types](#color-picker-types)  
    - [Getting Started](#getting-started)
        - [Default Example Application](#default-example-application)
        - [Live Web Demo](#live-web-demo)
- [Tutorial](#tutorial)
    - [Color Indicator](#color-indicator)
    - [Screen ColorPicker](#screen-colorpicker)  
    - [Dialog ColorPicker Method](#dialog-colorpicker-method)
    - [Dialog ColorPicker Function](#dialog-colorpicker-function)
- [API Guide](#api-guide)
    - [Elements of the Picker](#elements-of-the-picker)
        - [Enabled Color Pickers](#enabled-color-pickers)
        - [Enable Shades Selection](#enable-shades-selection)
        - [Tonal Palette](#tonal-palette)
        - [Custom Color Swatches](#custom-color-swatches)
        - [Customized labels](#customized-labels)
        - [Enable Opacity](#enable-opacity)
        - [Show Color Names](#show-color-names)
            - [Translate Material Color Names](#translate-material-color-names)
        - [Show Color Code](#show-color-code)
        - [Show Recent Colors](#show-recent-colors)
        - [Title and Heading Widgets](#title-and-heading-widgets)
    - [Picker Design](#picker-design)
        - [Color Picker Items](#color-picker-items)
        - [Wheel Diameter, Width and Border](#wheel-diameter-width-and-border)
        - [Opacity Slider Height, Width and Thumb Radius](#opacity-slider-height-width-and-thumb-radius)
    - [Picker Layout](#picker-layout)
        - [Tooltips](#tooltips)
    - [Dialog Action Buttons](#dialog-action-buttons)
    - [Copy-Paste Actions and Behavior](#copy-paste-actions-and-behavior)
        - [Code Field Copy Button](#code-field-copy-button)
        - [Keyboard Shortcuts](#keyboard-shortcuts)
        - [Toolbar Buttons](#toolbar-buttons)
        - [Context Menu](#context-menu)
        - [Color Code Formats and Paste Parsing](#color-code-formats-and-paste-parsing)
    - [onChange Callbacks](#onchange-callbacks)
    - [Dialogs](#dialogs)
        - [ColorPicker showPickerDialog Method](#colorpicker-showpickerdialog-method)
        - [Function showColorPickerDialog](#function-showcolorpickerdialog)
- [Desktop and Web Ready](#desktop-and-web-ready)
- [Additional Resources](#additional-resources)      

---

## Color Picker Types

The different types of available color pickers are:

1. Material primary colors and its shades. `ColorPickerType.primary`
2. Material accent colors and its shades. `ColorPickerType.accent`
3. Both primary and accent colors and their shades, in the same color picker. `ColorPickerType.both`
4. Black and white colors, including very near black and white shades. `ColorPickerType.bw`
5. Custom color swatches and their shades, that you define and name. `ColorPickerType.custom`
6. HSV color-wheel picker, that allows you to select or enter any color. `ColorPickerType.wheel`

When you show more than one color picker, a segmented sliding control allows you to select which one to use. You can 
configure the `ColorPicker` to include any of the above color pickers. Showing pickers 1 and 2, together with picker 3 
is not very useful, they are available as optional ways of showing and selecting the standard Material primary and 
accent colors.

Give the `ColorPicker` a heading and a subheading for the color shades, typically Text widgets with an appropriate style. 
Decide if the Material shades can be selected or not and if the selected color name and RGB code are visible in the 
picker. If the color HEX RGB code is visible, the picker can also include a button that allows you to copy the selected 
color code to the clipboard directly from the field. On the wheel picker you can enter a HEX RGB color code, and
the wheel picker will move to select the entered color, while also creating a color swatch for it.

The shape, size and spacing of the color picker items can be modified. There is a built-in dialog that can be used to
show and use the `ColorPicker` in a dialog. You can also make your own dialog and use the `ColorPicker`
widget in your own custom dialog or some other type of overlay.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/ColorPickerAllSize50-lower.png?raw=true" alt="ColorPicker variations lower"/>

## Getting Started

Add the `flex_color_picker` package to `pubspec.yaml`:

`dart pub add flex_color_picker` or `flutter pub add flex_color_picker`

Import the package to use it:

```dart
import 'package:flex_color_picker/flex_color_picker.dart';
```

### Default Example Application

To try the default example of the color picker on a device or simulator, clone the **FlexColorPicker** [GitHub 
repository](https://github.com/rydmike/flex_color_picker) and run the example:

```bash
cd example/
flutter run --release
```

The result is a default color picker in a Card on the screen, with only the Material primary and accent color 
pickers enabled. It also has two other color pickers that open up in dialogs with different styles and different 
enabled picker types. The [tutorial](#tutorial) goes through and explains the example application in detail.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/ColorPickerSimpleDemo.png?raw=true" alt="ColorPicker Basic"/>

### Live Web Demo

You can also try a live Web demo of the [**FlexColorPicker here**](https://rydmike.com/flexcolorpicker). With the Web
demo, you can modify most of the color picker's API values and use it as a tool to find a style that fits your 
application.

The source code for the Web demo, which is a bit more elaborate example than examples normally are, is also bundled with 
the package source code in the "example/lib/demo" folder.

The Web demo has a responsive view that expands into maximum four separately scrollable columns. The columns contain
many controls that you can use to adjust the color picker's settings. On a 1080p desktop screen,
you can see most of the settings at the same time as the color picker. With this, you can test the settings and see their
impact on the picker as you adjust them. 

The Web demo also has tooltips for each setting control. The tooltips show the name of the API it modifies and its 
current value. With this feature, you can use the web demo as a tool to configure the color picker to a desired style, 
and find the APIs and values that you used. 

The same toggle used to turn OFF the tooltips in the color picker also turns OFF
the API tooltips in the demo, in case they get in the way. By default, the tooltips are ON to show the used API and 
its current value.

The **FlexColorPicker** web demo also persists the settings as you change them. The next time you use it, with the same 
device and browser, it will restore the configuration that you left it in last time you used it. You can reset the
settings to their start default values as well.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/web_color_picker_v2.gif?raw=true" alt="ColorPicker WEB demo"/>

# Tutorial

In this chapter, we use the default and bundled example application as an introduction to the **FlexColorPicker**. We will
create three different color pickers, with different configurations and use the `ColorPicker` three different ways.

This example uses a `StatefulWidget` as its main page, the `ColorPickerPage`, where we define three different `Color`
objects in its local state, and give them a start value in the `StatefulWidget`'s `initState()`.

We will use these colors to indicate the currently selected color for the three examples and as start color value 
for each color picker.

```dart
class _ColorPickerPageState extends State<ColorPickerPage> {
  // Color for the picker shown in Card on the screen.
  late Color screenPickerColor;
  // Color for the picker in a dialog using onChanged.
  late Color dialogPickerColor;
  // Color for picker using the color select dialog.
  late Color dialogSelectColor; 

@override
void initState() {
  super.initState();
  screenPickerColor = Colors.blue;  // Material blue.
  dialogPickerColor = Colors.red;   // Material red.
  dialogSelectColor = const Color(0xFFA239CA); // A purple color.
}
```
## Color Indicator

We can use the `ColorIndicator` Widget, that the `ColorPicker` also uses internally, to show and select a new color. 
Alternatively, you can make and use a custom for Widget for this purpose. In this tutorial we use the `ColorIndicator` in 
a `ListTile`, and use the `ColorIndicator` as its trailing property to show the selected color.

The **FlexColorPicker** package also includes `ColorTools`, a set of helper functions that among other things, 
can display names of the standard Material colors, shade index, and an optional Flutter 
style Hex color code. We use the `ColorTools.materialNameAndCode` in the `ListTile`'s `subtitle` property to 
describe the selected color by showing its Material color name and index, as well as its Flutter style HEX color value. 

We also use the `ColorTools.nameThatColor` function, that names any color based on the closest matching color from a
list consisting of **1566** color values and their English names.

We begin by adding this ListTile to a ListView in the Scaffold body.

```dart
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
      centerTitle: true,
      title: const Text('FlexColorPicker Demo'),
    ),
    body: ListView(
        padding: const EdgeInsets.fromLTRB(8, 0, 8, 0),
      children: <Widget>[
        // Show the selected color.
        ListTile(
          title: const Text('Select color below to change this color'),
          subtitle:
            Text('${ColorTools.materialNameAndCode(screenPickerColor)} '
                 'aka ${ColorTools.nameThatColor(screenPickerColor)}'),
          trailing: ColorIndicator(
            width: 44,
            height: 44,
            borderRadius: 22,
            color: screenPickerColor,
          ),
        ),
   ...
```

## Screen ColorPicker

Next we add the FlexColorPicker `ColorPicker` widget to the `ListView`. We give the `ColorPicker`'s `color` property 
the defined starting color, in this case `screenPickerColor`. We also give the picker a `heading` and `subHeading`, 
plus the required `onColorChanged` callback function. 

We use the color from the callback in a `setState()` to modify the `screenPickerColor` to the color returned by
the callback. The `onColorChanged` callback in the `ColorPicker` is called whenever you select a new color in 
the `ColorPicker` with the selected `Color` value. In this example we have also wrapped the color picker in a `Card`.

```dart
  // Show the color picker in sized box in a raised card.
  SizedBox(
    width: double.infinity,
    child: Padding(
      padding: const EdgeInsets.all(6),
      child: Card(
        elevation: 2,
        child: ColorPicker(
          // Use the screenPickerColor as start and active color.
          color: screenPickerColor,
          // Update the screenPickerColor using the callback.
          onColorChanged: (Color color) =>
            setState(() => screenPickerColor = color),
          width: 44,
          height: 44,
          borderRadius: 22,
          heading: Text(
            'Select color',
            style: Theme.of(context).textTheme.headlineSmall,
          ),
          subheading: Text(
            'Select color shade',
            style: Theme.of(context).textTheme.titleSmall,
          ),
        ),
      ),
    ),
  ),
```

This gives us round color pick items, and a round color indicator above the picker to show the selected color:

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/ColorPicker02.png?raw=true" alt="ColorPicker round with indicator" width="300"/>

## Dialog ColorPicker Method 

A common use case for a color picker is to show a color selection widget and allow users to select a new color in 
a dialog. The `ColorPicker` comes with a built-in dialog that can be used for this. Alternatively you can use 
the `ColorPicker` widget and include it in your own custom dialog.

For the first dialog example, we will show all the built-in picker types, except the combined 
primary and accent colors picker type, and the near black and white shades' picker. We will add some custom colors
for the **Custom** section of the `ColorPicker`.

First we define our custom colors and from our color definitions we create primary and accent color swatches by 
using `ColorTools.createPrimarySwatch`, and for some example colors with the `ColorTools.createAccentSwatch` 
to get accent color swatches. 

We add these color swatches as keys to a `ColorSwatch` **Map**, that we map to our own `String` name values 
for our custom color swatches. You don't have to use the `ColorTools` functions to create the color swatches from 
a color, you can as well define and use your own custom hand tuned `ColorSwatch` swatches created
with `MaterialColor` or `MaterialAccentColor`, as shown in the [custom color swatches](#custom-color-swatches) chapter.
The `ColorTools` functions are just convenient helpers that can be used to make Material like primary and accent color 
swatches from a single color value.

```dart
  // Define custom colors. The 'guide' color values are from
  // https://material.io/design/color/the-color-system.html#color-theme-creation
  static const Color guidePrimary = Color(0xFF6200EE);
  static const Color guidePrimaryVariant = Color(0xFF3700B3);
  static const Color guideSecondary = Color(0xFF03DAC6);
  static const Color guideSecondaryVariant = Color(0xFF018786);
  static const Color guideError = Color(0xFFB00020);
  static const Color guideErrorDark = Color(0xFFCF6679);
  static const Color blueBlues = Color(0xFF174378);

  // Make a custom ColorSwatch to name map from the above custom colors.
  final Map<ColorSwatch<Object>, String> colorsNameMap =
      <ColorSwatch<Object>, String>{
    ColorTools.createPrimarySwatch(guidePrimary): 'Guide Purple',
    ColorTools.createPrimarySwatch(guidePrimaryVariant): 'Guide Purple Variant',
    ColorTools.createAccentSwatch(guideSecondary): 'Guide Teal',
    ColorTools.createAccentSwatch(guideSecondaryVariant): 'Guide Teal Variant',
    ColorTools.createPrimarySwatch(guideError): 'Guide Error',
    ColorTools.createPrimarySwatch(guideErrorDark): 'Guide Error Dark',
    ColorTools.createPrimarySwatch(blueBlues): 'Blue blues',
  };
```

We will use another `ListTile` to display a `ColorIndicator`, that we style a bit differently in this example. We also 
use its `onSelect` callback to open a dialog with another `ColorPicker`. As the starting pre-selected color, 
we will use the `dialogPickerColor` we defined already at the beginning of the tutorial.

Before we open the dialog we store the current `dialogPickerColor`'s color value. This way we can restore this 
color value if the user cancels the dialog. We put this ListTile before the previous one, so first in our list view. 
This will just ensure that it does not get hidden by the dialog on smaller phones. For demonstration purposes, 
we want this color to be visible and not obscured by the dialog.

```dart
  // Pick color in a dialog.
  ListTile(
    title: const Text('Click this color to change it in a dialog'),
    subtitle: Text(
      '${ColorTools.materialNameAndCode(dialogPickerColor, '
      'colorSwatchNameMap: colorsNameMap)} '
      'aka ${ColorTools.nameThatColor(dialogPickerColor)}',
    ),
    trailing: ColorIndicator(
      width: 44,
      height: 44,
      borderRadius: 4,
      color: dialogPickerColor,
      onSelectFocus: false,
      onSelect: () async {
        // Store current color before we open the dialog.
        final Color colorBeforeDialog = dialogPickerColor;
        // Wait for the picker to close, if dialog was dismissed, 
        // then restore the color we had before it was opened.
        if (!(await colorPickerDialog())) {
          setState(() {
            dialogPickerColor = colorBeforeDialog;
          });
        }
      },
    ),
  ),
```

> [!NOTE]  
> The above `onSelectFocus` property is used to inform the `ColorIndicator` that we do not want it to keep focus
> when we select and click on it in desktop and Web applications. On those platforms it gets focus when we
> click on it to open the dialog from it. If it keeps focus while the dialog is open and after the dialog is closed, 
> the active focus overlay color will distort its actual color a bit. In that case, we cannot observe the selected 
> color until we unfocus it. We don't want that, this property addresses this issue, by automatically unfocusing 
> it after we clicked on it.

Next we create a method to show a `ColorPicker` with the built-in `colorPickerDialog` dialog method. 
The `colorPickerDialog` method is an asynchronous bool function, that returns `true` if the user closed the dialog 
picker with the **OK** or **Select** dialog button. If **Cancel/Close** was selected, or if the user dismissed the 
dialog by clicking outside it, then `false` is returned.

In this example, we first enable a few more color picker types. The `pickersEnabled` property takes a map 
with `ColorPickerType` enum keys to boolean values. The map defines which color 
pickers we want to enable and use in the `ColorPicker`. 

In the example below, we included Material **primary**, **accent** colors, and the **custom** colors we defined above,
plus the HSV **color wheel** that allows us to select any color. We did not include the picker that combines the 
primary and accent colors in the same picker, nor the near black and near white color picker.

Below the custom colors we defined in `colorsNameMap` are given to the color picker's 
property `customColorSwatchesAndNames`. If you leave `customColorSwatchesAndNames` without an entry and 
happen to have `ColorPickerType.custom: true` enabled, the custom picker will not be shown.

```dart
  Future<bool> colorPickerDialog() async {
    return ColorPicker(
      // Use the dialogPickerColor as start and active color.
      color: dialogPickerColor,
      // Update the dialogPickerColor using the callback.
      onColorChanged: (Color color) =>
          setState(() => dialogPickerColor = color),
      width: 40,
      height: 40,
      borderRadius: 4,
      spacing: 5,
      runSpacing: 5,
      wheelDiameter: 155,
      heading: Text(
        'Select color',
        style: Theme.of(context).textTheme.titleSmall,
      ),
      subheading: Text(
        'Select color shade',
        style: Theme.of(context).textTheme.titleSmall,
      ),
      wheelSubheading: Text(
        'Selected color and its shades',
        style: Theme.of(context).textTheme.titleSmall,
      ),
      showMaterialName: true,
      showColorName: true,
      showColorCode: true,
      copyPasteBehavior: const ColorPickerCopyPasteBehavior(
        longPressMenu: true,
      ),
      materialNameTextStyle: Theme.of(context).textTheme.bodySmall,
      colorNameTextStyle: Theme.of(context).textTheme.bodySmall,
      colorCodeTextStyle: Theme.of(context).textTheme.bodySmall,
      pickersEnabled: const <ColorPickerType, bool>{
        ColorPickerType.both: false,
        ColorPickerType.primary: true,
        ColorPickerType.accent: true,
        ColorPickerType.bw: false,
        ColorPickerType.custom: true,
        ColorPickerType.wheel: true,
      },
      customColorSwatchesAndNames: colorsNameMap,
    ).showPickerDialog(
      context,
      // New in version 3.0.0 custom transitions support.
      transitionBuilder: (BuildContext context,
          Animation<double> a1,
          Animation<double> a2,
          Widget widget) {
        final double curvedValue =
            Curves.easeInOutBack.transform(a1.value) - 1.0;
        return Transform(
          transform: Matrix4.translationValues(
              0.0, curvedValue * 200, 0.0),
          child: Opacity(
            opacity: a1.value,
            child: widget,
          ),
        );
      },
      transitionDuration: const Duration(milliseconds: 400),
      constraints:
          const BoxConstraints(minHeight: 460, minWidth: 300, maxWidth: 320),
    );
  }
```

The above example uses a few more `ColorPicker` properties. It is styled to be more compact and to show the general 
color name via `showColorName`, as well as the selected color's HEX color code by enabling `showColorCode`. With the 
color code field, you can also copy the color value to the clipboard using the copy icon button
suffix in the field. With the wheel picker, you can also enter a hex color RGB value in the color code field. 
The two wheel color HSV selection indicators will move to the color selection matching the entered HEX RGB value.

The above example also uses the `copyPasteBehavior` configuration class `ColorPickerCopyPasteBehavior()` with
`longPressMenu` set to true, to activate a long press context COPY-PASTE menu in the picker.

Most importantly, the above example uses the `showPickerDialog` method to show the defined `ColorPicker` in a 
pre-made dialog. The dialog also needs a build-context, we pass one to it.

The above example also demonstrates in version 3.0.0 new custom `transitionBuilder` and `transitionDuration` usage. This part has not been updated to be included in the screen recording below. Please make your own build of the default example to see it. 

In this example we also define size `constraints` for the dialog. If you do not define size constraints, it will 
auto size to fit the dialog content. Using constraints allows the dialog to keep the same size when the content 
size changes slightly as you switch between the different color picker types you enabled. It just looks a bit 
better if the dialog size does not change when you switch picker-type with the type selector. The color-wheel
picker in particular will often require more space. The wheel size can be customized as well. It does, 
however, become more difficult to use if it is made too small. In this example, it is on purpose on the 
lower side of a still usable size.

The result of the above setup is a `ListTile` where the trailing color indicator widget can be clicked to 
open a dialog to select a new color for the trailing `ColorIndicator` color.

As the `dialogPickerColor` changes the color in the dialog, the `ColorIndicator`'s color also changes via this
interaction. If the dialog is canceled, the `ColorIndicator`'s original color is restored.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/ColorPickerSimpleDemo.gif?raw=true" alt="ColorPicker dialog demo" width="300"/>

**Bonus Exercise - Not Included the Example Code** 

As an extra exercise, and to better see this interactive change of the color when it is modified in the dialog, 
try connecting the `dialogPickerColor` color to the `AppBar`'s `backgroundColor` property. 

Did you manage to do it? What happened?

```dart
:
appBar: AppBar(
  // To do this, just add this row to the AppBar in the example.
  backgroundColor: dialogPickerColor,
  elevation: 1,
  centerTitle: true,
  title: const Text('ColorPicker Demo'),
),
```

As can be seen below, now the selected color in the dialog changes the `AppBar`'s color and this happens as you
change the color in the dialog. If you select the color, it is kept and cancelling, restores the `AppBar`'s 
color as well, **pretty cool!**

You can use this principle to connect the color picking interaction to colors that define your application's theme 
colors and modify your application's theme color values while the app is running. Showing how to do
this goes a bit beyond the scope of this tutorial, but it is pretty much as easy as the interactive AppBar background 
color manipulation we just did.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/ColorPickerSimpleDemoAppBar.gif?raw=true" alt="ColorPicker appbar demo" width="300"/>

## Dialog ColorPicker Function

If you do not need the feature that allows you to modify and update colors interactively from the dialog via a 
callback, you can use a more straight-forward async dialog function API. This function opens the picker 
with a pre-selected color and either returns the selected color when closed with **OK**, or returns the
color you opened it with, when closed with **Cancel** action.

You can call this `showColorPickerDialog` dialog function directly from e.g., an `onTap` or `onSelect` callback, 
commonly found in Buttons, InkWell and similar Widgets with interaction callbacks. Make the callback async and 
wait for `showColorPickerDialog` to return the selected color value. 

Let's take a look at how this works. As before, first we define another `ListTile` with a trailing `ColorIndicator`.
We place it last after the previous two `ListTile`'s in our `ListView`, just before the `ColorPicker` that is in 
the `Card` in the `ListView`. For the color that we manipulate, we use the `dialogSelectColor` Color that we defined
earlier. In this case, the start color value is not a color that exists in the default Material primary and accent 
color picker or any shade of them. Because the color cannot be found in the pickers with pre-defined colors, the 
color picker will automatically select the **Wheel** picker and show the start color value we defined in it.

In this case we make our `ColorIndicator`'s `onSelect` callback **async** and directly from it call the 
`showColorPickerDialog`. In the function call we also define the `ColorPicker`'s properties we want it to use in
the dialog. We pass in the start color value and wait for it to return the color selection result, that we get
when the dialog is closed via **OK** or **CANCEL**. After that we can use the returned color value, in this example 
we just update our `dialogSelectColor` state variable. 

```dart
ListTile(
  title: const Text('Click to select a new color from a dialog'),
  subtitle: Text(
    '${ColorTools.materialNameAndCode(dialogSelectColor, colorSwatchNameMap: colorsNameMap)} '
    'aka ${ColorTools.nameThatColor(dialogSelectColor)}',
  ),
  trailing: ColorIndicator(
      width: 40,
      height: 40,
      borderRadius: 0,
      color: dialogSelectColor,
      elevation: 1,
      onSelectFocus: false,
      onSelect: () async {
        // Wait for the dialog to return color selection result.
        final Color newColor = await showColorPickerDialog(
          // The dialog needs a context, we pass it in.
          context,
          // We use the dialogSelectColor, as its starting color.
          dialogSelectColor,
          title: Text('ColorPicker',
              style: Theme.of(context).textTheme.titleLarge),
          width: 40,
          height: 40,
          spacing: 0,
          runSpacing: 0,
          borderRadius: 0,
          wheelDiameter: 165,
          enableOpacity: true,
          showColorCode: true,
          colorCodeHasColor: true,
          pickersEnabled: <ColorPickerType, bool>{
            ColorPickerType.wheel: true,
          },
          copyPasteBehavior: const ColorPickerCopyPasteBehavior(
            copyButton: true,
            pasteButton: true,
            longPressMenu: true,
          ),
          actionButtons: const ColorPickerActionButtons(
            okButton: true,
            closeButton: true,
            dialogActionButtons: false,
          ),
          constraints: const BoxConstraints(
              minHeight: 480, minWidth: 320, maxWidth: 320),
        );
        // We update the dialogSelectColor, to the returned result
        // color. If the dialog was dismissed it actually returns
        // the color we started with. The extra update for that
        // below does not really matter, but if you want you can
        // check if they are equal and skip the update below.
        setState(() {
          dialogSelectColor = newColor;
        });
      }),
),
```

This dialog picker example also introduces a few more properties that we have not used before. For starters, 
we gave it a `title` widget instead of a `heading`. The title is more like the title of an `AppBar`. We 
also skipped all the subheading widgets to make a more compact picker. 

We used the `copyPasteBehavior` to define a `ColorPickerCopyPasteBehavior` configuration
that enables both copy (`copyButton: true`) and paste (`pasteButton: true`) action icon buttons in the picker's top
title toolbar. We also kept the long-press copy-paste menu from the previous picker example.

Additionally, we used the `actionButtons` to configure some options for the dialog action buttons with a 
`ColorPickerActionButtons` configuration class. With it, we set `dialogActionButtons: false`, to remove 
the dialog's bottom **CANCEL** and **OK** action buttons. Instead, we set `okButton: true` and `closeButton: true`, 
to enable an 'OK' check mark icon-button, and a 'Close' x icon-button in the dialog's top toolbar.

As a major new feature we also in the `ColorPicker` set `enableOpacity: true`. This shows the opacity slider
in the `ColorPicker`, that we can use to adjust the opacity from 0 to 100% of the selected. 

We also set `colorCodeHasColor: true`, this changes the style of the displayed color code field's background color.
It will now use the currently selected color as the field's background color. Making it show the color result of our
current color selection and opacity slider setting. The opacity slider has a checkered background,
so you can see how opaque the selected opacity value is when it is used on top of other widgets or images.

Below you can see the result of this picker setup, and also a demo of how you can copy-paste a selected color.

In the demo below, we just copy and pate a color from one dialog picker to another, but you can copy-paste colors
between the picker and any other app. On desktop builds, the app also supports keyboard COPY-PASTE shortcuts. For more
information about the COPY-PASTE features, see the API guide's chapter regarding its 
[features](#copy-paste-actions-and-behavior).

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/color_picker_copy_paste_demo.gif?raw=true" alt="ColorPicker copy-paste demo" width="300"/>

Under the hood, the `showColorPickerDialog` function uses the same `ColorPicker` and `showPickerDialog` method. 
It just bundles them together in one single async `showColorPickerDialog` function.

The API surface of this function is quite large. It bundles all the `ColorPicker` properties, 
including its `showPickerDialog` method's parameters, and an `AlertDialog`, with all its properties, plus 
the `showDialog` function and its parameters, all into one large function.

Despite its large API surface, it is still rather convenient to use. You seldom need to use
most of the underlying API properties, usually the default values for them work fine. They are exposed, 
should you ever need them.

**Finally**, the default example also includes a light and dark theme mode toggle. It is there so that you 
can test the look and operation of the color picker with a dark theme.

# API Guide

In addition to what is covered in the above [tutorial](#tutorial), the **FlexColorPicker** has a large number of 
additional features. Its behavior can easily be modified with its direct
properties and two additional configuration property classes `ColorPickerActionButtons` and
`ColorPickerCopyPasteBehavior`, that can be configured and passed in for even more customization options.

This guide goes through most of the API settings and provides links to API references. Below we will explore 
the `ColorPicker` APIs in more detail, and cover both basic and advanced features of
the **FlexColorPicker**.

## Elements of the Picker

This chapter shows the different visible elements of the color picker that you can enable and disable, or add as 
extra Widgets to the picker.

In [**main example**](#tutorial) and its tutorial, at the core is a passed in `Color()` object to the color picker's 
`color` property. It is used to pass in the color that the picker should pre-select. It will update, to show the new 
color if the picker Widget is updated with a new color. The `color` property is **not** required, it defaults 
to `Colors.blue` if it is omitted, but normally you would give it a starting value based on the color you want to 
modify.

The other main property is the `ValueChanged<Color>` callback `onColorChanged`. This is called whenever a new 
color value is selected in the color picker, with the selected color. What you do with the callback color depends 
on your use-case. In the tutorial examples we update the passed in color with `setState`, and the changed
color is shown in a color indicator widget, in the shape of a colored box or circle.

However, in the one of the dialog examples, it was also demonstrated how it can also be used to interactively change 
the `AppBar` color of the app itself. You can use the picker to change any color in
your application theme, or the color used by any Widget.

**The two core properties of the ColorPicker:**

```dart
ColorPicker(
  color: myColor,
  onColorChanged: (Color color) => setState(() => myColor = color),
),
```

If you need to update the `ColorPicker` externally pass in a new value to the `color` property. 
In the above example you could give the state variable `myColor` a new value from some other place than 
the above `onColorChanged` callback, and call `setState`. The [live Web demo](https://rydmike.com/flexcolorpicker/)
includes an example of how you can update the `ColorPicker` via other widget interactions, 
or even remote control, or mirror it completely from another **FlexColorPicker** opened as a dialog.

### Enabled Color Pickers

API reference: [pickersEnabled](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/pickersEnabled.html)

By default, the Material **primary** colors and **accent** colors pickers are enabled. To change the enabled pickers, 
you provide a `ColorPickerType` key to `bool` value map, with the pickers you want enabled to the property
`pickersEnabled`. You only need to provide key-values pairs for picker keys you want to change. Key values that are not 
provided use their defaults. 

If you only have one picker enabled, there is no sliding segment (tab) control shown that will allow you to switch 
between different color picker types. That would be pointless, since there is only one color picker. If all pickers
are disabled, the Material primary color picker will be shown.

If all other features are disabled, by default, they are not, then the screenshot below represents an example of a 
bare-bones **minimum picker**, showing only the main colors of the Material primary colors. If other defaults are OFF,
to enable producing this picker style, only the `pickersEnabled` setting to disable the accent color picker is needed 
to get the shown picker: 

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-enabled-1.png?raw=true" alt="Pickers 1"/>

Normally, you would enable a few more pickers. Below we enable the primary, secondary, near black and white and the wheel
picker. Since more than one picker is enabled, the color picker selector automatically appears:

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-enabled-2.png?raw=true" alt="Pickers 2"/>

If you want to show both Material primary and accent colors in the same picker, you can enable the 
`ColorPickerType.both` picker. In that case you usually want to disable `ColorPickerType.primary` and 
`ColorPickerType.accent`, as they contain duplicates of already available colors in the `both` picker. The live 
Web demo implements this as exclusive selections in its own logic. It is possible to show all three pickers,
but it really makes little sense.

### Enable Shades Selection

API reference: [enableShadesSelection](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/enableShadesSelection.html)

By default, selection of the Material primary and Accent **color swatch shade color**, after selection of the main
color, is **enabled**. In the above example `enableShadesSelection` had on purpose been disabled to produce the above,
main only color, very compact color picker example.

Below, we enable the Material color swatch shades selection. Typically, you want to be able
to also select the Material shade colors. Normally, you would just keep the default enabled setting and don't have to
use this property at all. You only need this property if you ant to disable the color-shade selection feature, 
which you do by setting `enableShadesSelection` to false.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-enabled-4.png?raw=true" alt="Pickers 4"/>

### Tonal Palette

API reference: [enableTonalPalette](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/enableTonalPalette.html), [tonalColorSameSize](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/tonalColorSameSize.html)

By default, generation of a selected color's Material-3 tonal-palette is disabled. You can enable
it by setting `enableTonalPalette` to true. 

When you select a color in the color picker and tonal palette is enabled, a 15-shade 
Material-3 tonal-palette for the selected color will be generated. The palette always starts 
with black, tone 0 for the used seed color and ends in white, tone 100.
    
The official Material 3 Dart library is used to create the tonal palette from any 
selected color. The color you select functions a seed color to generate the tonal
palette and might not itself be included and selected in the palette. You can
click on any color in the generated palette to select and pick a color.

Selecting a color in the tonal palette, only selects the color in the palette; it 
does not update the palette. Only when you select a color from the other color 
sources in the picker, is that color used as key color, to seed and generate an 
updated color palette for the selected color.

For more info on the Material-3 Color system see the [official guide](https://m3.material.io/styles/color/the-color-system/key-colors-tones).

The picker item size for tonal palette color indicator items is
10/13 the size of defined width and height. This is done to
as far as possible, try to match the width of the Primary Material Swatch
items total width. It has 10 colors, the M3 tonal palette has 15 colors.
The goal is to match their width when they are both shown. If you want the tonal 
palette color indicator items to be the same size as the other color indicators, 
set `tonalColorSameSize: true`.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-enabled-tonal-4.png?raw=true" alt="Tonal pickers 4"/>



### Custom Color Swatches

API reference: [customColorSwatchesAndNames](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/customColorSwatchesAndNames.html)

To use the custom-color swatch picker, you have to define your own custom `ColorSwatch` colors and pass them to the
picker via the `customColorSwatchesAndNames` property. By default, there are no custom colors defined. If you
enabled the `custom` picker and have not provided any custom color swatches, the picker will not be shown despite 
being enabled, since it has no colors to show.

You can make `ColorSwatch` objects with the Flutter SDK `MaterialColor` or the `MaterialAccentColor` classes by 
providing swatch color shades for each index. Alternatively you can use the `FlexColorPicker` helpers 
`ColorTools.createPrimarySwatch(color)` and `ColorTools.createAccentSwatch(color)` by just giving it a single color 
value. For `createPrimarySwatch` the provided color will always be used as the base for the [500] index and 
for `createAccentSwatch` for as color for index [200], the rest of the index color shades are computed. 

> Please note that these helpers just produce lighter and darker shades of the provided color for lower and higher 
> swatch indexes. If you give e.g., the `createPrimarySwatch` the same color value as a built-in Material primary 
> color with index [500], you will not get the same swatch as the built-in Material primary color swatch. 

To define color data to use with the `customColorSwatchesAndNames` property, to start using the custom color picker, 
first make a final **Map** with your custom `ColorSwatch` objects, and their color names. 
You decide what the colors are called. Here we use different methods make three custom colors.

```dart
final Map<ColorSwatch<Object>, String> customSwatches =
<ColorSwatch<Object>, String>{
  const MaterialColor(0xFFfae738, <int, Color>{
    50: Color(0xFFfffee9),
    100: Color(0xFFfff9c6),
    200: Color(0xFFfff59f),
    300: Color(0xFFfff178),
    400: Color(0xFFfdec59),
    500: Color(0xFFfae738),
    600: Color(0xFFf3dd3d),
    700: Color(0xFFdfc735),
    800: Color(0xFFcbb02f),
    900: Color(0xFFab8923),
  }): 'Alpine',
  ColorTools.createPrimarySwatch(const Color(0xFFBC350F)): 'Rust',
  ColorTools.createAccentSwatch(const Color(0xFFB062DB)): 'Lavender',
};
```
Then use the `customSwatches` map in your color picker as value for the `customColorSwatchesAndNames` property.

```dart
ColorPicker(
  color: myColor,
  onColorChanged: (Color color) => setState(() => myColor = color),
  pickersEnabled: const <ColorPickerType, bool>{
    ColorPickerType.both: false,
    ColorPickerType.primary: true,
    ColorPickerType.accent: true,
    ColorPickerType.bw: false,
    ColorPickerType.custom: true,
    ColorPickerType.wheel: true,
  },
  customColorSwatchesAndNames: customSwatches, // Our custom swatch colors.
```

This will create three custom color swatches, using our "Alpine", "Rust" and "Lavender" custom names in the **Custom** 
swatch picker.
<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-enabled-6.png?raw=true" alt="Picker 6"/>

### Customized labels
API reference: [pickerTypeLabels](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/pickerTypeLabels.html)

The picker labels have default English labels, you can override them to customize or translate the labels. You set the
labels by providing a `ColorPickerType` key to `String` value map with the picker labels you want to change with the
property `pickerTypeLabels`. You only have to provide key-value pairs for the labels you want to change, omitted keys 
will keep their default labels.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-enabled-3.png?raw=true" alt="Pickers 3"/>

### Enable Opacity

API reference: [enableOpacity](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/enableOpacity.html)

You can enable a color opacity slider by setting `enableOpacity` to `true`. With the slider, you can adjust the opacity
of the selected color. You can adjust opacity from totally opaque at 100%, to totally transparent at 0%. The selected
color and the impact of the opacity value on it are visualized by the checkered gradient on the opacity slider, 
and the selected color's opacity gradient on the slider. The thumb's position is over the resulting color's opacity 
when applied over a background.

The slider thumb label only shows opacity value changes in 1% increments. However, the slider has 255 discrete steps,
so there is a step for every alpha value in the resulting ARGB color value. If the color code value is enabled and
set to a format that includes the alpha, you can see that the alpha value can be adjusted in single increments
with the slider.

You cannot pass in opacity separately to the color picker to get a starting opacity value. If your passed in color
value has opacity in its alpha channel, it will automatically get used, but only if `enableOpacity` is true. If it
is false, any opacity or alpha in the color value, or in a color pasted into the picker, is ignored and used
as opaque by applying alpha #FF to it.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-enabled-5.png?raw=true" alt="Picker 5"/>

### Show Color Names

API reference: [showMaterialName, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/showMaterialName.html) 
[materialNameTextStyle, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/materialNameTextStyle.html) 
[showColorName, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/showColorName.html) 
[colorNameTextStyle.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/colorNameTextStyle.html)

The color picker can be configured to show the selected color's Material color name and its selected shade index number. 
It can also be configured to show a color name for any selected color based on the `ColorTools.nameThatColor` function, 
that uses a lookup list of **1566** color codes and their names. It finds the color that closest matches the selected 
color on the list, and shows this as the selected color's name after the Material color name. You can also provide 
the text style for these color name labels. If not provided they default to
`Theme.of(context).textTheme.bodyMedium`.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-enabled-7.png?raw=true" alt="Picker 7"/>

#### Translate Material Color Names

API reference: [Static color names](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorTools-class.html#static-properties)

The Material color names are defined as static values with English defaults for all Material colors in `ColorTools`. 
You can modify these values by directly changing their static string values. You can do this in a function that you 
call just once, or every time your app changes its translated locale and then 
provide your own localized Material color names. For example:

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-8.png?raw=true" alt="Picker 8"/>

> [!NOTE]
> The "name that color" feature using the lookup from 1566 color names is only available in English and cannot be
translated. 

### Show Color Code

API reference: [showColorCode, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/showColorCode.html)
[colorCodeHasColor, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/colorCodeHasColor.html)
[showColorValue, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/showColorValue.html)
[colorCodeTextStyle, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/colorCodeTextStyle.html)
[colorCodePrefixStyle.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/colorCodePrefixStyle.html)

The color code field shows the RGB color value of the selected color. On the **Wheel** picker the field also functions
as a HEX RGB color code **entry** field. The Wheel picker will move its indicators to show the color of the entered
color code, as the entry is done for every entered or deleted character in the field.

By default, the code field has a grey background, but you can also configure it to use the current selected color
as its background color. The color code field can also have a copy button as a suffix. This is **enabled by default** 
it allows you to copy the current color to the clipboard. There are different options for enabling copy-paste commands
in the FlexColorPicker and configuring the copy format also shown as prefix in the color code field. These features
are described in detail in the [copy-paste actions and behavior](#copy-paste-actions-and-behavior) chapter. 

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-9.png?raw=true" alt="Picker 9"/>

The `TextStyle` of the color code display and entry field can be changed with `colorCodeTextStyle`. It
defaults to `Theme.of(context).textTheme.bodyMedium`, if not defined. There is also a separate style for the
color code prefix that can be changed with `colorCodePrefixStyle`, if not defined it defaults to the same style as
`colorCodeTextStyle`.

### Show Recent Colors

API reference: [showRecentColors, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/showRecentColors.html)
[maxRecentColors, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/maxRecentColors.html)
[recentColors, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/recentColors.html)
[onRecentColorsChanged.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/onRecentColorsChanged.html)

When `showRecentColors` is enabled, the color picker shows recently selected colors in a list at the bottom of the
color picker. The list uses first-in, first-out to keep min 2 to max 20 colors (defaults to 5) on the recently 
used colors list, the desired max value can be modified with `maxRecentColors`.

Selecting a recently used color, moves the picker to the picker where the color is located and selects it again. If 
opacity is enabled, the opacity the color had when it was selected is also applied. Normally, when selecting colors and 
opacity is enabled, the value the opacity slider is at is kept. However, when selecting a recently used color, the 
opacity the color had when it was selected and added to the recently used colors list will be used. 

Selecting a color on the recently used colors list will not move it first in the list. It will keep its current 
position. Selecting a color already on the list will not add it again. The currently selected color is 
not added to the list until you select a new current color.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-10.png?raw=true" alt="Picker 10"/>

There is also an optional callback `onRecentColorsChanged`, that is called everytime a new color is added to the list, 
with the complete current list of recently used colors. If the optional callback is not provided, then it is not called.
You can use this callback to save and restore the recently used colors. 

To initialize the list when the color picker is created, give it a starting list with `recentColors`.
This start list could be a list kept in state during the current app session. It is then used 
when the color picker is created and re-opened to show the same recent colors used previously during the 
session. The start list could also even have been persisted and restored from a previous session. 
The live Web demo persists and restores the recently used colors-lists between 
sessions, in addition to all the settings, you can use it as an example of how to do this.

### Title and Heading Widgets

API reference: [title, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/title.html)
[heading, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/heading.html)
[subheading, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/subheading.html)
[tonalSubheading, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/tonalSubheading.html)
[wheelSubheading, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/wheelSubheading.html)
[opacitySubheading, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/opacitySubheading.html)
[recentColorsSubheading.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/recentColorsSubheading.html)


You can provide custom heading widgets for the picker's toolbar `title`, main `heading`, shades selection color 
`subheading`, tonal palette `tonalSubheading` and the `wheelSubheading`, opacity slider 
`opacitySubheading` and subheading for the recently used 
colors list `recentColorsSubheading`. If a heading is `null`, it is omitted. The headings can be any Widget, 
but typically they are `Text` widgets with a suitable style, as shown below.

The `tonalSubheading` in the tonal palette added in version 2.3.0 is not shown in the example 
image below, but it would be below the shade `subheading` and equivalent to it.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-11.png?raw=true" alt="Picker 11"/>

## Picker Design

The picker design APIs refer to properties that affect the size, shape and spacing of the individual color indicator 
Widgets inside the color picker, as well as the color wheel and opacity slider sizing. 

The [ColorIndicator](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorIndicator-class.html) 
Widget can also be used as a color indicator and selection widget outside the color picker. This is done 
in the default example, where it is used to show the selected color and also to open a dialog to modify the color.

### Color Picker Items

API reference: [height, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/height.html)
[width, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/width.html)
[borderRadius, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/borderRadius.html)
[hasBorder, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/hasBorder.html)
[borderColor, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/borderColor.html)
[elevation, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/elevation.html)
[spacing, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/spacing.html)
[runSpacing.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/runSpacing.html)

The color items that show the available colors can be modified. Their `height`, `width`, `borderRadius` plus their
`elevation`, and if they have a border `hasBorder` and what color the border is `borderColor`
(defaults to divider theme) can all be changed. 

Additionally, the `spacing` between the color box items and their `runSpacing` when they wrap to more than one 
row can be adjusted. The color picker items for the Material, Accent, B&W and Custom colors use a `Wrap` widget for
their layout, as do shade colors, and the colors in recently used colors list. 

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-13.png?raw=true" alt="Picker 13"/>

### Wheel Diameter, Width and Border

API reference: [wheelDiameter, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/wheelDiameter.html)
[wheelWidth, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/wheelWidth.html)
[wheelHasBorder, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/wheelHasBorder.html)
[borderColor.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/borderColor.html)

The **wheel** color picker's `wheelDiameter`, `wheelWidth` and border can be modified. The `borderColor` is 
the same property as the color picker's color items' border, but it has its own enable/disable toggle 
`wheelHasBorder` (defaults to false). The color-wheel width must be from 4 to 50 dp, and it defaults to 16 dp. The 
color-wheel diameter must be from 100 to max 500 dp, and it defaults to 190 dp.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-15.png?raw=true" alt="Picker 15"/>

### Opacity Slider Height, Width and Thumb Radius

API reference: [opacityTrackHeight, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/opacityTrackHeight.html)
[opacityTrackWidth, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/opacityTrackWidth.html)
[opacityThumbRadius.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/opacityThumbRadius.html)

The opacity slider's height `opacityTrackHeight`, width `opacityTrackWidth` and thumb radius `opacityThumbRadius` can be 
adjusted, below some examples:

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-16.png?raw=true" alt="Picker 16"/>

If the slider width is not defined, which it is not by default, it expands to fill available picker width.
Its minimum allowed width is 150 dp. The slider height must be from 8 to 50 dp and thumb radius from 12 to 30 dp.

## Picker Layout

API reference: [crossAxisAlignment, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/crossAxisAlignment.html)
[padding, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/padding.html)
[columnSpacing.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/columnSpacing.html)

The picker layout APIs deal with spacing of the elements in the color picker, their alignment and padding.

Use the properties `crossAxisAlignment`, `padding` and `columnSpacing` to adjust the look of the color picker content.
The `columnSpacing` refers to the additional vertical spacing between each element in the column used by the color 
picker layout. The `padding` and `crossAxisAlignment` are as typically used in Flutter. Please note that
`title` widget is not a part of the `Column` body layout of the color picker, and it is not affected by the
`crossAxisAlignment` property. You can think of the `title` a bit like an app bar title. It is always start 
aligned to leave enough space for one to four action buttons. The action buttons can optionally be enabled for the title bar, 
and they always appear at the end.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-12.png?raw=true" alt="Picker 12"/>

### Tooltips

API reference: [enableTooltips](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/enableTooltips.html)

The `enableTooltips` property defaults to true and enables all tooltips that are available in the color picker. If the
tooltips get in the way, you can disable them all by setting this property to `false`. Why not consider providing a 
property in your app that allows users to turn ON and OFF all the tooltips in the app? **FlexColorPicker** 
includes this toggle to make this easy to implement when it comes to its own tooltip behavior.

The tooltip strings used in FlexColorPicker are all based on existing labels in Flutter SDK and by default use
Material localizations and thus change with the locale. By doing this, they support all languages that Flutter does out 
of the box. You can still override the tooltip labels if so required and provide your own tooltip labels.

The following tooltips exist and use the default values shown in the table below.

| Usage         | English tooltip | Used MaterialLocalizations.of(context) |
|---------------|-----------------|----------------------------------------|
| Copy button   | Copy            | copyButtonLabel                        |
| Paste button  | Paste           | pasteButtonLabel                       |
| OK button     | OK              | okButtonLabel                          |
| Cancel button | Cancel          | cancelButtonLabel                      |
| Close button  | Close           | closeButtonLabel                       |


<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-14.png?raw=true" alt="Picker 14" width="500"/>

When the keyboard copy/paste shortcuts are enabled, the Copy and Paste tooltips automatically
also receive platform-aware keyboard-shortcut info, after the localized tooltip label. On macOS
' (CMD-C)' is appended to the copy tooltip and ' (CMD-V)' is appended to the paste tooltip.
On other platforms ' (CTRL-C)' is appended to the copy tooltip and ' (CTRL-V)' to the paste tooltip.

## Dialog Action Buttons

API reference: [ColorPickerActionButtons](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerActionButtons-class.html)

The API surface of the color picker was getting quite large. Therefore, two configuration classes are 
used to configure additional less frequently used settings. The first one is the
`ColorPickerActionButtons` used to define the color picker's 
OK and Cancel action buttons, and their style when they are used by the built-in dialogs.

You use it by passing in a `ColorPickerActionButtons` configuration to the `ColorPicker()`'s property `actionButtons`: 

```dart
ColorPicker(
  actionButtons: const ColorPickerActionButtons(...),
); 
```
You can define if **OK** and **Close** action buttons are on the top toolbar, or only in the dialog bottom actions 
area. The top toolbar buttons are plain icon-only buttons. For the bottom dialog action buttons you can choose between
`TextButton`, `OutlinedButton` and `ElevatedButton` for each button.

The used icons can be changed from default ones, as can their used tooltips. The labels on the bottom
action buttons can also be changed. By default, they, like the tooltips, use Material localizations, so they 
work well enough out of the box for most locales. The bottom action buttons can also use the default or
customized OK and Cancel **icons as prefix** icons to the labels. These icons are always shared with the 
corresponding icons defined for the top toolbar icon buttons.

The recommendation is to **not** use the top and bottom action buttons at the same time, but rather select one of the 
two options. The API does, however, allow us to use both, or even a mix and match. It is, for example, possible to 
show **Cancel** and **OK** actions at the bottom of the dialog, and also add just the 'x' close icon in the upper 
end corner of the dialog. This 'x' icon then also cancel closes the dialog as expected. This is a useful combination.
Adding the **OK** icon button, by default a check icon, as a close button to the top toolbar is a bit 
unconventional, if you also have the OK button as a bottom action. Without it enabled, the OK and Close buttons 
on the toolbar are a nice and compact alternative to selecting color or cancelling the dialog.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-17.png?raw=true" alt="Picker 17"/>

The bottom action buttons and their style depend on their ambient theme. 

There are more dialog action buttons design properties you can adjust, you can, for example, change 
the order of the OK and Cancel action, or have it be platform adaptive. 
By default, OK is on the right. Please see the
[ColorPickerActionButtons API reference](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerActionButtons-class.html)
for additional details.

## Copy-Paste Actions and Behavior

API reference: [ColorPickerCopyPasteBehavior](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior-class.html)

The `ColorPickerCopyPasteBehavior` is the second configuration-class group. It is used to configure the desired
COPY-PASTE behavior of the color picker. You use it by passing in a `ColorPickerCopyPasteBehavior` 
configuration to the `ColorPicker()`'s property `copyPasteBehavior`:

```dart
ColorPicker(
  copyPasteBehavior: const ColorPickerCopyPasteBehavior(...),
); 
```
You can control if the picker has:

* Copy and paste action buttons in the top toolbar.
* Long press and/or right click copy and paste context-menu.
* Ctrl-C and Ctrl-V keyboard shortcuts, also when not in the edit field.
  Keyboard shortcuts automatically use Command instead of Ctrl on macOS.
* A copy color action button in the code entry and display field.

You can also:
* Define a default result RGB string-format, for the copy command.
* Define icons for copy and paste action buttons.
* Define an icon-theme for the copy and paste icons.
* Define paste color-string parsing error feedback-type and message if used.
* Modify the tooltips for copy and paste buttons.

Paste operation supports all RGB string formats defined by 
[ColorPickerCopyFormat](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyFormat-class.html), 
but the copy format is only in the selected `copyFormat`.

### Code Field Copy Button

API reference: [editFieldCopyButton](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/editFieldCopyButton.html)

The color code display and entry field suffix **color copy icon button** are enabled by default. This
button existed already in version 1.x. It can now if so desired be removed by setting
`ColorPickerCopyPasteBehavior.editFieldCopyButton` to false.  

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-18.png?raw=true" alt="Picker 18"/>

### Keyboard Shortcuts

API reference: [ctrlC, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/ctrlC.html)
[ctrlV.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/ctrlV.html)

When `ctrlC` and `ctrlV` properties are set to `true`, by default they are, a CTRL/CMD-C keyboard press on a 
desktop keyboard will copy the currently selected color's RGB color code to the clipboard. A CTRL/CMD-V will 
paste the current clipboard text into the picker. The color picker will then try to parse the pasted value as a color
value and move to display the pasted color with the most suitable available picker. The CTRL keyboard modifier is used on 
Windows and Linux desktop OS, and the CMD modifier is used on macOS and iOS.

When enabled, the keyboard copy color shortcuts work when one of the ColorPicker's focusable widgets has focus.
These include the color indicators, color field, buttons, and the picker selector, as well as the color wheel. When the 
picker is used in a modal dialog, one of its widgets will typically always have focus. If the picker is used in 
layouts on the main surface, where other widgets may have focus, the keyboard shortcuts will not work until one of 
the color picker's focusable widgets gets focus.

When the keyboard copy/paste shortcuts are enabled, the Copy and Paste tooltips by default 
also receive platform-aware keyboard-shortcut info. After the localized default tooltip label, on macOS
' (CMD-C)' is appended to the copy tooltip and ' (CMD-V)' is appended to the paste tooltip.
On other platforms ' (CTRL-C)' is appended to the copy tooltip and ' (CTRL-V)' to the paste tooltip. This is shown
in the example in the next chapter.

### Toolbar Buttons

API reference: [copyButton, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/copyButton.html)
[copyIcon, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/copyIcon.html)
[copyTooltip, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/copyTooltip.html)
[pasteButton, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/pasteButton.html)
[pasteIcon, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/pasteIcon.html)
[pasteTooltip.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/pasteTooltip.html)

You can show a copy and paste action icon button in the picker's top toolbar end by setting `copyButton` and 
`pasteButton` to `true`. You change their default icons, that are `Icons.copy` and `Icons.paste`, by defining the 
properties `copyIcon` and `pasteIcon`. Their tooltips can also be changed.

The `copyTooltip` defaults to `MaterialLocalizations.of(context).copyButtonLabel`. If CTRL-C keyboard shortcut 
copying is also enabled, the string ' (CTRL-C)' is added on Linux and Windows platforms and on macOS ' (CMD-C)' 
is added.

The `pasteTooltip` defaults to `MaterialLocalizations.of(context).pasteButtonLabel`. If CTRL-V keyboard shortcut
copying is also enabled, the string ' (CTRL-V)' is added on Linux and Windows platforms and on macOS ' (CMD-V)'
is added.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-19.png?raw=true" alt="Picker 19"/>

### Context Menu

API reference: [secondaryMenu, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/secondaryMenu.html)
[longPressMenu, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/longPressMenu.html)
[secondaryOnDesktopLongOnDevice.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/secondaryOnDesktopLongOnDevice.html)

The **FlexColorPicker** provides a menu option for copying and pasting colors from and to the picker. You can 
enable a context like COPY-PASTE menu that can be triggered either via a long press or secondary mouse click, 
typically the right mouse button.

The secondary right click is often a good option on Windows and Linux desktop apps, to some extent it may also work 
on desktop web browsers. However, desktop browsers' built-in right-click menu also tends to get triggered by it. 
This menu may get in the way of the color picker's COPY-PASTE menu when secondary click is used in 
a desktop Web browser. On touch-only devices, or other use cases when a mouse right click is not optimal, 
the long press option to show the COPY-PASTE menu may work better.

Set property `secondaryMenu` to `true` (defaults to false), to enable using secondary button click anywhere in 
the color picker to open up the COPY-PASTE context menu.

Set property `longPressMenu` to `true` (defaults to false) to enable using long press anywhere in the color 
picker, to open up the COPY-PASTE context menu.

Set property `secondaryOnDesktopLongOnDevice` to `true` (defaults to false), to enable using long press in the color
picker to open up the COPY-PASTE context menu on iOS and Android touch devices. This allows you to still use secondary mouse button click on desktop platforms on Windows, Mac and Linux, as well as on desktop-based web browsers.

Set property `secondaryOnDesktopLongOnDeviceAndWeb` to `true` (defaults to false), to enable using long press in the color
picker, to open up the COPY-PASTE context menu on Web, iOS and Android touch devices. While using secondary mouse button
on desktop platforms Windows, Mac and Linux, but not if it is a desktop web app.

> Due to secondary-button on desktop Web browsers often activating the browser's own 
> secondary-button context menu, the `secondaryOnDesktopLongOnDevice` option may not be ideal for desktop 
> web browsers. You may want to use `secondaryOnDesktopLongOnDeviceAndWeb` option instead to avoid right-click
> menus on web desktop automatically, and thus automatically prefer long press on it as well.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-20.png?raw=true" alt="Picker 20"/>

If you want to style and customize the look of the popup-menu, it can also be done. Please refer to the following
APIs [menuThemeData](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/menuThemeData.html),
[menuWidth](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/menuWidth.html), 
[menuItemHeight](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/menuItemHeight.html), and 
[menuIconThemeData](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/menuIconThemeData.html) for more information.

### Color Code Formats and Paste Parsing

API reference: [copyFormat, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/copyFormat.html)
[parseShortHexCode, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/parseShortHexCode.html)
[editUsesParsedPaste, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/editUsesParsedPaste.html)
[snackBarParseError, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/snackBarParseError.html)
[snackBarMessage, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/snackBarMessage.html)
[snackBarDuration, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/snackBarDuration.html)
[feedbackParseError.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/feedbackParseError.html)

 [**copyFormat**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/copyFormat.html)  
 The color code display and edit field's value can be shown in five different formats by the setting the
 `copyformat` enum
[ColorPickerCopyFormat](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyFormat-class.html)
to desired format value. The `copyFormat` **also** defines the received string format of the copied RGB value when
 **any** of the copy functions are used. It defaults to `ColorPickerCopyFormat.dartCode`.

| ColorPickerCopyFormat | Resulting format                                                    |
|-----------------------|---------------------------------------------------------------------|
| dartCode              | Flutter Hex RGB format '0xAARRGGBB' (**default**)                   |
| hexRRGGBB             | Hex RGB format with no alpha 'RRGGBB'                               |
| hexAARRGGBB           | Hex RGB format with alpha 'AARRGGBB'                                |
| numHexRRGGBB          | Web Hex RGB format with a leading num # sign and no alpha '#RRGGBB' |
| numHexAARRGGBB        | Web Hex RGB format with a leading num # sign and alpha '#AARRGGBB'  |

When pasting color RGB text string values into the color picker, any of the above formats are always accepted and 
parsed to its color value.

The color picker's paste parser also filters out none valid HEX code related characters from the string, and 
truncates it to the max length of the above formats from the right (end) side!
Partial values like for example '0', 'aC', '#334' and '0xFF34' are also allowed and are interpreted as being right aligned 
in the complete 8-char hex code. 

If alpha values are not included in a pasted hex char string, it is always set to
'FF'. If alpha is included in the pasted color value, but alpha via
[enableOpacity](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/enableOpacity.html)
is not enabled for the color picker, then the alpha value included in the pasted color string value will be replaced
with 'FF' or fully opaque.

[**parseShortHexCode**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/parseShortHexCode.html)  
The color picker's paste parser can optionally also interpret 3-char hex code as done by CSS/WEB. This is enabled by
setting `parseShortHexCode` to `true` (defaults to false). When true, the hex color code paste action and field 
entry parser will interpret short three character web hex color codes like when using CSS/WEB. This results in 
short HEX RGB color codes, like 123, ABC, F0C and 5D1 being interpreted as 112233, AABBCC, FF00CC and 55DD11.

[**editUsesParsedPaste**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/editUsesParsedPaste.html)  
The color code entry field can also be set to use the paste parser by setting `editUsesParsedPaste` to `true` (defaults
to false). When true, the color code entry field uses the paste parser for keyboard paste shortcuts.  
A standard text field keyboard paste shortcut, will paste whatever text is in the copy-paste buffer into the field.
This is the `false` default behavior here too, with the exception that the field only accepts valid hex value input
chars (0–9, A–F). It thus always filters out and pastes only the acceptable input characters from the paste buffer.

When `editUsesParsedPaste` property is `true`, the edit field will use the same color paste value parser used
by the other paste actions when the input field is not in focus. This results in a paste action in the entry field that 
always fully replaces the content with the parsed color value of the pasted string data. It does not paste in the 
string in the paste buffer into the text field, it changes it to its parsed value, converted back to a string. 
Currently, this setting only impacts CTRL-V and CMD-V keyboard shortcut
pasting on desktops. The paste on Android and iOS are not intercepted when this setting is true. The false setting is 
equivalent to past versions (1.x) default behavior when pasting strings into the code entry field. 

Setting `editUsesParsedPaste` to true, may be preferred for a more consistent paste experience in the picker.

[**snackBarParseError**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/snackBarParseError.html)  
Set `snackBarParseError` to `true`, to show a snack bar paste parse error message when pasting something that
could not be parsed to a color value, into the color picker. A paste parse error occurs when something is pasted 
that cannot be parsed to a color value. 

[**snackBarMessage**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/snackBarMessage.html)  
The `snackBarMessage` defines the text message label shown in the paste parse error snack bar. The `snackBarMessage` 
label is shown in the snack bar when there is a paste parse error, and `snackBarParseError` is true. 

If the `snackBarMessage` is not defined (is null), it defaults to the combination of the two Material localization
labels `pasteButtonLabel`: `invalidDateFormatLabel`. In English, this will say
**Paste: Invalid format**. The `Snackbar`, uses the closest ambient theme with `SnackBarThemeData` for its theming.

Below an example of a `copyformat`, `parseShortHexCode`, `editUsesParsedPaste` and `snackBarParseError` configuration,
and a snack bar parse error message.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-21.png?raw=true" alt="Picker 21"/>

[**snackBarDuration**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/snackBarDuration.html)  
The duration the paste parse error snack bar message is shown can be set via `snackBarDuration`. It defaults to 
`const Duration(milliseconds: 1800)`.

[**feedbackParseError**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPickerCopyPasteBehavior/feedbackParseError.html)  
By setting `feedbackParseError` to true the device will vibrate, make an audible click sound or an alert sound on some
platforms, when a paste parse error occurs.

This feature is **experimental**, its support is **very** limited on most platforms in Flutter. If Flutter SDK some day 
supports the Material Sound Guide sounds, this feature can be improved with better sound effects. Currently, it cannot
be improved without importing none SDK plugins/packages to make sounds. This package strives to work without any 
plugins or packages, so it will not add any none Flutter SDK imports. (Defaults to `false`).

## onChange Callbacks

API reference: [onColorChanged, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/onColorChanged.html)
[onColorChangeStart, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/onColorChangeStart.html)
[onColorChangeEnd, ](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/onColorChangeEnd.html)
[onRecentColorsChanged.](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/onRecentColorsChanged.html)

The **onChange** callbacks inform you about color selection changes the user is doing in the color picker, as they
are happening. Only the `onColorChanged` callback is required, the other callbacks can be omitted if they are 
not needed. If they are null, they will not be called.

[**onColorChanged**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/onColorChanged.html)  
A required `ValueChanged<Color>` callback, called when user selects a new color with the selected new color value.

Called every time, the color value changes via a color selection click. When operating thumbs on the color wheel, or  
transparency sliders, or entering a new character in the color code field. Changing which picker-type is viewed does not 
trigger this callback, it is not triggered until a color in the viewed picker is selected.

[**onColorChangeStart**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/onColorChangeStart.html)  
Optional `ValueChanged<Color>` callback. Called when user starts color selection with current color value, before
the new color selection is applied. When clicking a new color in color items, the color value before the selected 
new value was clicked is thus returned. It is also called with the current color, when the user starts the interaction 
on the color wheel, or the transparency slider. 

[**onColorChangeEnd**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/onColorChangeEnd.html)  
Optional `ValueChanged<Color>` callback. Called when user ends color selection with the new color value.
When clicking a new color on color items, the clicked color is returned at once, as the change ends directly after first click.
The callback's main purpose is, when it is called with the resulting color value, when the user ends the interaction on 
the color-wheel or the transparency slider, to inform us when such interaction ended. The 
`onColorChanged` and `onColorChangeEnd` will always end with the same returned
color value, but `onColorChangeEnd` only when the interaction on the wheel and sliders have ended, with only the final
result from the interaction.

If you are using a state logging solution in your application, you can use the **start** and **end**
events to get the current selected color state when the change starts. Then store the result when the
user has finished changing the color and only if the color value was different. This is useful on the wheel and 
opacity slider operations, as they will generate a lot of `onColorChanged` events while they are operated, which you 
may not want to log. If it is applicable to the use-case, then using the `showColorPickerDialog` function described
[here](#function-showcolorpickerdialog), is another way around this when logging is used. 

It is worth noticing that for keyboard color code entry, as each entry also changes the selected color interactively 
for every entered character, we cannot know when the editing is actually done. Thus, keyboard entries generate start 
and end events for every char input, just as when selecting a color by clicking on direct color items or when pasting in 
a new color.

You can use the [LIVE web example](https://rydmike.com/flexcolorpicker/#/) to observe and study the behavior of the
above callbacks when you use the picker. The demo includes trackers that show their behavior.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/FCP-22.png?raw=true" alt="Picker 22"/>

[**onRecentColorsChanged**](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/onRecentColorsChanged.html)    
Optional `ValueChanged<List<Color>>` callback that returns the current list of recently selected colors.

This optional callback is called every time a new color is added to the recent colors list with the complete current 
list of recently used colors. If the optional callback is not provided, then it is not called. You can
use this callback to save and restore the recently used colors. To initialize the list when the color picker
is created, give it a starting value via `recentColors`. This could be a list kept just in state during
the current app session, or it could have been persisted and restored from a previous session.

## Dialogs

The **FlexColorPicker** comes with two built-in dialogs. You can also make your own custom dialog by
including the `ColorPicker()` in your own dialog or overlays designs. In this chapter we will look at the two built-in
dialogs. They are really using the same dialog under the hood, but they are intended different use cases.

### ColorPicker showPickerDialog Method
API reference: [showPickerDialog](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/showPickerDialog.html)

This dialog allows you to track the ColorPicker's different **onChange** callbacks when the dialog is open, as colors are 
being manipulated, and to react to the changes as they happen. You can use this to interactively change color
properties of the application's Widgets and even its entire theme. You can see the effect of changes applied as a new color is 
selected in the dialog picker, even while dragging the wheel and sliders.

The `showPickerDialog` dialog demo in the default example app shown earlier [here](#dialog-colorpicker-method) 
explains how to use the built-in 
[ColorPicker(...).showPickerDialog](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/ColorPicker/showPickerDialog.html)
method.

The disadvantage of this dialog is that you have to maintain the state yourself. You have to store the color before you open the 
dialog, and restore this color if the dialog is canceled, instead of a color selected. The API can also be a bit 
cumbersome to use. The above example demonstrates how to do it.

### Function showColorPickerDialog 

API reference: [showColorPickerDialog](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/showColorPickerDialog.html)

The `showColorPickerDialog` function is often simpler to use. Pass in a build-context for the dialog, and the 
required start color value. Call the function with needed color picker and dialog setup properties, and 
await for it to return the selected color when the dialog is closed. 
If no color is selected, when the dialog is canceled or dismissed, then it just returns the passed in start color.

This picker might be simpler to use in many scenarios. However, it cannot use the feature where colors and 
themes can be updated in the background behind the dialog, as colors are selected in it, before the dialog is 
even closed. It also cannot return the list of recently selected colors, but you can still give it a starting 
set of recently selected colors. Potentially the callback for the recently used colors lists could be added to 
the `showColorPickerDialog`'s exposed APIs, it is however currently not exposed.

In many cases, when you just need to open a picker dialog to select a color and move on, this
version offers a simpler API for that. Under the hood, it is just a wrapper for the other version with the on change 
callbacks. It thus shares all other properties and features with the `ColorPicker`, combined with 
its `showPickerDialog` method.

The `showColorPickerDialog` dialog demo in the default example app shown [earlier](#dialog-colorpicker-function), 
explains how to use the built-in 
[ColorPicker(...).showColorPickerDialog](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/showColorPickerDialog.html) 
function.

Since the properties `elevation` and `title`, in the `showPickerDialog` method would collide with the same
named ones in the `ColorPicker`, the dialog's elevation and title in `showColorPickerDialog` are instead
called `dailogElevation` and `dialogTitle`. This is to avoid name conflicts when they are 
present in the same function.

# Desktop and Web Ready

**FlexColorPicker** works on all Flutter platforms, Android, iOS, Web, Windows, macOS and Linux.
Here is an example of the demo application running on Windows desktop.

<img src="https://github.com/rydmike/flex_color_picker/blob/master/resources/ColorPickerEnterCode.gif?raw=true" alt="ColorPicker on Windows" width="350"/>

The live [Web demo](https://rydmike.com/flexcolorpicker/) is an example of it running and being used in a Web build. 
For the major part, the color picker runs well with either
[Flutter Web renderer](https://flutter.dev/docs/development/tools/web-renderers), 
HTML or CanvasKit.

If the color picker's opacity slider feature is used on WEB builds `enableOpacity: true`, then you
may prefer build using the SKIA **canvaskit** renderer only. The opacity slider uses `ImageShader`, 
a Flutter API that is not available on **html** builds in older Flutter versions. It was not 
available not in stable version 2.2.1.

 ```
flutter run -d chrome --web-renderer canvaskit
flutter build web --web-renderer canvaskit
```

> [!NOTE]  
> **UPDATE Feb 18, 2022:** When using Flutter stable version 2.10.1, the `ImageShader` API
> seems available and working also when using --web-renderer html, build. However, if you
> run into issues with the opacity slider on web builds, prefer using canvaskit instead of auto or
> html renderer when you use the `ColorPicker` in web apps and enable the opacity slider.

The **FlexColorPicker** goes a bit further than just working on web and desktop builds. For example, pick item focusing 
behaves as can be expected. The picker supports keyboard navigation and control selection and control activation, 
especially when it is used in a dialog where other controls on the screen do not affect the intended keyboard 
navigation order. As mentioned in the API guide, if the picker is so configured, it also has keyboard shortcuts 
for copy and paste commands, that even adapt to the used desktop platform.

The wheel-picker cannot be operated with just a keyboard, it needs a mouse or touch control. It will remain so, as it
is not a design well suited for keyboard control. It is designed to require a mouse or touch-input to be operated.

The opacity slider can be operated via keyboard controls too. Future picker options may offer additional, advanced 
color picker types, designed using only sliders for selecting any custom color. This design will be able to 
use keyboard controls to define and select any color.

The currently used color picker type selection control is based on the `CupertinoSlidingSegmentedControl` widget. 
It unfortunately does not support keyboard control. A future version may include additional picker-type 
selection controls that support keyboard navigation and picker "tab" selection. When such controls are added, the
current version will remain available as default for backward compatibility.

# Additional Resources

There are more configuration options available in the `ColorPicker` than those described in the above
API guide, please use the complete [API doc reference](https://pub.dev/documentation/flex_color_picker/latest/flex_color_picker/flex_color_picker-library.html) for 
additional information.

The source code of the [live Web example](https://rydmike.com/flexcolorpicker/) is included in the package example 
folder, in "example/lib/demo". By studying it, you can see a practical example of how to use all the features
it uses. 

The live Web demo also has tooltips showing the used API behind every demonstrated interactive control. This
can be used as a quick reference to find the used APIs as you interactively try the Web example.

**Happy color picking!**