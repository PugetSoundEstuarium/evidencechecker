# Night at the Estuary · Google Sheets Setup

This package gives you a Google Sheets + Apps Script web app that does four things:

1. Holds a private list of all bottle codes
2. Reveals whether a code is a fragment or a pass
3. Logs each registration into Google Sheets
4. Emails you each time a code is registered

## What is included

- 100 total bottle codes
- 15 fragment codes
- 85 Estuary Investigation Pass codes
- launch lock until July 1, 2026
- one-time use bottle codes
- required name + email capture
- privacy options
- optional note field
- organizer email on every registration
- dashboard that tracks fragment progress

## Before you start

You need:

- a Google account
- Google Sheets
- the email address that should receive notifications

## Step 1. Create the spreadsheet

1. Open Google Sheets.
2. Create a new blank spreadsheet.
3. Rename it something clear, such as:
   `Night at the Estuary Investigation`

## Step 2. Open Apps Script

1. In the spreadsheet, click **Extensions**.
2. Click **Apps Script**.
3. A new Apps Script tab will open.

## Step 3. Replace the default files

You will see a default file called `Code.gs`.

1. Delete the contents of `Code.gs`.
2. Open the `Code.gs` file from this package.
3. Copy everything.
4. Paste it into the Apps Script `Code.gs` file.

Now add the HTML files:

1. In Apps Script, click the **+** button next to Files.
2. Choose **HTML**.
3. Name it `Index` and paste in the contents of `Index.html`.
4. Add another HTML file named `Styles` and paste in `Styles.html`.
5. Add another HTML file named `ClientJS` and paste in `ClientJS.html`.

Now set the manifest:

1. In Apps Script, click the gear icon or project settings so you can view `appsscript.json` if needed.
2. Replace its contents with the contents of the package `appsscript.json`.

## Step 4. Update your email address

In `Code.gs`, find this line near the top:

`ORGANIZER_EMAIL: 'hap@pugetsoundestuarium.org',`

Change it if needed.

## Step 5. Save the project

1. Click the save icon.
2. Give the Apps Script project a name if prompted.

## Step 6. Run setup once

1. In the function dropdown at the top, choose `generateCodeRegistry`.
2. Click **Run**.
3. The first time, Google will ask for authorization.
4. Approve the permissions.

This will create these tabs in your spreadsheet:

- `Settings`
- `CodeRegistry`
- `Entries`
- `Dashboard`

## Step 7. Check the codes

1. Return to the spreadsheet.
2. Open the `CodeRegistry` tab.
3. You will see 100 rows.
4. Each row has:
   - a bottle code
   - an item type of `fragment` or `pass`
   - the item label

This sheet is your master list. Do not give this sheet to guests.

## Step 8. Deploy the web app

1. Go back to Apps Script.
2. Click **Deploy**.
3. Click **New deployment**.
4. Under Select type, choose **Web app**.
5. Set:
   - **Execute as:** Me
   - **Who has access:** Anyone
6. Click **Deploy**.
7. Copy the web app URL.

## Step 9. Build the QR codes

Each bottle needs its own QR code that contains its own bottle code.

The format is:

`YOUR_WEB_APP_URL?code=ABCD-EFGH-JKLM`

Example:

`https://script.google.com/macros/s/XXXX/exec?code=ABCD-EFGH-JKLM`

How to do it:

1. Copy the bottle code from the `CodeRegistry` tab.
2. Add it to the end of your web app URL using `?code=`.
3. Turn that full URL into a QR code.
4. Put that QR code on the bottle.

## Step 10. Test before printing

Test at least 3 bottles before you print all QR codes.

### Test checklist

1. Scan one QR code before July 1.
2. Confirm it shows the locked page.
3. Temporarily change the launch date in `Code.gs` if you want to test the reveal flow now.
4. Scan a fragment code.
5. Confirm it shows a fragment reveal.
6. Scan a pass code.
7. Confirm it shows a pass reveal.
8. Complete one registration.
9. Confirm:
   - a row appears in `Entries`
   - the matching code is marked claimed in `CodeRegistry`
   - the `Dashboard` updates
   - you receive an email notification

## What guests experience

### Before July 1
They see:
- The investigation is not yet open
- Return July 1 to reveal what is inside

### After July 1
They:
- scan the bottle QR code
- see whether they have a fragment or pass
- enter name and email
- choose privacy options
- submit

## Your key tabs

### `CodeRegistry`
Master inventory of all bottle codes

### `Entries`
Every successful registration

### `Dashboard`
Quick progress summary

## Common changes you may want to make

### Change launch date
In `Code.gs`, change:

`LAUNCH_DATE: '2026-07-01',`

### Change pass validity window
In `Code.gs`, change:

- `PASS_VALID_FROM`
- `PASS_VALID_TO`

### Regenerate all bottle codes
Run the function:

`generateCodeRegistry`

Warning: do this only before printing QR codes.

### Clear registrations but keep the same bottle codes
Run the function:

`resetClaimsKeepCodes`

## Important note

If you deploy a new version later, you may need to create a new deployment version or update the existing deployment in Apps Script.

## Recommendation

Keep one private backup copy of the spreadsheet after setup and before live use.
