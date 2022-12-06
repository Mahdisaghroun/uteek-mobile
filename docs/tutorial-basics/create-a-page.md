---
sidebar_position: 1
---

# Android

## Linking your repository
If you haven't previously connected to your repository service account, you must do this first. Once your account is connected, select the repository where your React Native project is located. You must have admin and pull permissions to set up a build for a repository.

## Selecting a branch
After selecting a repository, select the branch you want to build. By default, App Center lists all active branches.

##  Setting up your first build
Before your first build, you must configure the React Native project.

###  Project
Select your project’s package.json. App Center will automatically extract information from its associated build.gradle (app level) file, including dependencies, build tools version, build types, and product flavors.

 Note

For best performance, the analysis is currently limited to four directory levels including the root of your repository.

###  Build variant
The available build variants will populate from the Build Types and Product Flavors specified in the project's build.gradle (app level) file. Select which build variant should be built.

 Note

App Center Build supports finding build variants as the combination of a Build Type (debug, release or custom defined) and one optional Product Flavor. Detecting combinations of multiple product flavors aren't supported at this time.

### Node.js version
Select the Node.js version to use for the build Read more about how to select Node.js version

### Build triggers
By default, a new build is triggered every time a developer pushes to a configured branch. This is referred to as "Continuous Integration". If you prefer to trigger a new build manually, you can change this setting in the configuration pane.

### Build Android App Bundle (.aab)
The Android App Bundle is a distribution format that can be uploaded to the Play Store. It's used to generate optimized APKs for specific devices. You can find out more about the Android App Bundle in the official Android documentation, which also helps you understand whether you want to build a bundle along with your regular .apk.

Toggle on the option for Android App Bundle to produce an .aab in addition to the .apk. If the build.gradle (app level) file contains the android.bundle block, this option will automatically be toggled on.

### Increment version number
When enabled, the version code in the AndroidManifest.xml of your app automatically increments for each build. The change happens during the actual build and won't be committed to your repository.

### Launch your successful build on a real device
Use the newly produced APK file to test if your app starts on a real device. Launch tests will add approximately 10 more minutes to the total build time. Read more about how to configure launch tests.

### Code signing
A successful build will produce an .apk file and an additional .aab file if enabled. To release the build to the Play Store, it must be signed with a valid certificate stored in a keystore. To sign the builds produced from a branch, enable code signing in the configuration pane, upload your keystore to your repository, and provide the relevant values in the configuration pane. You can read more about Android code signing App Center's Android code signing documentation. The .aab will be signed using the same credentials as the .apk.

### Distribute the build
You can configure each successful build from a branch to be distributed to a previously created distribution group or a store destination. You can add a new distribution group or configure a store connection from within the Distribute service. There's always a default distribution group called "Collaborators" that includes all the users who have access to the app.

 Note

If distributing to the Google Play Store, an Android App Bundle (.aab) is preferred and will be distributed if enabled. For App Center distribution groups and Intune store destinations, a regular .apk will be used even if an .aab is also generated.

## Build results
After a build triggers, the build will be in one of the following states:

queued - the build is in a queue waiting for resources to be freed up
building - the build is running the predefined tasks
succeeded - the build is completed and it's succeeded
failed - the build has completed but it's failed; you can troubleshoot what went wrong by downloading and inspecting the build log
canceled - the build has been canceled by a user action or it's timed out
### Build logs
For a completed build (succeeded or failed), download the logs to understand more about how the build went. App Center provides an archive with the following files:

```NA
|-- 1_build.txt (this is the general build log)
|-- build (this folder contains a separate log file for each build step)
    |-- build-step-1
    |-- build-step-2
    |--
    |-- build-step-n (e.g. n_Post Job Cleanup.txt)
    ```
The build step-specific logs (located in the build/ directory of the archive) are helpful for troubleshooting and understanding in what step and why the build failed.

### The app (.apk)
The .apk file is an Android application packaged file that stores the Android app. If the build has been correctly signed, the app can be installed on a real device and deployed to the Play Store. If the build hasn't been signed, the app can run on an emulator or be used for other purposes.

