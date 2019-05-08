# ProfileCreator 0.2.6

## New Features

### Additional Payload Key Information

A new footer for payload keys is shown if there are additional information about that key. 

The following information items are currently supported:

- If the key is only supported from or up to a specific os/app-version.
- URL linking to additional documentation about the key, shown as a small book icon. When clicked it opens this URL in your default web browser. (#135)

### Export to .plist

Now, in addition to exporting profiles you can also export preferences to a .plist.  This makes it easier to import into the Custom Settings payload of an MDM.

This option is only shown when holding the export button in the profile or payload window to bring upp the context menu and choosing "Export Plist".

This will export each enabled payload domain to their own file in the selected folder.

### Export Button in Editor Window

Added an export button to the profile editor window to make exporting the currently open profile easier.

### Export Keyboard Shortcut

The Export menu item now has a keyboard shortcut mapped to `⌘E` (#128)

### Custom ProfileIdentifierFormat & PayloadIdentifierFormat

In the ProfileCreator preferences under 'Advanced', you can specify a custom default format for the `ProfileIdentifier` & `PayloadIdentifier` values.  See [the wiki](https://github.com/erikberglund/ProfileCreator/wiki/Preferences:-Advanced#payload-identifier) for more info. (#55)

The application will rename your profile configuration file (.pfcconf) to match the current value.

**IMPORTANT** As there can't be two files with the same name in a directory, the application will not rename a file if the new name already exists. The file is still saved though, but keeps its old name.

The file rename only occurs when a profile is saved, it does not change every saved file retroactively if the setting is changed.

### New Interface Item: Slider

A slider is now available as an input method for certain payload keys with a predefined list of items to select. See [Use slider as input method](#Use-slider-as-input-method)

### New Interface Item: Combo Box

The app now support keys that allow both custom input and selecting values from a list. See [Allow both custom and `pfm_range_list` values as input](#Allow-both-custom-and-pfm_range_list-values-as-input)

### Copy Description Text

Now payload key description text is selectable for copying & pasting.

### Develper: Show Payload Manifest in Finder

When you select a payload from the left sidebar, you can click 'Show Payload Manifest in Finder' from the Developer menu (this must be enabled first) to take you directly to the manifest file in the Finder.

### Donate Button

I have been asked multiple times to add a Donate button, so from this version there is a Donate button in the application preferences under General.

## Updated ProfileManifest Features

Vist the [Manifest Format Versions](https://github.com/erikberglund/ProfileManifests/wiki/Manifest-Format-Versions) to view all changes made to the manifest format used by ProfileCreator.

### ProfileManifest Subdomains

In some cases, there are payloads that are used for multiple purposes.  com.apple.MCX, for example, handles Energy Settings as well as Time Server & Mobile Accounts.  This provides the ability to separate preferences into different manifest files, but which all contribute to the same domain. (https://github.com/erikberglund/ProfileManifests/issues/20)

- com.apple.MCX-EnergySettings
- com.apple.MCX-MobileAccounts
- com.apple.MCX-TimeServer

### Allow historical dates

Now you can supply a historical date for `date` preferences by setting `pfm_date_allow_past` key to `true`. (#129)

### Additional options for payload keys utilizing a `pfm_range_list`

#### Allow only unique values in an Array

The new key `pfm_value_unique` when set to `true` will only permit a given value to be added once within an array.  Support for additional input methods will be added in a later release (#146).

#### Allow both custom and `pfm_range_list` values as input

The new key `pfm_range_list_allow_custom_value` when set to `true` will allow the user to enter custom value(s) for a given preference while also selecting from the available `pfm_range_list` items.

#### Use slider as input method

To use a slider as the input method for a `pfm_range_list`, the new key: `pfm_view` must be set to `slider`.

### Support for value copy from other domains

The `pfm_value_copy` and `pfm_default_copy` keys now supports specifying the domain before the key path to be copied by using the `@` character as domain-keypath separator.

One example of this configuration are payloads that support for the identity payload. By specifying the following configuration in a payloads `IdentificationUUID` key, the value for the Identification payload's UUID will be automatically populated as the default value if the identity payload is added to the profile.

```xml
<key>pfm_default_copy</key>
<string>com.apple.configurationprofile.identification@PayloadUUID</string>
```

### Allow custom decimal places in number textfields.

The new key `pfm_value_decimal_places` will allow the manifest creator to specify the number of decimal places to show in the GUI. (#110)

## New Payloads

- org.mozilla.firefox (macOS)(Added by @bp88) (https://github.com/erikberglund/ProfileManifests/pull/16)
- com.apple.iMovieApp (macOS)(Added by @wegotoeleven) 
- MunkiReport (macOS)(Added by @apizz) (https://github.com/erikberglund/ProfileManifests/pull/29)
- com.apple.NetworkBrowser (macOS)(Added by @apizz) (https://github.com/erikberglund/ProfileManifests/pull/47)
- uk.co.dataJAR.jamJAR (macOS)(Added by @apizz) (https://github.com/erikberglund/ProfileManifests/pull/48)
- com.apple.garageband (macOS)(Added by @apizz) (https://github.com/erikberglund/ProfileManifests/pull/49)
- com.apple.notificationsettings (iOS)(Added by @apizz) (https://github.com/erikberglund/ProfileManifests/pull/64)
- com.apple.touristd (macOS)(Added by @apizz) (https://github.com/erikberglund/ProfileManifests/pull/65)
- com.barebones.bbedit.plist (macOS)(Added by @apizz) (https://github.com/erikberglund/ProfileManifests/pull/69)
- com.apple.applicationaccess-tvOS (tvOS)(Added by @apizz) (https://github.com/erikberglund/ProfileManifests/pull/71)
- com.apple.applicationaccess-iOS (iOS)(Added by @apizz) (https://github.com/erikberglund/ProfileManifests/pull/72)
- com.apple.Safari (macOS)(Added by @erikberglund)
- com.apple.education (macOS/iOS)(Added by @apizz)
- com.apple.tvremote (macOS)(Added by @apizz)
- com.apple.MCX-MobileAccounts (macOS)(Added by @erikberglund)
- com.apple.MCX-TimeServer (macOS)(Added by @erikberglund)
- com.microsoft.rdc (macOS)(Added by @apizz)

## Updated Payloads

### com.apple.iMovieApp
- @wegotoeleven added user-supplied keys to allow suppressing iMovie prompts for different iMovie app versions (https://github.com/erikberglund/ProfileManifests/pull/21 & https://github.com/erikberglund/ProfileManifests/pull/40)

### com.apple.logic10
- @apizz did some manifest reformatting & added description regarding the correct preference misspelling of `DontShowAdditionalContentDowload ` (https://github.com/erikberglund/ProfileManifests/pull/54)

### com.apple.SoftwareUpdate
- @wegotoeleven added `AutomaticallyInstallMacOSUpdates` (https://github.com/erikberglund/ProfileManifests/pull/19)
- @mikedowler corrected wording on `AutomaticallyInstallMacOSUpdates` pref to correctly indicate this refers to macOS updates, not automatic App Store Updates (which is handled by `AutoUpdate` in com.apple.commerce and unfortunately cannot be managed by profile 😢 ) (https://github.com/erikberglund/ProfileManifests/pull/63)

### com.apple.applicationaccess-macOS (*formerly com.apple.applicationaccess*)
- @mikedowler added `allowPasswordAutoFill`, `allowPasswordSharing`,  `allowPasswordProximityRequests `, `allowCloudBTMM `, and `allowCloudFMM` (https://github.com/erikberglund/ProfileManifests/pull/59)
- @apizz added menu structure (https://github.com/erikberglund/ProfileManifests/pull/73)

### com.microsoft.autoupdate2
- @qu1gl3s added Microsoft Teams & OneDrive to MAU (https://github.com/erikberglund/ProfileManifests/pull/23)
- @qu1gl3s added `pfm_range_list` items for `Application ID`given difference between MAU 4.6 and earlier & MAU 4.7+ (https://github.com/erikberglund/ProfileManifests/pull/60)

### com.apple.dashboard
- @erikberglund fixed the key `WhiteList`, which was incorrectly listed as `whiteList`. (https://github.com/erikberglund/ProfileManifests/commit/9c0b7e80531a71f042895817e0869a7d136d1de5)

### com.apple.NSExtensions
- @mikedowler fixed the incorrect payload identifier & type (was listed as com.apple.font) (https://github.com/erikberglund/ProfileManifests/pull/58)

### com.apple.mail.managed
- @erikberglund added `IdentificationUUID` (https://github.com/erikberglund/ProfileManifests/commit/100d154a131b6c13ef34cf2ba78e02718b8fd1c3)

### com.apple.ews.account (*formerly com.apple.eas.account*)
- @erikberglund fixed the incorrect PayloadType (was com.apple.eas.account) (https://github.com/erikberglund/ProfileManifests/commit/635d8217ff79ecdfc4da3a3a782b441e91ccd8d9)
- @erikberglund added support for `IdentificationUUID` from com.apple.mail.managed (https://github.com/erikberglund/ProfileManifests/commit/3c24c3aa4c35a14947ced9ff45f76473168bc754)
- @erikberglund fixed incorrect required tag for `EmailAddress` (https://github.com/erikberglund/ProfileManifests/commit/50b50991eb509a753961ce357634c5c0f8341e19)

### com.microsoft.Outlook
- @wegotoeleven added `DisableTeamsMeeting` (https://github.com/erikberglund/ProfileManifests/pull/25)

### com.microsoft.Excel

- @wegotoeleven added `TryDefaultPassword` (https://github.com/erikberglund/ProfileManifests/pull/24)

### com.microsoft.OneDrive

- @apizz added `FilesOnDemandPolicy`, `FilesOnDemandEnabled`, `IsHydrationToastAllowed`, & `HydrationDisallowedApps`  (https://github.com/erikberglund/ProfileManifests/pull/30)

### menu.nomad.login.ad

- @erikberglund added all new and updated keys for 1.3

### com.apple.Enterprise-Connect

- @erikberglund added all new and updated keys for 2.0

## Bug Fixes

- Fixed a bug that was causing the selected payload tab when switching GUI & XML views to not be remembered (#59 & #127)
- Fixed bug causing a long `pfm_range_list` to not display all available options (#99)
- Fixed issue causing segmented controls to not extend to multiple lines (#100)
- Fixed issue causing multiple items to not be able to be added to an array (#101)
- Fixed issue where an array of booleans was not creating a UI (#104)
- Fixed issue where the `pfm_value_unit` was not displaying when `pfm_range_list` was used (#111)
- Fixed issue where in some cases the full `pfm_description` was not displaying (#117 & #57)
- Fixed issue where in some cases the "Deprecated" text was being hidden when a long `pfm_title` was used (#119)
- Fixed issue where `pfm_app_deprecated` was not appearing (#138 & #118)
- Fixed issue were a long text field would cause the `pfm_value_unit` to not appear (#141)
- Fixed issue that prevented you from adding additional items supplied in a `pfm_range_list` for an array of strings when the first item from the list was selected.
- Fixed a bug where arrays with a single dictionary (where the array has `pfm_range_max` = 1 and the subkey of that array was a dictionary) would not display, save or export correctly. (LoginScripts for example).
- Fixed issue that caused a preference with no `pfm_title` configured to have its text turn orange when clicked but not return to black when clicked again.
- Fixed issue where the number input text field was too small for some range definitions when the value type was set to `float`. (#108)
- Fixed issue where the application sometimes would crash if no item was selected in a tableview and the `-` button was pressed to remove a row.
- Fixed issue where the export button's menu was shown even if the button was disabled.
- Fixed issue where importing an existing mobileconfig with payloads not known to ProfileCreator would not show an error if the payload was in the "Profile" content style.
- Fixed issue where importing an existing mobileconfig with payloads not known to ProfileCreator would not allow the unknown payloads to be exported.
- Fixed issue where the placeholder string `Set On Device` was not shown for conditionals that had a requirement for pushed payloads.
- Fixed minor layout issues with tableview row items.

## Contribute

There are many ways to contribute to this project. Here are a few listed below:

- Test and report bugs or incorrect behavior both in the UI and in the exported profiles.
- Language and spelling errors. (English is not my native language).
- Missing payloads or payload keys. (Contribute to the ProfileManifests repository to improve the manifests used to define all payloads, keys and their interactions.)
- Add feature requests or suggestions by opening an issue in this repository.

