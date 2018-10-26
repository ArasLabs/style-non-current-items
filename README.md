# Style Non-Current Items

This document demonstrates two ways to style the form of a non-current version of an item.

1. Change the background color of the non-current item's form.
2. Display a watermark/overlay image indicating that the item displayed is not current.

## Project Details

See [TESTSTATUS file](./TESTSTATUS.md) for latest testing information.

#### Built Using:
Aras 11.0 SP7

#### Versions Tested:
Aras 11.0 SP7

#### Browsers Tested:
Internet Explorer 11, Firefox 38 ESR, Chrome

> Though built and tested using Aras 11.0 SP7, this project should function in older releases of Aras 11.0 and Aras 10.0.

## How It Works

The project's import package includes two methods - `labs_StyleNonCurrent` and `labs_NonCurrentOverlay`, both of which use the same basic logic to determine whether the context item is the current version.

First, we check whether the context item includes the `is_current` property. If so, we proceed with that value. If not, we retrieve the `is_current` property from the server. If the `is_current` property's value is `0`, we style the form accordingly:

- **labs_StyleNonCurrent:** changes the background color of the item's form
- **labs_NonCurrentOverlay:** displays an HTML field containing a watermark image

## Installation

#### Important!
**Always back up your code tree and database before applying an import package or code tree patch!**

### Pre-requisites

1. Aras Innovator installed (version 11.0 SPx preferred)
2. Aras Package Import tool
3. StyleNonCurrentItems import package
4. StyleNonCurrentItems code tree overlay

### Installation Steps

1. Backup your code tree and store the backup in a safe place.
2. Copy the Innovator folder from the project's CodeTree subdirectory.
3. Paste the Innovator folder into the root directory of your Aras installation.
  * Tip: This is the same directory that contains the InnovatorServerConfig.xml file.
4. Backup your database and store the BAK file in a safe place.
5. Open up the Aras Package Import tool.
6. Enter your login credentials and click **Login**
  * _Note: You must login as root for the package import to succeed!_
7. Enter the package name in the TargetRelease field.
  * Optional: Enter a description in the Description field.
8. Enter the path to your local `..\StyleNonCurrentItems\Import\imports.mf` file in the Manifest File field.
9. Select **StyleNonCurrentItems** in the Available for Import field.
10. Select Type = **Merge** and Mode = **Thorough Mode**.
11. Click **Import** in the top left corner.
12. Close the Aras Package Import tool.

You are now ready to login to Aras and check out the examples for customizing 'non-current items' forms.

## Usage

### Change the Background Color

![Custom Background Color](./Screenshots/bg-color.gif)

1. Log in to Aras as admin.
2. Click **Administration > Forms** and search for the Part form.
3. Open the Part form for editing.
4. Click the **Form Event** tab.
5. Find `labs_StyleNonCurrent` in the grid and set the **Event** column value to **OnLoad**.
6. Save the form.
7. Click **Design > Parts** in the table of contents (TOC).
8. Open an existing Part with previous versions (generation > 1).
9. On the Part form, click **View > Revisions**.
10. In the resulting dialog, double-click one of the previous generations of the Part.

The Part form that appears will have a grey background. If you would like to change the color or style applied to 'non-current items', you can edit the `labs_StyleNonCurrent` method.

### Display a Watermark Image

![Watermark Image](./Screenshots/overlay.gif)

1. Log in to Aras as admin.
2. Click **Administration > Forms** and search for the Part form.
3. Open the Part form for editing.
4. Click the **Form Event** tab.
5. Find `labs_NonCurrentOverlay` in the grid and set the **Event** column value to **OnLoad**.
6. Find `labs_StyleNonCurrent` in the grid and confirm the **Event** column value is null/blank.
7. Save the form.
8. Click **Design > Parts** in the table of contents (TOC).
9. Open an existing Part with previous versions (generation > 1).
10. On the Part form, click **View > Revisions**.
11. In the resulting dialog, double-click one of the previous generations of the Part.

The Part form that appears will have a watermark image that says "Non Current". To change the watermark image being displayed:

1. Add your image to the code tree under `Innovator\Client\customer\`.
2. Update the HTML source of the `overlay` field on the Part form.

> Note: If your custom watermark image is not semi-transparent, you will need to update the CSS rules for the contents of the `overlay` field.

## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request

For more information on contributing to this project, another Aras Labs project, or any Aras Community project, shoot us an email at araslabs@aras.com.

## Credits

Created by Eli Donahue for Aras Labs. @EliJDonahue

## License

Aras Labs projects are published to Github under the MIT license. See the [LICENSE file](./LICENSE.md) for license rights and limitations.
