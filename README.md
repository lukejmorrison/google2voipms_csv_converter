# Google Contacts to VoIP.ms CSV Converter

## Description

This script converts a Google Contacts CSV file exported from Google Contacts into a VoIP.ms phonebook CSV format. It uses [PapaParse](https://www.papaparse.com/) to parse the CSV files and generates an output file compatible with the VoIP.ms phonebook import feature. The script supports multiple phone numbers per contact, processes labels for group assignment (e.g., "starred" or custom groups), and formats phone numbers by removing non-digit characters (except for a leading "+").

Once converted, you can upload the properly formatted phonebook to your VoIP.ms account to manage incoming calls. To use this setup with VoIP.ms:
- **Upload the Phonebook**: After conversion, upload the CSV to VoIP.ms via the phonebook import feature.
- **Set Default DID Routing**: Configure the default routing for your DID (Direct Inward Dialing) number to "Hangup". This ensures that calls from unknown or unfiltered numbers are automatically disconnected.
- **Create Caller ID Filters**: Use the group names assigned in the phonebook (e.g., "General", "ForwardToCell") to create caller ID filters in VoIP.ms. These filters override the default "Hangup" routing, directing calls to specific destinations like voicemail, a cell phone, or custom recordings based on the caller’s group.

## Usage

1. **Open the Script**: Launch `gmailcontacts2voipms_phonebook_csv.html` in a web browser.
2. **Upload File**: Click the "Choose File" button and select your Google Contacts CSV file.
3. **Header Option**: Check the "Include header row in output CSV" checkbox if you want headers in the output file.
4. **Convert**: Click the "Convert" button.
5. **Download**: The converted file will automatically download as `YYYY-MM-DD_voipms_phonebook.csv` (e.g., `2025-04-04_voipms_phonebook.csv`).

## Using with VoIP.ms Caller ID Filtering

After uploading your converted phonebook to VoIP.ms, you can leverage the group labels to create caller ID filters for customized call routing. This section explains how to set it up.

### Setup Overview

1. **Default Routing**:
   - In your VoIP.ms account, navigate to your DID settings.
   - Set the default routing for your DID to "System: Hangup". This ensures all calls without a matching filter are terminated.

2. **Caller ID Filters**:
   - Go to the "Caller ID Filtering" section in VoIP.ms.
   - Create filters that match the group labels from your phonebook (e.g., "General", "ToVMGroup").
   - Assign a specific routing action to each filter (e.g., voicemail, forwarding, or playing a recording).

### Example Filters

Here are some example caller ID filters based on group labels from the phonebook:

- **General Group**:
  - **Filter**: Match group "General".
  - **Routing**: Forward to voicemail at 4168384337.
  - **Purpose**: Send calls from contacts labeled "General" to a specific voicemail.

- **ToVMGroup**:
  - **Filter**: Match group "ToVMGroup".
  - **Routing**: Forward to voicemail at 7058080241.
  - **Purpose**: Route calls from this group to a different voicemail.

- **ForwardToCell**:
  - **Filter**: Match group "ForwardToCell".
  - **Routing**: Forward to your cell phone (e.g., forwarding entry 571417).
  - **Purpose**: Direct calls from important contacts to your mobile.

- **BuzzerGroup**:
  - **Filter**: Match group "BuzzerGroup".
  - **Routing**: Play a DTMF tone (e.g., IVR 95554 with DTMF 999).
  - **Purpose**: Play a custom tone or recording for these callers.

- **HangupGroup**:
  - **Filter**: Match group "HangupGroup".
  - **Routing**: System Hangup.
  - **Purpose**: Immediately disconnect calls from this group.

### How Group Labels Are Assigned

The conversion script assigns group labels as follows:
- **Starred Contacts**: If a contact is starred in Google Contacts, it gets the label "starred".
- **Custom Labels**: The first non-default label (not starting with "*") is used as the group label (e.g., "ForwardToCell").
- **Default Label**: If no custom labels are present, the group label defaults to "General".

When creating filters in VoIP.ms, ensure the group names match exactly as they appear in the phonebook CSV.

### Additional Notes

- For detailed instructions on setting up caller ID filters, see the [VoIP.ms CallerID Filtering documentation](https://wiki.voip.ms/article/CallerID_Filtering).
- Wildcards (e.g., `514*`) are supported for phone number matching, but for group-based filtering, use the exact group label.

## Sample CSV Files

Below are two sample CSV files with fictional sci-fi names and numbers, demonstrating the conversion process and group label usage.

### Sample Google Contacts CSV (`2025-04-04T19-31-00_sample_google_contacts.csv`)

```csv
"First Name","Last Name","Phone 1 - Value","Phone 1 - Type","Phone 2 - Value","Phone 2 - Type","Labels"
"Hari","Seldon","12025550123","Home","","","ForwardToVM705808 ::: * myContacts ::: * starred"
"Trillian","McMillan","13035551234","Mobile","13035559876","Home","ForwardToCell ::: * myContacts ::: * starred"
"Mannie","Garcia","14045554321","Mobile","","","ForwardToCell ::: * myContacts ::: * starred"
"Arthur","Dent","15055556789","Mobile","","","General ::: * myContacts"
"","Hyperion Cantos","16065550987","Main","","","Buzzer ::: * myContacts"
"Ford","Prefect","17075557890","Other","","","Hangup ::: * myContacts"
"R. Daneel","Olivaw","18085553210","Mobile","","","* myContacts"
"Wyoming","Knott","19095554321","Work","19095559876","Home","General ::: * myContacts"
"Zaphod","Beeblebrox","20005551234","Mobile","","","Hangup ::: * myContacts ::: * starred"
"Salvor","Hardin","21015557654","Home","","","ForwardToVM705808 ::: * myContacts"
```

### Sample VoIP.ms Phonebook CSV (`2025-04-04T19-31-00_sample_voipms_phonebook.csv`)

```csv
"Speed Dial","Name","Phone Number","Group Label","Caller ID Override","Note"
"","Hari Seldon - Home","12025550123","starred","",""
"","Trillian McMillan - Mobile","13035551234","starred","",""
"","Trillian McMillan - Home","13035559876","starred","",""
"","Mannie Garcia - Mobile","14045554321","starred","",""
"","Arthur Dent - Mobile","15055556789","General","",""
"","Hyperion Cantos - Main","16065550987","Buzzer","",""
"","Ford Prefect - Other","17075557890","Hangup","",""
"","R. Daneel Olivaw - Mobile","18085553210","General","",""
"","Wyoming Knott - Work","19095554321","General","",""
"","Wyoming Knott - Home","19095559876","General","",""
"","Zaphod Beeblebrox - Mobile","20005551234","starred","",""
"","Salvor Hardin - Home","21015557654","ForwardToVM705808","",""
```

## Running Locally with PapaParse

To run the script offline:
1. **Download PapaParse**: Get `papaparse.min.js` from [https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js](https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js).
2. **Save Locally**: Place it next to `gmailcontacts2voipms_phonebook_csv.html`.
3. **Update HTML**: Use `<script src="papaparse.min.js"></script>` in the HTML file.
4. **Run**: Open `gmailcontacts2voipms_phonebook_csv.html` in a browser.

## Uploading to GitHub via VS Code

To upload to `https://github.com/lukejmorrison/google2voipms_csv_converter`:
1. Open the project in VS Code.
2. Run: `git init`, `git add .`, `git commit -m "Updated with VoIP.ms filtering"`.
3. Link repo: `git remote add origin https://github.com/lukejmorrison/google2voipms_csv_converter.git`.
4. Push: `git push -u origin main`.

```