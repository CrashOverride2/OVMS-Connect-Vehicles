![OVMS Connect](assets/images/splash.png)
# Creating a Vehicle Configuration File

## Overview

The OVMS Connect app uses a flexible system to display vehicle status information dynamically on the "Vehicle Info" screen. This is achieved through a JSON configuration file that maps data points and visual elements to a top-down image of the vehicle.

By creating a new JSON file and the corresponding image assets, you can add support for any vehicle. This guide explains the file structure and the JSON schema in detail.

## 1. File & Folder Structure

First, you need to create the correct folder and file structure within the project's `assets` directory. The app looks for files following a specific naming convention.

Let's assume you are adding a "Tesla Model S" with the internal name `models`.

1.  **Vehicle Asset Folder:** Create a new folder for your vehicle inside `assets/images/vehicles/`.
    *   `assets/images/vehicles/models/`

2.  **Base Images:** Add the primary vehicle images to this folder. The app uses a top-down view for this screen and a side view for the main dashboard. The file name should be `<color>_top.png` and `<color>_side.png`.
    *   **Top View:** `assets/images/vehicles/models/default_top.png`
    *   **Side View:** `assets/images/vehicles/models/default_side.png`

3.  **Overlay Images:** Create an `overlays` subfolder. This will hold all the small, transparent PNG images that are layered on top of the base image (e.g., an open door, glowing headlights).
    *   `assets/images/vehicles/models/overlays/`
    *   Example: `assets/images/vehicles/models/overlays/overlay_trunk.png`

4.  **JSON Configuration File:** Create the JSON file in the `assets/vehicle_configs/` directory. The filename **must match** the vehicle asset folder name.
    *   `assets/vehicle_configs/models.json`

---

## 2. The JSON Configuration File

The `<vehicle_name>.json` file is the blueprint for the `VehicleInfoScreen`. It's a collection of objects that define what to show and where to show it.

The coordinate system is based on percentages relative to the base image, where:
*   `(0.0, 0.0)` is the **top-left corner**.
*   `(1.0, 1.0)` is the **bottom-right corner**.

### JSON Schema Details

### `capabilities` (Object)

This is a set of boolean flags that tells the app which features the vehicle supports and which UI elements to attempt to render. If a capability is `false`, the corresponding overlay points in the JSON will be ignored.

| Key             | Type    | Description                                                                                              |
| :-------------- | :------ | :------------------------------------------------------------------------------------------------------- |
| `hasTpms`       | Boolean | `true` if the vehicle has a Tyre Pressure Monitoring System. Enables the `tyres` array processing.        |
| `hasDoors`      | Boolean | `true` if the vehicle reports individual door status. Enables `doorFL`, `doorFR`, `doorRL`, `doorRR`.      |
| `hasHood`       | Boolean | `true` if the vehicle reports hood (bonnet) status. Enables the `hood` object.                           |
| `hasTrunk`      | Boolean | `true` if the vehicle reports trunk (boot) status. Enables the `trunk` object.                           |
| `hasChargePort` | Boolean | `true` if the vehicle reports charge port door status. Enables the `chargePort` object.                    |
| `hasHeadlights` | Boolean | `true` if the vehicle reports headlight status. Enables the `headlights` object.                         |

### Component Points (`hood`, `trunk`, `doorFL`, etc.)

These objects define the position and appearance of specific vehicle components. They all use the `OverlayPoint` structure.

#### `OverlayPoint` Structure

| Key                    | Type    | Description                                                                                                                                                                                                                                                                   |
| :--------------------- | :------ | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xPercent`             | Number  | The horizontal position of the item's **center**, from `0.0` (left) to `1.0` (right).                                                                                                                                                                                           |
| `yPercent`             | Number  | The vertical position of the item's **center**, from `0.0` (top) to `1.0` (bottom).                                                                                                                                                                                             |
| `widthPercent`         | Number  | (Optional) The width of the overlay as a percentage of the base image's width. Defaults to `0.12` (12%).                                                                                                                                                                       |
| `heightPercent`        | Number  | (Optional) The height of the overlay as a percentage of the base image's height. Defaults to `0.12` (12%).                                                                                                                                                                      |
| `rotationDegrees`      | Number  | (Optional) Rotates the overlay clockwise. Defaults to `0`.                                                                                                                                                                                                                    |
| `isFullSize`           | Boolean | If `true`, the overlay is stretched to cover the entire base image, ignoring all positioning and size percentages. Ideal for large overlays like open doors that replace the whole car view.                                                                                     |
| `activeStateImagePath` | String  | (Optional) The filename of the overlay image (e.g., `overlay_trunk.png`) to show when the component is "active" (e.g., open, on). The path is relative to the `overlays` folder. **If omitted, a default icon/text widget is shown instead (see "Fallback Behavior" below).** |
| `inactiveStateImagePath` | String  | (Optional) The filename of the image to show when the component is "inactive". If omitted, nothing is shown for the inactive state.                                                                                                                                             |


### Fallback Behavior: Default Icons (No Image Needed)

A key feature of the layout system is its ability to function even without a full set of custom images. This is especially useful for the standard component points (`hood`, `trunk`, `doorFL`, etc.).

If you define a component point (e.g., `hood`) in your JSON but **do not** provide an `activeStateImagePath`, the app will automatically render a default, dynamic widget at the specified location.

This default widget consists of:
*   An **Icon** that changes to represent the state (e.g., a filled circle for "open," an outlined circle for "closed").
*   A short **Text Label** (e.g., "Hood", "FL", "Trunk").
*   **Dynamic Coloring**: The icon and text will be colored to indicate status—usually red for an "active" or "alert" state (like an open door) and a neutral color for a "normal" state.

**Why is this useful?**
It allows you to create a basic, working vehicle layout very quickly. You can define the positions of all your doors, hood, and trunk, and the app will provide immediate visual feedback without you needing to create a single overlay image in a graphics editor. You can always add the custom `activeStateImagePath` later to enhance the visual presentation.

**Example (using fallback):**
```json
"hood": {
  "xPercent": 0.5,
  "yPercent": 0.2
}
```

### `tyres` (Array of `OverlayPoint`)

If `capabilities.hasTpms` is `true`, this array defines the locations for the TPMS data readouts. The order is important and should match the data source, typically: **Front-Left, Front-Right, Rear-Left, Rear-Right.**

```json
"tyres": [
  { "xPercent": 0.09, "yPercent": 0.28, "widthPercent": 0.17, "heightPercent": 0.07 },
  { "xPercent": 0.91, "yPercent": 0.28, "widthPercent": 0.17, "heightPercent": 0.07 },
  { "xPercent": 0.09, "yPercent": 0.82, "widthPercent": 0.17, "heightPercent": 0.07 },
  { "xPercent": 0.91, "yPercent": 0.82, "widthPercent": 0.17, "heightPercent": 0.07 }
]
```

### `dataPoints` (Array of `DataPoint`)

This array defines text-based data overlays, perfect for showing temperatures, voltages, etc.

| Key             | Type   | Description                                                                                                                                             |
| :-------------- | :----- | :------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `xPercent`      | Number | The horizontal position of the data box's **top-left corner**.                                                                                          |
| `yPercent`      | Number | The vertical position of the data box's **top-left corner**.                                                                                            |
| `label`         | String | The text label for the data (e.g., "Motor", "Battery").                                                                                                 |
| `mqttTopic`     | String | The full MQTT topic that provides the value for this data point (e.g., `v/m/temp`).                                                                     |
| `unit`          | String | (Optional) The unit to display after the value (e.g., "°C", "V", "%").                                                                                  |
| `iconCodepoint` | String | (Optional) The hex codepoint for a [Material Symbols](https://fonts.google.com/icons?selected=Material+Symbols) icon. Do not include the `0x` prefix. |

```json
"dataPoints": [
  {
    "xPercent": 0.42,
    "yPercent": 0.12,
    "label": "Motor",
    "mqttTopic": "v/m/temp",
    "unit": "°C",
    "iconCodepoint": "f305"
  }
]
```

### `statefulIconPoints` (Array of `StatefulIconPoint`)

Defines icons that change based on a boolean (true/false) MQTT value. Perfect for status indicators like car locked/unlocked or valet mode.

| Key            | Type   | Description                                                                      |
| :------------- | :----- | :------------------------------------------------------------------------------- |
| `xPercent`     | Number | The horizontal position of the icon's **center**.                                |
| `yPercent`     | Number | The vertical position of the icon's **center**.                                  |
| `mqttTopic`    | String | The MQTT topic that provides the `true`/`false` value.                           |
| `iconForTrue`  | String | The Material Symbols hex codepoint for the icon to show when the value is `true`.  |
| `iconForFalse` | String | The Material Symbols hex codepoint for the icon to show when the value is `false`. |
| `iconForNull`  | String | (Optional) The icon codepoint to show if the MQTT value is missing or invalid.   |

```json
"statefulIconPoints": [
  {
    "xPercent": 0.45,
    "yPercent": 0.5,
    "mqttTopic": "v/e/locked",
    "iconForTrue": "e897",
    "iconForFalse": "e898",
    "iconForNull": "e63f"
  }
]
```

### Multi-State Image Overlays (`chargeStateOverlay`, etc.)

This overlay displays a specific image from a list based on the *string value* of an MQTT topic. This is used for things like charge status ("charging", "done", "stopped"). You can define multiple of these with custom keys.

| Key                | Type              | Description                                                                                                                                                                                                 |
| :----------------- | :---------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `xPercent`         | Number            | Horizontal center for positioned overlays. Ignored if `isFullSize` is true.                                                                                                                                   |
| `yPercent`         | Number            | Vertical center for positioned overlays. Ignored if `isFullSize` is true.                                                                                                                                   |
| `mqttTopic`        | String            | The MQTT topic whose string value will determine which image to show.                                                                                                                                       |
| `isFullSize`       | Boolean           | If `true`, the chosen image is a full-size overlay. If `false`, it's a smaller, positioned image.                                                                                                             |
| `visibilityTopics` | Array of Strings  | (Optional) The overlay will only be visible if **at least one** of the MQTT topics in this list has a value of `true`. Useful for showing charge overlays only when the charge port is open or a pilot is active. |
| `imagePathMap`     | Object            | A dictionary mapping the string values from the `mqttTopic` to their corresponding overlay image filenames.                                                                                                 |

```json
"chargeStateOverlay": {
  "xPercent": 0.5,
  "yPercent": 0.5,
  "mqttTopic": "v/c/state",
  "isFullSize": true,
  "visibilityTopics": [ "v/c/pilot", "v/d/cp" ],
  "imagePathMap": {
    "charging": "chargeport_orange.png",
    "done": "chargeport_green.png",
    "stopped": "chargeport_red.png"
  }
}
```

---

## 3. Tips & Tricks

*   **Finding Coordinates:** Open your `_top.png` image in a graphics editor that shows pixel coordinates. Find the pixel `(x, y)` for your desired location. Calculate the percentages: `xPercent = pixel_x / image_width`, `yPercent = pixel_y / image_height`.
*   **Finding Icon Codepoints:** Browse the [Google Fonts Material Symbols page](https://fonts.google.com/icons?selected=Material+Symbols). Select an icon, and in the side panel, find the "Codepoint" value (e.g., `e897`). Use this value in your JSON.
*   **Start Simple:** Begin by defining just the `capabilities` and the component points (`hood`, `doors`, etc.) without any `ImagePath` values to take advantage of the fallback icons. This will help you quickly place everything correctly. You can add custom images later.
*   **Validate your JSON:** Use an online JSON validator to ensure your file has no syntax errors before adding it to the project.

---

## 4. Full metrics list

Here is a list with all Standard Metrics:

**[➡️ OVMS Standard Metrics](metrics.md)**