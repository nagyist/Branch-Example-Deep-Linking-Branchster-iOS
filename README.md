## Create a personal copy of the Branchsters app for testing!

1. From the command line:
     - Clone the repo: `git clone git@github.com:BranchMetrics/Branch-Example-Deep-Linking-Branchster-iOS.git`
     - `cd Branch-Example-Deep-Linking-Branchster-iOS/`
     - `pod install`
2. In Finder open: **BranchMonsterFactory.xcworkspace**
3. In Xcode click on the root node of the project: BranchMonsterFactory
4. Under Targets select BranchMonsterFactory, then the General tab
5. Change the Bundle Identifier to something **unique** (for this demo we'll use `io.branch.Objective-C.Branchsters`)
6. Change the Team to your Team (it must be a *paid* Apple Developer Account) and click **Fix Issue** to generate a new Provisioning Profile
7. Log in to the [Branch dashboard](https://dashboard.branch.io) and create a new app from the drop-down menu in the top right cornder
8. On the Settings, screen copy the Branch key
9. In the Xcode project's **info.plist** file, change the `branch_key` entry to the value of your new Branch key key
10. Add a new String key to the **info.plist** file: `branch_app_domain`
11. Populate the new `branch_app_domain` key with the value of the **Default domain name** field found in the Custom Link Domain section of the dashboard's Link Settings tab
12. Populate the Branch dashboard with the following values:
    - Always try to open app: Checked
    - I have an iOS App: Checked
    - iOS URL: `branchsters://` (from the **info.plist** file, this is URL Types > URL Schemes > Item 0)
    - Custom URL: (enter a web site here if you haven't published the app to the App Store - http://www.branch.io, for example)
    - Default URL: (any web site will do: http://www.branch.io, for example)

## Set up Universal Links

> **NOTE:** these steps will not work if you do not have a *paid* Apple Developer Account

1. In the **Branchsters.entitlements** file, add entries for the new Branch Live and Test link domains. For example:
    - **applinks:xxxx.app.link**
    - **applinks:xxxx.test-app.link**
    - **applinks:xxxx-alternate.app.link**
    - **applinks:xxxx-alternate.test-app.link**
2. Run the app and make sure that it launches properly on a device or on a simulator
3. Select the **Branchsters.entitlements** file and ensure the **BranchMonsterFactory** box is checked inside Target Membership
4. Populate the Branch dashboard with the following values:
    - Enable Universal Links: checked
    - Bundle Identifier: as set in the project above
    - Apple App Prefix: (find this in the Apple developer dashboard: https://developer.apple.com/account/ios/identifier/bundle)
4. Save the settings - you are done!

### Test
1. If the app was installed on the test device already:
    - Delete the app from the device
    - Clear Safari web content, history and cookies (Settings > Safari > Clear History and Website Data)
    - Reset the device's IDFA (Settings > Privacy > Advertising > Reset Advertising Identifier...)
2. Create a Marketing link from the Branch dashboard
3. Paste the link into Notes on an iPhone
4. Tap the link - you will get redirected to the web page
5. Install the app on the device via Xcode
6. Tapping on the link should now open the app directly
