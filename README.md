Here is an updated version of your README to include handling single lenses and lens groups, along with other refinements:

---

# ZMCKit

ZMCKit is an Android library that simplifies the integration of Snap Camera functionalities into your applications. It supports capturing images and videos using single or group lens configurations.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
  - [Initialize ZMCKitManager](#initialize-zmckitmanager)
  - [Show Single Lens](#show-single-lens)
  - [Show Lens Group](#show-lens-group)
  - [Handle Camera Capture Results](#handle-camera-capture-results)
- [License](#license)

---

## Installation

### Step 1: Add the Repository

Add the following Maven repository to your project-level `build.gradle` file:

```groovy
allprojects {
    repositories {
        google()
        mavenCentral()
        maven {
            url "https://raw.githubusercontent.com/idealinktr/ZMCKit-Android/main/"
        }
    }
}
```

### Step 2: Add the Dependency

In your app-level `build.gradle` file, include the dependency:

```groovy
dependencies {
    implementation 'com.ziylanmedya:zmckit:1.0.0' // Update the version as necessary
}
```

---

## Usage

### Initialize ZMCKitManager

To start using the camera features, initialize the `ZMCKitManager` in your activity or fragment. Use the provided callbacks to handle camera capture results.

```kotlin
import com.snap.zmckit.ZMCKitManager

class MainActivity : AppCompatActivity() {

    private lateinit var zmckitManager: ZMCKitManager

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        zmckitManager = ZMCKitManager(this)

        // Initialize capture launcher with callback
        zmckitManager.initCaptureLauncher(object : ZMCKitManager.CaptureCallback {
            override fun onImageCaptured(uri: String) {
                Log.d("MainActivity", "Image captured: $uri")
            }

            override fun onVideoCaptured(uri: String) {
                Log.d("MainActivity", "Video captured: $uri")
            }

            override fun onCaptureCancelled() {
                Log.d("MainActivity", "Capture cancelled")
            }

            override fun onCaptureFailure(exception: Exception) {
                Log.e("MainActivity", "Capture failed", exception)
            }
        })
    }
}
```

---

### Show Single Lens

Use the `showProductView` method to display a single lens by specifying its `lensId`:

```kotlin
fun showSingleLens() {
    val snapAPIToken = "your_api_token"
    val partnerGroupId = "your_group_id"
    val lensId = "your_lens_id"

    zmckitManager.showProductView(
        snapAPIToken = snapAPIToken,
        partnerGroupId = partnerGroupId,
        lensId = lensId
    )
}
```

---

### Show Lens Group

To display a group of lenses, use the `showGroupView` method and provide the `partnerGroupId`:

```kotlin
fun showLensGroup() {
    val snapAPIToken = "your_api_token"
    val partnerGroupId = "your_group_id"

    zmckitManager.showGroupView(
        snapAPIToken = snapAPIToken,
        partnerGroupId = partnerGroupId
    )
}
```

---

### Handle Camera Capture Results

`ZMCKitManager` provides callbacks to handle image and video capture results:

```kotlin
zmckitManager.initCaptureLauncher(object : ZMCKitManager.CaptureCallback {
    override fun onImageCaptured(uri: String) {
        Log.d("MainActivity", "Image captured: $uri")
    }

    override fun onVideoCaptured(uri: String) {
        Log.d("MainActivity", "Video captured: $uri")
    }

    override fun onCaptureCancelled() {
        Log.d("MainActivity", "Capture cancelled")
    }

    override fun onCaptureFailure(exception: Exception) {
        Log.e("MainActivity", "Capture failed", exception)
    }
})
```

To launch the camera and handle captures:

```kotlin
zmckitManager.openCamera(
    cameraFacingFront = true,
    cameraFacingFlipEnabled = true
)
```

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

This version includes sections to clarify usage for single and group lenses while ensuring consistency with the methods provided in the updated code. Let me know if you need further refinements!