# Changelog

All notable changes to the **FlexColorPicker** package are documented in this file.

## 3.7.0

**Dec 29, 2024**

**PACKAGE**

* Updated the package to support and require at least Flutter v3.27.0.
* Fixed all new analyzer lint warnings and removed usage of all deprecated `Color` properties.
  * While the package now uses the updated `Color` class with support for wide color gamut, the color inputs and outputs are still 32-bit RGB color values. A future feature update may add support for more and new color formats.

**NEW**

* Added convenience `Color` sRGB extensions that can be used as none deprecated replacements for `alpha`, `red`, `green`, `blue` and `value` they are called `alpha8bit`, `red8bit`, `green8bit`, `blue8bit` and `value32bit`. FlexColorPicker uses them internally to avoid using the deprecated Color properties.

**KNOWN ISSUES**

* There style breaking issue on the padding around the custom opacity `Slider`. The thumb also jumps towards the center when pressed. These issues did not exist in Flutter 3.24.x and earlier versions. It seems like the issue cannot be completely solved in custom Slider implementation. The extra padding and thumb jumping towards the center seem related to `Slider` changes introduced in **Flutter 3.27.0**. Those changes were made in preparation for releasing support for the updated Material-3 slider styles. For more information, see issue https://github.com/rydmike/flex_color_picker/issues/90. A fix in Flutter SDK may be needed to solve this issue.   

## 3.6.0 

**September 25, 2024**

**NEW**

The ColorPicker got the following new properties and features:

* Boolean `showEditIconButton`, defaults to `false`.
  * Whether to show an edit icon button before the color code field. The edit icon button can be used to give users a visual que that the color code field can be edited. When set to true, the icon button is only shown when the wheel picker is active and `colorCodeReadOnly` is false. Tapping the icon button will focus the color code entry field.
  * Feature included in updated web demo app: **YES**


* IconData `editIcon`, defaults to `Icons.edit`.
  * The icon to use on the edit icon button.
  * Feature included in updated web demo app: **NO**, only default icon used.


* Boolean `focusedEditHasNoColor`, defaults to `false`.
  * Whether the color code entry field should have no color when focused. If the option, to make the color code field have the same color as the selected color is enabled via `colorCodeHasColor`, it makes it look and double like a big color indicator that shows the selected color. This can also make the edit of the color code confusing, as its color on purpose also changes as you edit and enter a new color value. If you find this behavior confusing and want to make the color code field always have no color during value entry, regardless of the selected color, then set this option to true.
  * Feature included in updated web demo app: **YES**


* Boolean `tonalPaletteFixedMinChroma`, defaults to `false`.
  * Whether the tonal palette uses a fixed minimum chroma value for all tones, or if it uses the chroma value of the selected color. Prior to version 3.6.0, the tonal palette used minimum chroma value of 48 or chroma of the selected color. This was the default primary tonal palette behavior in Flutter's ColorScheme.fromSeed method before Flutter version 3.22.0. Starting from FlexColorPicker version 3.6.0, the picker creates a HCT color space tonal palette using whatever hue and chroma the selected color has. If you for some reason want to use the old behavior, set this property to true. This will make the tonal palette use the fixed minimum chroma value of 48 for all tones.
  * Feature included in updated web demo app: **YES**

**FIX**

* Since version 3.4.0 the value of property `ColorPickerCopyPasteBehavior.editUsesParsedPaste` had no impact on the picker's paste behavior when the color code text field was focused. The color picker always behaved as if this property was true. Which incidentally is the behavior that pretty much all uses cases should use. This feature now again works as stated in its doc comments. However, the default value was changed from `false` to `true`, to match the actual default behavior it has had since version 3.4.0, and the behavior that should be preferred. The `false` setting was there to provide color code text field paste behavior backwards compatibility with versions before 2.0.0. We may deprecate this property in a future version, as it is not really recommended to use `false` at all, but for now it is fixed again.  

**TESTS**

* Improved the test coverage of the ColorPicker.

## 3.5.1

**June 28, 2024**

**CHORE**

* Update FlexSeedScheme to min version 3.0.0.
* Update example app dependencies to latest versions.

## 3.5.0

**May 15, 2024**

Requires min Flutter 3.22.0.

No new features or fixes in this release. A version bump to use FlexSeedScheme 2.0.0 compatible with Flutter version 3.22.0 and its new breaking ColorScheme.

The ColorPicker contains no breaking changes, but underlying Flutter does, and this version is only compatible with Flutter 3.22.0 and later.

**NEW**

* Added property `mainAxisSize` to `ColorPicker` and `showColorPickerDialog`, it controls the vertical axis size of the picker's column layout. Defaults to `MainAxisSize.max` as before, like `Columns` do by default. The property was added to enable setting the dialog to use `MainAxisSize.min` if needed.

**FIX**

* Fix wheel picker jumping to BW or custom picker under certain conditions.
  * When the wheel picker's opacity value is not 100, moving the color picker cursor to the white corner or bottom black edge of the color box triggers a jump. It automatically selects BW or a custom picker containing black or white values. This is now fixed. The picker cursor will stay in the wheel picker, and the color box will not jump to BW or custom picker when the cursor is moved to the white corner or bottom black edge of the color box.
* Improved and updated API documentation for `ColorPicker` properties `color` and `onColorChanged`.
* Fixed typos and language in the readme.

## 3.4.1

**Mar 16, 2024**


**FIX**

Package

- Fixed [#81](https://github.com/rydmike/flex_color_picker/issues/81) The property `tonalSubheading` in the convenience dialog function `showColorPickerDialog` was never passed along to the `ColorPicker` used to construct the dialog, causing the tonal subheading to never show up in the resulting dialog.


**New** 
 
Web demo

- There is now a color picker in the web demo app also using and demonstrating the usage of the optional convenience `showColorPickerDialog` function.  


## 3.4.0

**Mar 3, 2024**

Requires min Flutter 3.16.0 and Dart 3.0.0.
 
**NEW**

- Added enum values `filled` and `filledTonal` to `ColorPickerActionButtonType` and added support for these button styles as OK/Cancel buttons in the ColorPicker dialog. 
- Added `dialogActionOnlyOkButton` to `ColorPickerActionButtons`. Defaults to false. If set to true and `dialogActionButtons` is true, only the OK button will be shown.
- Added support for a second custom color palette to the picker. In addition to `ColorPickerType.custom` there is now also a `ColorPickerType.customSecondary` picker selector. It gets its values from `ColorPicker.customSecondaryColorSwatchesAndNames`. 
- Added support for transparent colors for both custom color palette pickers. They can now have opacity in the picker in their custom color values. This also works if the opacity and slider in `ColorPicker.enableOpacity` is not enabled. Nothing new is required to use this feature. It works automatically when custom color palettes are used that have partially transparent colors in them. 
- Added `shadowColor` and `surfaceTintColor` to the dialog properties to enable control of the shadow color and surface tint color of the color picker dialog.
- The color utilities `ColorTools.createPrimarySwatch` and `ColorTools.createAccentSwatch` now create color swatches with alpha channel value kept at its input values for all created swatch indexes. Previously they set alpha to `#FF`, even if the value might have been something else. Creating palettes with very low alpha in the source color will not produce pretty palettes, but it is now possible to create them.
- The Color picker received two new layout properties. Previously all vertical spacings between the column elements in the picker were controlled by the `ColorPicker` property `columnSpacing`. For two key elements, you can now override this spacing. 
  - Use `toolbarSpacing` to adjust the vertical spacing below the top toolbar header and its action buttons. The purpose is to enable using zero space or close to it, so the top toolbar and action buttons can be closer to the picker selection control than the rest of the spacing in the picker uses.
  - Use `shadesSpacing` to adjust the vertical spacing after the Material-2 swatch palette. By setting it to zero or one, you can create a design where the Material-2 swatch-based palette is closer to or connected to the Material-3 tonal palette. As long as the tonal palette does not use a heading, of course.
  - Both `toolbarSpacing` and `shadesSpacing` default to `columnSpacing` if they are not defined.
  - More of these vertical spacing fine-tuning properties can be added if there is a need for them.

**CHANGE**

- Dialog **OK** and **Cancel** action buttons now use the `.icon` Material button variants, when icon usage is enabled. Previously they baked in the leading icon into the button child Widget. This version follows the Material design spec exactly. The visual change is minor, but it does look better now when icons are used.
- Recent colors now also capture the opacity of a selected color as a different color, it does this also when you change opacity. Selecting a color with opacity in the recent colors list will set the picker's opacity to the opacity the color in the recent colors list has.

**FIX**

Package
- Replaced APIs deprecated in Flutter 3.19.0. Replaced internally used deprecated APIs `RawKeyboardListener`, `RawKeyEvent`, `RawKeyDownEvent`, `RawKeyEventDataMacOs`, `RawKeyEventDataIos` with `Shortcut` APIs.
- When using custom transitions the `InheritedTheme.capture ` should use `actionButtons.useRootNavigator` value and not default it to true. Fixed.

Web demo 
- Reset to defaults did not reset settings for `wheelSquarePadding` and `wheelSquareBorderRadius`. Fixed.


## 3.3.1

**January 21, 2024**

- FIX: Fixed issue [#71 _activeColorSwatchList init in Wheel with tonal palette case](https://github.com/rydmike/flex_color_picker/issues/71).
- CHORE: Bump FlexSeedScheme to version 1.4.0.
- TEST: Improved test coverage from 65% to 74%.

## 3.3.0

**July 18, 2023**

**NEW**

- Use `ColorPicker.tonalColorSameSize` set to true, to make the Material-3 HCT tonal palette color indicators use the same size as the size defined for the other color indicators. Previously and by default, the tonal color indicators are smaller to make the palette width match the width of the Material-2 swatch color palette, that has fewer colors.

**FIX**

- Fixed issue [#67 Inner circle does not move](https://github.com/rydmike/flex_color_picker/issues/67).
  - When clicking on the color wheels square color box part inside the Hue circle, the click moved the selection on wheel when clicking close to the square edge. This is now fixed. The fix also introduces exact wheel tap/drag to start an operation of Hue wheel. Previously, the Hue wheel would start operating when taping or dragging on the square containing the Hue wheel, but outside the squared color area inside it. Now to start dragging or make a tap action, it must start on the Hue wheel. Dragging around outside it or inside it, once a drag operation has started, works as before.  

- Fixed issue [#66 White color selects multiple colors](https://github.com/rydmike/flex_color_picker/issues/66).
  - Part of original design with the picker was to only have a given color value appear in one color palette. When adding custom color palettes or using tonal palettes, the same color values may appear in multiple palettes. Selecting such a color value would highlight all the palettes the color appears in. Tonal palettes always contain white and black colors, so it is particularly problematic when using them. This fix prevents showing the main color as selected in multiple palettes and avoids switching Material swatch palette when operating on a tonal palettes. As a part of this FIX, main Material swatch shade color index 500 or Material accent swatch shade color index 200, is only shown as selected when its color is actually selected in a Material swatch or Material tonal color tone.

## 3.2.2

**May 11, 2023**

- Updated to use minimum `flex_seed_scheme ^1.3.0`. This version, no longer depends on `material_color_utilities`, thus avoiding all version issues and conflicts when Flutter changes what breaking version of `material_color_utilities` it uses on different channels and versions.
- Tested package with Flutter 3.10 and rebuilt web demo example with the new Flutter release.


## 3.2.1

**Apr 16, 2023**

- Changed to using `flex_seed_scheme: ^1.2.4` that depends on `material_color_utilities` with version constraint set to `>=0.2.0 <0.4.0` from `^0.2.0`.
  - This change enables the package to be used on current Flutter **stable** 3.7 versions, as well as the latest 3.10.x versions on channels **beta** and **master**. It will also work with the next stable Flutter release after 3.7.
- Updated default example to use Material 3.


## 3.2.0

**Apr 2, 2023**

**NEW**

* Based on user request, exposed widget `ColorCodeField` as a part of the package's public API. It can now be used externally as well. The `ColorCodeField` is the color code entry and display field used by the `ColorPicker`. 

## 3.1.0

**Feb 1, 2023**

**CHANGE**

* Requires minimum Flutter 3.7.0 and Dart 2.19.0 that Flutter 3.7.0 uses. Version 3.7.0 of Flutter broke the nullable `Overlay.of` API. The new API is `Overlay.maybeOf`. This forced a new release of **FlexColorPicker** that requires minimum Flutter 3.7 that breaks compatibility with older versions of Flutter.

**FIX**

* Dart format and analyzer updates for Flutter 3.7.0.
* Add example screenshots to pubspec.yaml.

## 3.0.2

**Jan 13, 2023**

**FIX**
 
* Fixed the color picker item size Slider in the Web demo app. No changes to the package.

## 3.0.1

**Jan 12, 2023**

**FIX**

* The `onColorChanged` was called twice if just clicking on the wheel color picker's wheel or square to set a new color value via a single click. This fixes it, and such clicks now only generate one `onColorChanged` call-back. Dragging on the wheel and square still generate `onColorChanged` call-backs during the entire drag process. To get callbacks just at start or end of drags, use `onColorChangeStart` and `onColorChangeEnd` as before. 

## 3.0.0

**Nov 23, 2022**

**BREAKING - STYLE**

* The color picker dialog `actionsPadding` now default to null. This results in that if it is undefined, its value is determined by the ambient `AlertDialogTheme`, or if it is not defined either, the default for `AlertDialog`. It has different defaults depending on if Material 2 or Material 3 is used. Default value in previous versions of **FlexColorPicker** was: `EdgeInsets.symmetric(horizontal: 16)`
* The color picker dialog `buttonPadding` now default to null. This results in that if it is undefined, its value is determined by the ambient `AlertDialogTheme`, or if it is not defined either, the default for `AlertDialog`. It has different defaults depending on if Material 2 or Material 3 is used. Default value in previous versions of **FlexColorPicker** was: `EdgeInsets.all(16)`

* The API usage of the above properties is unchanged. It is only the default behavior that has been updated to be less opinionated and to enable using theme-dependent settings.

**BREAKING - REMOVED**

* Removed in version 2.1.0 no longer used and already deprecated parameter `useRootNavigator` in `ColorPicker` method `showPickerDialog`. 
* Removed in version 2.1.0 no longer used and already deprecated parameter `useRootNavigator` in function `showColorPickerDialog`.

**NEW**

* To `ColorPicker` method `showPickerDialog` and to function `showColorPickerDialog`, added parameters `barrierLabel` and `anchorPoint` as pass along values to Flutter SDK `showDialog` and `showGeneralDialog`.

* To `ColorPicker` method `showPickerDialog` and to function `showColorPickerDialog` added parameters `transitionBuilder` and `transitionDuration`. If `transitionBuilder` is not null, the `showPickerDialog` and `showColorPickerDialog` will use the `showGeneralDialog` Flutter SDK function instead of `showDialog`. The `showGeneralDialog` function will be used with the provided `transitionBuilder` and `transitionDuration`. The `transitionDuration` only has any impact when the `transitionBuilder` is used. If `transitionBuilder` is null, then the `showPickerDialog` and `showColorPickerDialog` use the Flutter SDK `showDialog` implementation as before, thus using the default Material platform dependent `showDialog` transition and duration. 

**EXAMPLES**

* Default example: Added an example of how to use the `transitionBuilder`.
* Web example: Modernized its theme by using Material 3 and a seed generated `ColorScheme`.


## 2.6.1

**Sep 9, 2022**

* Add `secondaryOffset` to `OpacitySliderTrack` `paint` method override to **fix** new requirement 
  for master channel compatibility, works with the stable channel too. Thanks, 
  [Dan Reynolds](https://github.com/danReynolds) for the PR.

## 2.6.0

**Aug 30, 2022**

* Contains all updates from 2.6.0-dev, dev2 and dev3.
* Updated minimum dependencies to Dart >=2.18.0 and Flutter >= 3.3.0.

## 2.6.0-dev.3

**August 28, 2022**

**CHANGE**

* This is a dev release that works with Flutter beta 3.3.0-0.5.pre and master channel.
  It has more relaxed constraints than 2.6.0-dev.2.

* This version no longer depends directly on package `material_color_utilities` it uses
  `flex_seed_scheme` instead, with a transitive dependency on `material_color_utilities`.

* Changed all used `TextTheme` style names to M3 versions, including docs. 

## 2.6.0-dev.2

**August 21, 2022**

**CHANGE**

* This is a dev release for those that need to work with both stable and master channel, where 
  Flutter master 
  SDK depends on material_color_utilities 0.2.0 and 3.3.0 beta, pre for upcoming Flutter 3.3.0 
  stable, use material_color_utilities 0.1.5. It uses a controversial package constraint of:
  `material_color_utilities: '>=0.1.5 <=0.2.0'`. Using older versions 0.1.3 and 0.1.4 in theory 
  also works, but they contain some breaking color values in the used algorithm for calculation of
  tonal palettes. The color changes are very minor and typically not visible to the eye.

* This dev release also disabled two trivial tests that contained incompatible results between 
  Flutter 3.0.5 stable, 3.3.0-0.4.pre beta and 3.1.0-x master.

## 2.6.0-dev.1 

**August 5, 2022**

**CHANGE**

* This is a dev release for those that need to work with the master channel, where Flutter SDK 
  depends on material_color_utilities ^0.2.0.

* Updated material_color_utilities to ^0.2.0. This version constraint does not
  work with Flutter 3.0.x stable or beta 3.3.x, and their earlier versions.
  This dev release is required to use Flutter SDK **master** `3.1.0-0.0.pre.2111` or later,
  that uses material_color_utilities 0.2.0.  

* For other (older) versions of Flutter SDK, you can use package version 2.5.0 that has a 
  material_color_utilities version constraint of ^0.1.3.

* This release also updates Dart SDK constraint to `'>=2.17.0 <3.0.0'` and has Flutter listed as `'>=3.1.0-0.0.pre.2111'`.  

**DOCS**

* Harmonized the changelog style and its history. The new style and how it looks will be tested
  with a dev release to ensure it works well on pub.

## 2.5.0

**April 21, 2022**

**NEW**

* Added new features to add padding between the wheel-picker's shade square and hue wheel,
  and to adjust the border radius on the shade square.
  Addresses enhancement request [#47 "Square padding"](https://github.com/rydmike/flex_color_picker/issues/47).
  The new features are available via `ColorPicker` properties `wheelSquarePadding` and `wheelSquareBorderRadius`.

## 2.4.0

**April 15, 2022**

**FIX**

 * Fixes [issue #44](https://github.com/rydmike/flex_color_picker/issues/44) "High wheelWidth cause wrong cursor position in the ColorPicker"

**NEW**

* The order of the action buttons Cancel - OK on the bottom of the built-in
  dialog can be changed to OK - Cancel. come in three flavors controlled by enum
  `ColorPickerActionButtonOrder` having values:
  - `okIsRight` this is the default, to no break past behavior.
  - `okIsLeft`
  - `adaptive` order depends on the used platform. Windows uses `okIsLeft` others
    `okIsRight`.

  The feature is enabled via the `ColorPickerActionButtons` configuration
  and its new property `dialogActionOrder`.

* By default, the color picker tries to set focus to its own internal widgets when it is
  created. It does this when either [ctrlC] or [ctrlV] are enabled in
  order for the keyboard listener to be able to react to copy-paste events
  even if no control on the widget has been focused yet.
  If you need another widget to retain focus, e.g., if the picker is used on a
  surface/scope shared with other widgets and not in its own dialog, then
  setting [autoFocus] to false might help.

  If both [ctrlC] and [ctrlV] are false, the picker yields the focus the
  same way as setting [autoFocus] false, but then you have no keyboard-shortcut
  copy-paste functions at all. With [autoFocus] false, you can still use
  keyboard copy-paste shortcuts and yield the focus from the picker.
  When you do this, the copy-paste keyboard shortcuts will not work until
  one of the picker's components is focused by interacting with any of them.

  The picker still grabs focus when you click on its background. This is used as a way
  to set focus to keyboard listener to enable copy-paste keyboard shortcuts
  or when you operate any of its controls, the control in question
  always gains focus.

  You can now turn OFF the autofocus used by the keyboard listener by setting
  `autoFocus` to false in `ColorPickerCopyPasteBehavior`.

  This new feature can potentially also be used to address [issue #33](https://github.com/rydmike/flex_color_picker/issues/33).


**CHANGE**

* The generated Material Color swatch you get when you click on any color in the
  wheel picker has been updated and is a bit improved. It is still not the
  actual M2 `MaterialColor` swatch algorithm, like the Tonal Palette is when it
  comes to Material 3. It uses the actual seed algorithm for the primary
  tonal palette you get with the selected color as input. The wheel detects when
  you select any Material 2 swatch color and shows its swatch then.
  For other colors, it computes a `MaterialColor` swatch. This swatch
  is still not using the correct algorithm, but it is a bit better looking
  than before.

  There is currently no know Dart implementation of this algorithm, if there
  were it would be in use here. There are some versions in JS of the algorithm
  that have been reverse-engineered from the Material 2 design guide website.
  If someone wants to make a Dart version, that would be fabulous. Links and more
  information can be found in `ColorTools.createPrimarySwatch`

**EXAMPLES**

  The web demo app has been updated to demonstrate above new features.

## 2.3.1

**March 3, 2022**

**FIX**

* Fix for nullable/none-nullable difference for Flutter `IconButton` between Flutter
  version 2.10.0 and earlier versions Flutter 2.8.1, where `iconSize` is nullable in
  Flutter 2.10.x, but not in Flutter 2.8.1. See issues [report #40](https://github.com/rydmike/flex_color_picker/issues/40) and [PR #41](https://github.com/rydmike/flex_color_picker/pull/41).


## 2.3.0

**February 18, 2022**

**NEW**

* Added capability to show a Material 3 tonal-palette as per
  [Material 3 design specification](https://m3.material.io/styles/color/the-color-system/key-colors-tones).

* To enable it set new `ColorPicker` property `enableTonalPalette` to true.
  It is false by default. Like the Material Swatch shades heading that
  that has an optional `subHeading` widget, when tonal palette is enabled
  you can show an optional `tonalSubheading` widget above it.

  - When you click/select a color in the color picker, and tonal palette is
  enabled, a 13-shade Material 3 tonal-palette for the selected color will be
  generated. It always starts with black, tone 0 for the used seed color and
  ends in white, tone 100.

  - The official Material 3 Dart library is used to create the tonal palette
  from any selected color. The color you select functions a seed color to
  generate the tonal palette and might not be included itself and selected in
  the palette. You can click on any color in the generated palette to
  select and pick a color.

  - Selecting a color in the tonal palette, only selects the color in the palette. 
   It does not update the palette. Only when you select a color from the other
   color sources in the picker, is that color used as key color, to seed and generate
   an updated color palette for the selected color.


**CHANGE**

* The WEB example was updated to include enabling and disabling
  the tonal palette and built it with the Flutter version stable 2.10.1.
* All dependencies in the Web demo were updated to their latest version.

  The Web demo example requires at least Flutter 2.10.0 to be built.
  It uses ColorScheme properties in its theme that were not available
  earlier and removed in 2.10.0 deprecated color properties from its theme.
  The color picker package itself still has the same version requirement as before
  of Dart SDK: `'>=2.14.0 < 3.0.0'`.

## 2.2.0

**November 17, 2021**

* Fixed the style for color entry field, to always use the intended fixed stadium style.
* Updated dependencies for the web demo, big change was Riverpod to use v1.0.0.
* Lint rule updates.
* Bump Dart SDK requirement to 2.14.
* Build and publish the WEB demo with the updated version using Flutter 2.5.3.

## 2.1.2

**July 16, 2021**

**CHANGE**

* Improved performance by splitting wheel painting into
  multiple painters and introducing `RepaintBoundary` widgets around
  expensive painters to avoid unnecessary repaints. Thank you,
  [Krista Koivisto](https://github.com/krista-koivisto) for this excellent contribution!

## 2.1.1

**July 2, 2021**
 
* Documentation fix.

## 2.1.0

**July 2, 2021**

* **Fix:** The `useRootNavigator` argument is now respected on all Navigator
  `pop` functions used in the `ColorPicker` widget itself and by
  built-in dialogs used by the `ColorPicker`. To support this,
  the current `useRootNavigator` property in the `ColorPicker.showPickerDialog()` and
  in the function `showColorPickerDialog` had to be deprecated.

  The property has moved to become a configuration option in `ColorPickerActionButtons`
  class to make it accessible to the Navigator pop functions both in
  the `ColorPicker` widget itself, as well as to built-in dialogs.

  The default behavior has not changed, the setting still defaults to using
  dialogs that use the root navigator, but now the pop functions work as intended.
  If you for some reason have used none root navigators for the built-in
  dialogs in previous versions, you need to set
  `ColorPickerActionButtons(useRootNavigator: false)` and pass it to
  `ColorPicker(actionButtons)` or `showColorPickerDialog(actionButtons)`.
* **Tests:** Started adding more tests and coverage report.
    Total 5668 tests, coverage 65.36%.
* Documentation and typo updates.

## 2.0.2

**June 11, 2021**

* **Improvement:** Performance slightly improved via an additional rebuild check.
* **New feature:** ColorTools got a new static function `swatchContainsColor`.
* **New feature:** Set property `secondaryOnDesktopLongOnDeviceAndWeb` to `true` (defaults to false) in
  ColorPickerCopyPasteBehavior, to enable using long press in the color picker, to open up the COPY-PASTE
  context menu on Web, iOS and Android touch devices. While using secondary mouse button
  on desktop platforms Windows, Mac and Linux, but not if it is a desktop web app.
* **Documentation:** Fixed broken API reference links in the API guide chapter. Mentioned that WEB build
  requires a canvas kit build if `enableOpacity` feature is used.
* **Web example:** The live web example got updated to use the latest Flutter stable embedder.
* **CI/CD:** Tried the CI/CD deployment with --base-href="/flexcolorpicker/" instead of `repl`. Did not
  work, continuing with `repl` for now.

## 2.0.1

**April 10, 2021**

* **New feature:** Enabled updating the color picker externally. Set the `color` property of the widget to a new value to update it. You can even "remote control" the color picker by updating the `color`, if so needed.

  This is mostly a potential use-case for desktop and web, when the picker is not used in a dialog.
  You can use this on a phone or tablet too, but often there is not enough space to keep the picker
  visible on the main surface this way on mobile devices. However, on desktops it is certainly a valid use
  case that should be supported. It was previously not supported by design, but as we are going to support 
  web/desktop use-cases, it should certainly be supported. This update adds support for it. The picker only
  updates if the externally provided `color` constructor property differs from its internally kept color
  state. Finding the right picker, computing its swatches, is a bit demanding, but it seems to work fluidly,
  even when remote-controlling the wheel and sliders interactively.

* **Web example**: Updated the Web example to also show the "remote control" of the on-screen color picker. A
  remote control widget with a few color boxes, that you can click on to update its colors externally was added.
  The demo even goes meta! You can use a modal dialog version of the ColorPicker, to control the ColorPicker
  on the screen in the card, from the dialog ColorPicker! Maybe not as such so useful, but an interesting demo.

## 2.0.0

**April 9, 2021**

* This release only contains documentation updates from pre-release **2.0.0-nullsafety.5**
* Thi is the first stable release of the null-safe version
* This is a **MAJOR** new feature release, in addition to the null-safety conversion.
  Please see changelogs from 2.0.0-nullsafety.0 to nullsafety.5, for a complete list of changes and new features.
* To get familiar with version 2.0.0 and all its new features, it is recommended to go through the updated tutorial,
  and the API guide in the readme file.
* For convenience, the list of breaking changes from the previous stable version 1.1.5 is shown below.


**BREAKING**

In addition to breaking changes as a result of the null-safety implementation, this release contains a few other
**minor breaking changes** from version 1.x, they mostly concern visual nuances and label defaults.

* The `colorCodeIcon` has been deprecated and no longer has any function. To modify the copy icon on the color
  code entry field, define the `ColorPickerCopyPasteBehavior(copyIcon: myIcon)` and provide it to the
  `copyPasteBehavior` property, it defaults to same icon as in versions 1.x.
* The bottom dialog action button that selects the color now says **OK** instead of **Select**. The label for the OK
  button by default comes from a Material localization. You can as before change it to whatever string you want.
* The dialog bottom action button for **OK** by default now uses a plain `TextButton` and
  not an `OutlinedButton`. This change is done to conform to a less opinionated default style. You can still
  manually configure it to use an `OutlinedButton` instead as before. Now you can choose, before there was
  no choice.
* The dialog bottom **OK** button is no longer autofocused.
* The extension `FlexPickerNoNullStringExtensions` on none nullable
  `String` named `toColor`, no longer returns color value `Color(0x00000000)` for colors that cannot be parsed
  to a Color. It now returns `Color(0xFF000000)`. This is because the Flutter SDK dislikes the fully transparent
  black `Color(0x00000000)`, if it is fully opaque black, it works better as a fallback safety color.
  The `FlexPickerNullableStringExtensions` on `String?` named `toColorMaybeNull` works as before by returning
  null when the `String?` cannot be parsed to a `Color`.
* The color code edit and entry field now work more like a normal text entry field. It still
  only accepts valid hex input and converts all inputs to uppercase.

## 2.0.0-nullsafety.5

**April 8, 2021**

* **Fix:** Setting `borderColor` did not change the border color on the wheel when `wheelHasBorder` was true.
* **New features:** The `showPickerDialog` method now exposes most (= not directly controlled) properties of the underlying `AlertDialog` used to make the dialog, this includes e.g., the `backgroundColor`, `elevation`, `clipBehavior` and `shape` as new exposed properties that may be useful.
* **New feature:** Added a new alternative color picker dialog function `showColorPickerDialog` that returns a `Future<Color>` which when the dialog is closed, returns the selected color from the dialog or original start color value, if no selection was made. This picker might be simpler to use in some scenarios. However, it does not allow for the feature where colors and theme's can update in the background behind the dialog, as colors are selected in it, before it is even closed. However, if you just need to open a dialog, select a color and move on, this version offers a simpler API for that. Under the hood it is just a wrapper for the previous more capable version with the onChange callbacks. It shares all other properties and features with the `ColorPicker`, combined with its `showPickerDialog` method, except all the **onChanged** callbacks that are excluded. Since the properties `elevation` and `title` in the `showPickerDialog` method, would collide with the same named properties in `ColorPicker`. The dialog's elevation and title in the `showColorPickerDialog` are instead called `dialogElevation` and `dialogTitle` in it.

* **Improvement:** Performance was improved via more optimized rebuilds.
* **Documentation:** The first version of updated documentation with API guide documentation is now included. It still requires proofreading before stable release, but getting close to being ready for release now.
* **Default example:** The default example got a new picker that shows how the new `showColorPickerDialog` functions.
* **Web example:** The Web example, with the built-in API tooltips guides, got a major rewrite. It was originally not intended to be as large as it grew to be, but since it grew so much it needed a rewrite. 
  * It now uses Riverpod to make its simple state management needs easy to handle and much cleaner than before. It also includes persisting the settings directly as settings are changed in the app. Persistence is implemented with Hive. It should work on all Flutter platforms as well, but it has only been tested on Android, Web and Windows.
  * As an experiment, only RiverPod StateProviders were used. While the setup is a bit tedious, it enables the desired fine-grained control over rebuilds of all the used setting control widgets. Each setting is also stored as an individual key-value pair in the used Hive box. A ProviderObserver that observes changes in the StateProviders we want to persist is used to save any state change to the used Hive box, regardless of where the state is changed in the demo app. 
  * This setup was an experiment to see if it might work and provide some simplification benefits. At least in this case, it did. It is also a pretty interesting and simple solution. The default start values are also defined via the Riverpod StateProvider's default values, that also use their const Hive string key as their provider name. Each StateProvider gets its start setting value from the Hive box with the same key. If the key does not exist yet in Hive, it falls back to a default value from a const Map using the same string const as its key, for the default fallback value. Reset back to default values is also done by setting all providers' state back to their default values as defined by the same const fallback value map.

## 2.0.0-nullsafety.4

**March 22, 2021**

* **New feature:** A bool `enableOpacity` property was added that enables an opacity
  slider that can be used to control the alpha channel in the selected ARGB color value. The slider
  height can be controlled with `opacityTrackHeight`, the width with `opacityTrackWidth` and the
  slider thumb size with `opacityThumbRadius`. There is also a `opacitySubheading` Widget that can
  be used to provide a Widget heading for the opacity slider.

## 2.0.0-nullsafety.3

**March 12, 2021**

* **Fix:** Color code field no longer receives focus when switching to it on the wheel page.
  Focus is set to color wheel, or the selected color shade if shade colors are present.
  The focus handling has also been improved for desktop usage.
* **Fix:** The property `editUsesParsedPaste` now works as intended, if true, desktop keyboard paste commands,
  while editing a color value are intercepted, and the hole pasted buffer value gets parsed, it does not get
  pasted into the field. For normal field paste functionality keep `editUsesParsedPaste` false (default).
* **Minor breaking:** The color code edit and entry field now work more like a normal text entry field. It still
  only accepts valid hex input and converts all inputs to uppercase.
* **New property:** If `colorCodeHasColor` is true, then the background of the color code entry field uses the current
  selected color.
* **New property** If `colorCodeReadOnly` the color code entry field is always read-only. Normally, color code can
  be edited on the wheel picker, set this to true to make it read only there as well. Copy/paste operations still work
  if they are enabled even if the color code field entry is in read-only mode.
* **New feature:** The `copyPasteBehavior` property received three new features and properties:
   * The copy/paste context menu can now also optionally use secondary, typically mouse right, click by setting
     `secondaryMenu` to true.
   *  It also has a mode where long press will be used on iOS/Android, but secondary mouse click will be
      used on desktop/web, by setting `secondaryOnDesktopLongOnDevice` to true.
   *  When `parseShortHexCode` is true the hex color code paste action and field entry parser,
      interpret short three character web hex color codes like in CSS.
* **New extension:** The extension `FlexPickerNoNullStringExtensions` on `String` got a new
  extension function `Color toColorShort(bool enableShortRGB)`.
* **New extension:** The extension `FlexPickerNullableStringExtensions` on `String?` got a new
  extension function `Color? toColorShortMaybeNull(bool enableShortRGB)`.
* **Minor breaking:** The extension `FlexPickerNoNullStringExtensions` on none nullable
  `String` named `toColor`, no longer returns color value `Color(0x00000000)` for colors that cannot be parsed
  to a Color. It now returns `Color(0xFF000000)`. This is because the Flutter SDK dislikes the fully transparent
  black `Color(0x00000000)`, if it is fully opaque black, it works better as a fallback safety color.
  The `FlexPickerNullableStringExtensions` on `String?` named `toColorMaybeNull` works as before by returning
  null when the `String?` cannot be parsed to a `Color`.
* **Tests:** Added unit tests for `ColorPickerActionButtonType` and `ColorPickerCopyPasteBehavior`.

*See API documentation for more information.*

## 2.0.0-nullsafety.2

**March 3, 2021**

* Documentation and live Web demo link fixes.

## 2.0.0-nullsafety.1

**March 3, 2021**

There are many new features included in this version 2 pre-release. The new features can be explored with the
[live Web example](https://rydmike.com/flexcolorpicker/). Its source code is also included in the package
example folder, in "example/lib/demo/main.dart".

* **Improvement:** The wheel picker now moves on pointer-down to point location, it no longer 
  requires a slight movement for its thumbs to move to the selected start tracking point.
* **Improvements:** Keyboard traversal of the colors and selecting indicator colors with the keyboard using enter or space key. The wheel can however still not be operated with a keyboard, only touch and mouse controlled.
* **New property:** `onColorChangeStart` called when user starts color selection with current color before the change. 
* **New property:** `onColorChangeEnd` called when user ends color selection with the new color value.
* **New property:** `selectedPickerTypeColor` the color of the thumb on the slider that shows the selected picker. Ported from none null-safe version 1.1.4, does not exist in version 2.0.0-nullsafety.0.
* **New property:** `colorCodePrefixStyle` defines the text style of the prefix for the color code.
  If not defined it defaults to same style as `colorCodeTextStyle`.
  Ported from none null-safe version 1.1.4, does not exist in version 2.0.0-nullsafety.0.
* **New property:** `title` is a Widget used as an app bar type of title widget above the heading. Can also include copy, paste, select-close and cancel-cancel icon buttons when the picker is used as a dialog.
* **New feature:** There is an `actionButtons` property that takes an `ColorPickerActionButtons()`. It is used to define what type of **Ok** and **Cancel** action buttons the color picker has when used in a dialog. It is possible to define if bottom action buttons should be `TextButton`, `OutlinedButton` or `ElevatedButton` per button. If not defined, the labels on the buttons come from Material localizations, not from hard-coded default values. See breaking label for the 'Select' label. There are optional select/OK and cancel icon buttons that can be used in the title bar for a more compact dialog.
* **New feature**: There is a `copyPasteBehavior` property that takes an `ColorPickerCopyPasteBehavior()`.
  It is used to define the copy/paste behavior of the color picker, including:
    * Keyboard shortcuts: CTRL-C, CMD-C, CTRL-V, CMD-V
    * Top toolbar copy-paste buttons.
    * Long press copy-paste menu.

  All copy/paste behaviors are optional and can be enabled based on what is needed.

  For the copy format, the desired resulting RGB color string format can be configured to use #RRGGBB RRGGBB #AARRGGBB AARRGGBB and 0xAARRGGBB (default) options. The selected copy format is indicated with the corresponding prefix in the color code display/edit field when it is enabled.

  Paste supports parsing multiple RGB color string formats. It automatically detects what format is used and auto parses to correct Flutter/Dart color value. You can, for example, paste string formatted as #RRGGBB RRGGBB #AARRGGBB AARRGGBB #RGB RGB or 0xAARRGGBB, partial color string values also work. You can also activate a snack bar that informs the users if they paste color strings in an unsupported RGB string format into the color picker.

  *See API documentation for more information.*

* **New feature**: The picker can display recently used colors in a list of color indicators at the bottom of the picker. You can use the following properties to control it.
    * `showRecentColors` set to true/false to enable/disable the usage of the recent colors feature.
    * `recentColorsSubheading` subheading widget for the recently used colors. Typically, a Text widget, e.g., `Text('Recent colors')`. If not provided, there is no sub heading for the recently used colors.
    * `maxRecentColors` number of recent colors to track, from 2 to 20 allowed.
    * `recentColors` a list with current recent color, defaults to empty. You can store the last list and use this list to restore the previous recent colors list.
    * `onRecentColorsChanged` optional value callback that returns a copy the current list of recently used colors. Use it to store a copy of the recent colors to be able to restore it later.

 *See API documentation for more information.*

**BREAKING** 

The following are **minor breaking changes** from version 1.1.5, they mostly concern visual nuances and label defaults.

* The `colorCodeIcon` has been deprecated and no longer has any function. To modify the copy icon on the color code entry field, define the `ColorPickerCopyPasteBehavior(copyIcon: myIcon)` and provide it to the `copyPasteBehavior` property, it defaults to same icon as in version 1.1.5.
* The bottom dialog action button that selects the color now says **OK** instead of **Select**. The label for the OK button by default comes from a Material localization. You can as before change it to whatever string you want.
* The dialog bottom action button for **OK** by default now uses just a plain `TextButton` and not an `OutlinedButton`, this change is done to conform to a less opinionated default style. You can still manually configure it to use an `OutlinedButton` instead as before. Now you can choose, before there was no choice.
* The dialog bottom **OK** button is no longer autofocused.

## 2.0.0-nullsafety.0

**February 15, 2021**

* First version with null safety.
* A workaround to issue [#71687](https://github.com/flutter/flutter/issues/71687) was introduced. The issue has not been solved. However, the workaround allows for the Wrap implementation, that was changed to a Row in version 1.1.2, to be used again.
* The almost full API-configurable Web demo is included in the package in "example/lib/demo/main.dart" together with the previous default example in `example/lib/main.dart`. Previously, this Web example was in a separate GitHub repository. The example was updated to make it responsive, to offer better usability on Web builds.

## 1.1.5

**March 3, 2021**

* **Fix:** When `selectedPickerTypeColor` color was undefined, the thumb did not receive the same text color as the default and only one before in version 1.1.3 and earlier, in dark-mode. This broke compatibility with past style when using dark-mode. This fix restores the correct past style when the `selectedPickerTypeColor` is undefined.

## 1.1.4

**March 3, 2021**

* **Feature:** New property `selectedPickerTypeColor`: Defines the color of the thumb on the slider that shows the selected picker.
* **Feature:** New property `colorCodePrefixStyle`: Defines the text style of the prefix for the color code. If not defined it defaults to same style as `colorCodeTextStyle`.

## 1.1.3

**December 22, 2020**

* **Fix:** Faulty documentation and comment for showPickerDialog parameter insetPadding.
* **Fix:** Faulty default value for showPickerDialog parameter insetPadding, the new default
  value is the same as Flutter and Material default
  `EdgeInsets.symmetric(horizontal: 40.0, vertical: 24.0)`, as it should have been.
* **Documentation:** Minor documentation style correction.

## 1.1.2

**December 5, 2020**

* Temporary: The Wrap implementation for showing the color code and integer value was changed to a Row due to a regression in Flutter SDK causing a crash issue on channels dev and master when showing the ColorPicker in a Dialog. For more info see here: https://github.com/flutter/flutter/issues/71687 
  * When the issue is resolved, the implementation will be reverted to Wrap again. Using a Wrap has the benefit of breaking the color code display+input field and the rarely used int value, into two rows in case a large font is used in a narrow view. The Row may overflow in some rare cases. If you do not plan to use the ColorPicker with channels and versions affected by the issue, you can still use the previous version 1.1.1 to keep using the Wrap implementation if you need it. With normal styling, it is typically unnecessary.
* Fixed that the provided `TextStyle` via property `colorCodeTextStyle` was not also applied to the shown color integer value when `showColorValue` was set to `true`, as stated in API doc and intended.

## 1.1.1

**November 11, 2020**

* Updated the example app and documentation. The update includes updated screenshots and updated animated GIFs.
* Unit tests for ColorTools added. Widget tests are still pending for later updates.

## 1.1.0

**November 6, 2020**

* New API: Added `showColorValue` to optionally display the int value of the selected color. This can be used to support developers when they need to see or copy selected color values as int numbers.
* New APIs: Exposed previously missing static color names in the API for all the accent and B&W color names in `ColorTools`. All the color name values default to English color names, but can now be changed to translated strings to provide Material color names in other languages as well.
* Updated the live Web demo to demonstrate the `showColorValue` property.
* Example and documentation updated.

## 1.0.0

**November 5, 2020**

* First official release.
* Example and documentation updated.
* Updated the live Web demo version to use the released package.
* New API: Added `shouldUpdate` to the color-wheel picker, as a fix for an issue where black selection changed hue to red. This is a lower level API. You do not need to use it unless you make your own picker from scratch, and you want to use the wheel picker in your own picker.
* Final API name tweaks before version 1.0.0 release:
* Renamed: API `createPrimaryColor` -> `createPrimarySwatch`
* Renamed: API `createAccentColor` -> `createAccentSwatch`
* Renamed: API `colorNameAndHexCode` -> `materialNameAndCode`
* Renamed: API `colorName` -> `materialName`
* Renamed: API `colorHexCode` -> `colorCode`

## 1.0.0-dev.5

**November 5, 2020**

* Added a feature on the wheel color picker that enables entry of a hex RGB value to select a color.
* API changes to support separate display of Material color name `showMaterialName` and selected color code `showColorCode`, plus defining their text styles `materialNameTextStyle` and `colorCodeTextStyle`.
* New API `showColorName` to display an English color name for any selected color, not just the Material color names or custom named color swatches. It has text style that can be defined as well `colorNameTextStyle`.
* New API `colorCodeIcon` that exposes the color code copy icon, so it can be customized.
* New API `enableTooltips` to enable current and future tooltips used in the picker. Currently, only the copy color code button has a tooltip.
* A new method introduced in ColorTools called `nameThatColor(Color color)`. It returns a name for any color passed to it. Only supports English names. Based on a Dart port of http://chir.ag/projects/ntc, it contains 1566 colors and their names. It matches the given color to the closest similar color in the list and returns its name.
* Example and documentation updated.

## 1.0.0-dev.4

**November 2, 2020**

* Update to try to get the images to show up on pub.dev.
* Minor documentation corrections.

## 1.0.0-dev.3

**November 2, 2020**

* Significant API name changes and cleanup. Decided to implement previously planned changes before the official release.

## 1.0.0-dev.2

**October 30, 2020**

* First development pre-release on pub.dev.

---

# Planned Updates and New Features

These are the topics I currently have on the TODO list for this package. Do you have a new suggestion and idea? Feel free to open a [suggestion or issue](https://github.com/rydmike/flex_color_picker/issues) in the repo.

- [ ] Additional controls for selecting active picker, maybe a custom slider, ToggleButtons and probably also a compact dropdown.
- [ ] Add one more color picker type _advanced_, using sliders as controls for the other formats. 
- [ ] Add support for other color formats than RGB, HSL, HSV, CMYK, M3-HCT.
- [ ] Add support for a pipette tool to pick colors from the screen.
- [ ] Add possibility to in picker add selected colors to a custom picker.
- [ ] Reactor the code to prepare for making a major new version 4.0.0. 
- [x] Add more tests. Done. Now at 84%, pretty OK now, but even more tests are always welcome.
- [x] Release the stable version 2.0.0
- [x] Add GitHub actions for test, analyze, coverage, build and web demo deployment.
- [x] Add a simpler optional async dialog picker function that returns selected color.
- [x] Add support for colors with opacity or alpha.
- [x] Improve copy/paste feature.
- [x] Version 2.0.0-nullsafety.0: Add null safe version.
- [x] Version 1.1.1: Add first tests of the ColorPicker, so far only unit tests for ColorTools, more tests will be added later. ColorTools has 4694 tests.
- [x] Publish version 1.0.0 on pub.dev.
- [x] Release version 1.0.0.
- [x] Add "name that color" function that can give a name to "any" color in English.
- [x] For the color-wheel picker, add text input to get a given color based on entered HEX code.
- [x] Fix doc images that show up OK in GitHub readme.md, but not on pub.dev.
- [x] Review and correct documentation mistakes and typos, first pass anyway.
- [x] Review and update the API.
