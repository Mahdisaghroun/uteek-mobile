---
sidebar_position: 2
---

# IOS

App Center can build React Native apps written in React Native version 0.34 or newer.

To build a React Native app for iOS:

Connect to your repository service account (for example: Azure DevOps, Bitbucket, GitHub, or VSTS).
Select a repository and a branch where your app lives.
Configure the build's project or workspace, and the scheme you want to build.
 Note

For the app to run on a real device, the build needs to be code signed with a valid provisioning profile and a certificate.

## Linking your repository
First, connect your repository service account to App Center. Once your account is connected, select the repository where your iOS project is located. You must have admin and pull permission for the repository.

## Selecting a branch
After selecting a repository, select the branch you want to build. By default, all the active branches will be listed.

## Setting up your first build
Before your first build, the React Native project needs to be configured.

### Project
Select your project’s package.json. App Center will automatically detect the associated Xcode project/workspace.

### Xcode version
Select the Xcode version to run the build on from the dropdown list. If the toggle "Use legacy build system" is On, then the legacy build system will be used whatever the project or workspace settings. If the toggle "Use legacy build system" is Off, then the build system configuration from the project or workspace settings will be used.

 Note

Workspace setting should be committed to the repository
If workspace setting isn't committed, then the modern build system will be used
### Node.js version
Select the Node.js version to use for the build. Learn more about how to select Node.js version

### Build triggers
By default, a new build is triggered every time a developer pushes to a configured branch. If you prefer to trigger a new build manually, you can change this setting in the configuration pane.

### Increment build number
When enabled, the CFBundleVersion in the project's Info.plist of your app automatically increments for each build. The change happens pre-build and won't be committed to your repository.

### Code signing
A successful build produces an .ipa file. To install the build on a device, the build must be signed with a valid provisioning profile and certificate. To sign the builds produced from a branch, enable code signing in the configuration pane and upload a provisioning profile (.mobileprovision file) and a valid certificate (.p12), along with the password for the certificate.

The settings in your Xcode project must be compatible with the files you're uploading. Read more about App Center's iOS code signing and the Apple Developer documentation.

Signing apps with app or watchOS extensions requires an additional provisioning profile per extension.

### Launch your successful build on a real device
Use the newly produced .ipa file to test if your app starts on a real device; the launch test adds about 10 more minutes to the total build time. Read more about how to configure launch tests.

### CocoaPods
App Center scans the selected branch and if it finds a Podfile, it will automatically do a pod install step at the beginning of every build. This ensures that all dependencies are installed.

### Distribute to a distribution group
Configure each successful build from a branch to be distributed to a previously created distribution group. Add a new distribution group from within the Distribute section. There's always a default distribution group called "Collaborators" that includes all users who have access to the app.

Once you save the configuration, a new build will be automatically started.

## Build results
Builds can be in one the following states:

queued - the build is enqueued waiting for available resources
building - the build is running and executing predefined tasks
succeeded - the build completed successfully
failed - the build completed unsuccessfully; troubleshoot what went wrong by downloading and inspecting the build log
canceled - the build was canceled through user action or timed out
4.1. Build logs
For a completed build (succeeded or failed), download the logs to understand more about how the build went. App Center provides an archive with the following files:

```NA
|-- 1_build.txt (this is the general build log)
|-- build (this folder contains a separate log file for each build step)
    |-- <build-step-1> (e.g. 2_Get Sources.txt)
    |-- <build-step-2> (e.g. 3_Pod install.txt)
    |--
    |-- <build-step-n> (e.g. n_Post Job Cleanup.txt)
```
The build logs (located in the build/ directory of the archive) are helpful for troubleshooting and understanding in what step and why the build failed.

### The app (.ipa)
The .ipa file is an iPhone application archive file that contains the iOS app.

If the build was signed correctly, you can install the .ipa file on a real device that's included in the provisioning profile used when signing. More details about code signing and distribution with App Center can be found in App Center's iOS code signing documentation.
If the build isn't signed during the build, developers can sign the .ipa file (locally using codesign) or used for other purposes (for example, upload to Test service for UI testing on real devices or run in the simulator).
Unsigned builds won't produce an .ipa file. The artifact of an unsigned build is the .xcarchive file, which can be used to generate an .ipa file with the Xcode Archives organizer.