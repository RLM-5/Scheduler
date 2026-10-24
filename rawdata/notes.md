# CaseStudies2-2026.html notes

## What it does
- Name field. Submit becomes enabled once a name is entered.
- On blur / change of name: if a document with that name exists in Firestore, loads the previously selected cases and times.
- Case study checkboxes (A–G) with notes for D and F.
- Time slot checkboxes inferred from the GMTP case study lock blocks in the W45 and W46 calendar screenshots (mix of 60 and 75 min).
- Two Submit buttons (top and bottom) both save the current selection to Firestore (document ID = name).
- Two Copy buttons (clipboard pictogram) copy a plain-text summary (name + selected cases + selected times) to the clipboard.

## Firebase
- Uses Firebase JS SDK (compat) via CDN.
- Collection: `caseStudies2_2026`
- Document ID: the entered name
- Fields: name, cases (array of ids), times (array of ids), updatedAt

## Before it works
You must:
1. Create a Firebase project (Europe region for Firestore).
2. Create a Firestore database in production mode.
3. Set rules to open (anyone can read/write):
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /{document=**} {
         allow read, write: if true;
       }
     }
   }
   ```
4. Get the web app config and replace the placeholder `firebaseConfig` object in the HTML.

## Times inferred
From the calendar screenshots (GMTP case study lock, bluish):
- Mon 2 Nov 08:45–10:00, 12:00–13:15
- Thu 5 Nov 08:45–10:00, 11:00–12:00, 12:00–13:00, 13:15–14:30, 14:30–15:45
- Fri 6 Nov 08:45–10:00
- Mon 9 Nov 08:45–10:00, 12:45–14:00

Adjust the `times` array in the HTML if the exact end times differ.
