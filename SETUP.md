# Fernhill Garden Resident Services — setup

The repository was empty when this page was created. This adds a responsive resident service directory with a single category dropdown and contact cards. The categories are Electrician, Plumber, Gardener, Security, Dhobi / Laundry, Library, Carpenter, Housekeeping, AC Technician, Lift Maintenance, Garbage Collection and Car Washing.

## 1. Enable GitHub Pages
In the GitHub repository, open **Settings → Pages**. Choose **Deploy from a branch**, select **main** and **/(root)**, then Save. The expected site URL is https://ainn5.github.io/FGAOA/.

## 2. Configure Firebase phone OTP
1. Create a Firebase project at https://console.firebase.google.com/.
2. Add a Web app and copy its Firebase configuration.
3. In `index.html`, replace the four `PASTE_...` values in `firebaseConfig`.
4. In Firebase Authentication, enable **Phone** sign-in.
5. Add `ainn5.github.io` under Authentication → Settings → Authorized domains.
6. Enable Cloud Firestore.

Phone OTP may require Firebase billing/usage setup and applicable SMS quotas. Do not publish real contact data until access rules are installed and tested.

## 3. Install Firestore security rules
Copy `firestore.rules` into Firebase Console → Firestore Database → Rules and Publish. These rules allow active registered residents to read contacts; only an account with the Firebase custom claim `admin: true` can manage records. Do not weaken these rules to make the page work.

## 4. Add residents and contacts
Use a trusted admin process (Firebase Admin SDK or a secured admin tool) to create records. Never give residents direct write access.

- `residents/{firebase-auth-uid}`: `{ phoneNumber: "+919876543210", active: true }`
- `contacts/{document-id}`: `{ category: "Electrician", name: "Contact name", phone: "+919876543210", availability: "9 AM–6 PM", active: true }`

The resident record's phoneNumber must exactly match the verified Firebase Auth phone number. Set the custom claim `admin: true` only for trusted administrators.

## 5. Important
- The website code is deployed separately from Firebase. GitHub Pages hosts the front end; Firebase handles authentication and private contact data.
- No actual resident phone numbers or service contacts were supplied, so the directory starts with no contact records.
- Do not put private phone numbers, resident lists, Firebase Admin SDK credentials, or service-account keys in this public GitHub repository.
