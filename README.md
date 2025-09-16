# ZMCKit

ZMCKit is an Android library that simplifies the integration of camera functionalities in your applications. This library is designed to work seamlessly with the CameraActivity for capturing images and videos, as well as handling lens changes and other camera configurations.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [License](#license)

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

In your app-level `build.gradle` file, add the following dependency:

```groovy
dependencies {
    implementation 'com.ziylanmedya:zmckit:1.0.8' // Update the version as necessary
}
```

## Usage

### Step 1: Initialize ZMCKitManager

In your main activity or wherever you want to use the camera functionality, initialize the `ZMCKitManager`:

```kotlin
import com.snap.zmckit.ZMCKitManager

class MainActivity : AppCompatActivity() {

    private lateinit var zmckitManager: ZMCKitManager

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Initialize ZMCKitManager
        zmckitManager = ZMCKitManager.getInstance(this)

        // Initialize Capture Launcher and Set Callbacks
        zmckitManager.initCaptureLauncher(object : ZMCKitManager.CaptureCallback {
            override fun onImageCaptured(uri: String) {
                println("Image Captured.")
            }

            override fun onVideoCaptured(uri: String) {
                println("Video Captured.")
            }

            override fun onCaptureCancelled() {
                println("Capture was cancelled.")
            }

            override fun onCaptureFailure(exception: Exception) {
                println("Capture failed.")
            }
        })

        // Set a listener to handle lens change
        zmckitManager.onLensChange { lensId ->
            // Handle the lens change event
            println("Lens changed: $lensId")
        }
    }
}
```

### Step 2: Launch the Camera

To open the camera for a product or group view, use the following methods:

#### For Single Product View:
```kotlin
// Setup button to launch product view
findViewById<Button>(R.id.showProductButton).setOnClickListener {
    zmckitManager.showProductView(
        snapAPIToken = BuildConfig.CAMERA_KIT_API_TOKEN,
        partnerGroupId = BuildConfig.LENS_GROUP_ID,
        lensId = BuildConfig.LENS_ID
    )
}
```

#### For Group View:
```kotlin
// Setup button to launch group view
findViewById<Button>(R.id.showGroupButton).setOnClickListener {
    zmckitManager.showGroupView(
        snapAPIToken = BuildConfig.CAMERA_KIT_API_TOKEN,
        partnerGroupId = BuildConfig.LENS_GROUP_ID
    )
}
```

### Example

Here’s a complete example of how to use the `ZMCKit` library in an activity:

```kotlin
class MainActivity : AppCompatActivity() {

    private lateinit var zmckitManager: ZMCKitManager

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        zmckitManager = ZMCKitManager.getInstance(this)

        // Initialize Capture Launcher and Set Callbacks
        zmckitManager.initCaptureLauncher(object : ZMCKitManager.CaptureCallback {
            override fun onImageCaptured(uri: String) {
                println("Image Captured.")
            }

            override fun onVideoCaptured(uri: String) {
                println("Video Captured.")
            }

            override fun onCaptureCancelled() {
                println("Capture was cancelled.")
            }

            override fun onCaptureFailure(exception: Exception) {
                println("Capture failed.")
            }
        })

        // Set a listener to handle lens change
        zmckitManager.onLensChange { lensId ->
            // Handle the lens change event
            println("Lens changed: $lensId")
        }

        // Buttons to show product or group views
        findViewById<Button>(R.id.showProductButton).setOnClickListener {
            zmckitManager.showProductView(
                snapAPIToken = BuildConfig.CAMERA_KIT_API_TOKEN,
                partnerGroupId = BuildConfig.LENS_GROUP_ID,
                lensId = BuildConfig.LENS_ID
            )
        }

        findViewById<Button>(R.id.showGroupButton).setOnClickListener {
            zmckitManager.showGroupView(
                snapAPIToken = BuildConfig.CAMERA_KIT_API_TOKEN,
                partnerGroupId = BuildConfig.LENS_GROUP_ID
            )
        }
    }
}
```

In this example, the camera functionality is integrated with buttons to switch between product view and group view. The results are automatically handled in the background by `ZMCKitManager` through the registered callbacks.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
