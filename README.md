# Google Contacts to VoIP.ms CSV Converter

## Description

This script converts a Google Contacts CSV file exported from Google Contacts into a VoIP.ms phonebook CSV format. It uses [PapaParse](https://www.papaparse.com/) to parse the CSV files and generates an output file compatible with the VoIP.ms phonebook import feature. The script supports multiple phone numbers per contact, processes labels for group assignment (e.g., "starred" or custom groups), and formats phone numbers by removing non-digit characters (except for a leading "+").

Once converted, you can upload the properly formatted phonebook to your VoIP.ms account to manage incoming calls. To use this setup with VoIP.ms:
- **Upload the Phonebook**: After conversion, upload the CSV to VoIP.ms via the phonebook import feature.
- **Set Default DID Routing**: Configure the default routing for your DID to "Hangup". This ensures calls from unknown numbers are disconnected.
- **Create Caller ID Filters**: Use group names from the phonebook (e.g., "General", "ForwardToCell") to create caller ID filters in VoIP.ms, overriding the default "Hangup" routing to destinations like voicemail or a cell phone.

## Usage

1. **Open the Script**: Launch `gmailcontacts2voipms_phonebook_csv.html` in a web browser.
2. **Upload File**: Click the "Choose File" button and select your Google Contacts CSV file.
3. **Header Option**: Check the "Include header row in output CSV" checkbox if desired.
4. **Convert**: Click the "Convert" button.
5. **Download**: The file downloads as `YYYY-MM-DD_voipms_phonebook.csv` (e.g., `2025-04-04_voipms_phonebook.csv`).

## Deploying from Git Repository

To deploy this tool directly from the GitHub repository (`https://github.com/lukejmorrison/google2voipms_csv_converter`):

1. **Clone the Repository**:
   - Open a terminal or command prompt.
   - Run:
     ```bash
     git clone https://github.com/lukejmorrison/google2voipms_csv_converter.git
     ```
   - This downloads the project to a local folder named `google2voipms_csv_converter`.

2. **Navigate to the Project**:
   - Change directory:
     ```bash
     cd google2voipms_csv_converter
     ```

3. **Run the Tool**:
   - Open `gmailcontacts2voipms_phonebook_csv.html` in a web browser (e.g., double-click the file or drag it into Chrome/Firefox).
   - The tool uses PapaParse via CDN by default, so an internet connection is required unless you configure it for offline use (see below).

4. **Optional: Offline Use**:
   - Download `papaparse.min.js` from [PapaParse CDN](https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js).
   - Save it in the project folder.
   - Edit `gmailcontacts2voipms_phonebook_csv.html` to replace:
     ```html
     <script src="https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js"></script>
     ```
     with:
     ```html
     <script src="papaparse.min.js"></script>
     ```
   - Now it runs offline.

## Contributing to the Project

If you’d like to contribute to this project by fixing bugs, adding features, or improving the code:

1. **Fork the Repository**:
   - Go to `https://github.com/lukejmorrison/google2voipms_csv_converter`.
   - Click the "Fork" button to create a copy under your GitHub account.

2. **Clone Your Fork**:
   - Clone your forked repository:
     ```bash
     git clone https://github.com/YOUR_USERNAME/google2voipms_csv_converter.git
     ```
   - Replace `YOUR_USERNAME` with your GitHub username.

3. **Create a Branch**:
   - Navigate to the project folder:
     ```bash
     cd google2voipms_csv_converter
     ```
   - Create a new branch for your changes:
     ```bash
     git checkout -b feature-or-fix-name
     ```
     (e.g., `git checkout -b add-speed-dial-support`)

4. **Make Changes**:
   - Edit files (e.g., `gmailcontacts2voipms_phonebook_csv.html`) using your preferred editor (like VS Code).
   - Test your changes by opening the updated HTML file in a browser.

5. **Commit and Push**:
   - Stage your changes:
     ```bash
     git add .
     ```
   - Commit with a descriptive message:
     ```bash
     git commit -m "Added speed dial assignment feature"
     ```
   - Push to your fork:
     ```bash
     git push origin feature-or-fix-name
     ```

6. **Submit a Pull Request**:
   - Go to your forked repository on GitHub.
   - Click "Pull requests" > "New pull request".
   - Select your branch and submit it to `lukejmorrison/google2voipms_csv_converter`’s `main` branch.
   - Describe your changes in the PR description.

7. **Collaboration**:
   - I’ll review your pull request, suggest changes if needed, and merge it once approved.

**Tips**:
- Ensure your changes align with the project’s purpose (converting Google Contacts to VoIP.ms phonebook CSV).
- Test thoroughly with sample CSVs before submitting.

## Using with VoIP.ms Caller ID Filtering

After uploading your phonebook to VoIP.ms:
1. **Default Routing**: Set your DID to "System: Hangup" in DID settings.
2. **Caller ID Filters**: In "Caller ID Filtering", create filters matching group labels (e.g., "General" to voicemail 4168384337, "ForwardToCell" to a cell phone).

See the VoIP.ms documentation: [CallerID Filtering](https://wiki.voip.ms/article/CallerID_Filtering).

## Sample CSV Files

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

To run offline:
1. Download `papaparse.min.js` from [PapaParse CDN](https://cdnjs.cloudflare.com/ajax/libs/PapaParse/5.3.0/papaparse.min.js).
2. Save it next to `gmailcontacts2voipms_phonebook_csv.html`.
3. Update HTML: `<script src="papaparse.min.js"></script>`.
4. Open `gmailcontacts2voipms_phonebook_csv.html` in a browser.

## Uploading to GitHub via VS Code

To upload to `https://github.com/lukejmorrison/google2voipms_csv_converter`:
1. Open project in VS Code.
2. Run:
   ```bash
   git init
   git add .
   git commit -m "Updated with VoIP.ms filtering"
   git remote add origin https://github.com/lukejmorrison/google2voipms_csv_converter.git
   git push -u origin main
   ```
3. **Troubleshooting**: If you get `error: src refspec main does not match any`:
   - Check branch: `git branch`
   - If on `master`, push: `git push -u origin master`
   - Or rename: `git branch -m master main`, then `git push -u origin main`
   - Ensure commits exist: `git log`

```