# SBAHCBC Queuing System

This folder is ready to publish with GitHub Pages.

## Files

- `index.html` - the queuing system web page.
- `register.html` - the public player registration form for QR access.
- `qr.html` - a QR code helper page for the final registration link.
- `setup-online-registration.html` - step-by-step help for connecting Firebase.
- `firebase-config.js` - online database settings for registration sync.
- `.nojekyll` - tells GitHub Pages to serve the files exactly as they are.

## Publish On GitHub Pages

1. Create a new GitHub repository.
2. Upload the files from this folder to the repository root.
3. Open the repository settings.
4. Go to **Pages**.
5. Under **Build and deployment**, choose:
   - Source: **Deploy from a branch**
   - Branch: **main**
   - Folder: **/root**
6. Click **Save**.
7. GitHub will show the public website link after deployment finishes.

## Online Registration Setup

If `register.html` says online registration is not configured, that means `firebase-config.js` still contains placeholder values. The page is working, but it is blocked until a shared online database is connected.

GitHub Pages can host the screens, but it cannot store shared registration data by itself. To make QR registrations sync into the system, create a Firebase project and use Firebase Realtime Database.

1. Create a Firebase project.
2. Add a Web App inside Firebase.
3. Copy the Firebase web app config.
4. Open `firebase-config.js`.
5. Replace all `PASTE_...` placeholder values with your Firebase values.
6. In Firebase, enable **Realtime Database**.
7. For initial testing, use these database rules:

```json
{
  "rules": {
    "registrations": {
      ".read": true,
      ".write": true
    }
  }
}
```

After publishing, your player registration link will be:

```text
https://YOUR-GITHUB-USERNAME.github.io/YOUR-REPOSITORY/register.html
```

Open `qr.html`, paste that `register.html` link, and generate the QR code.

## Important Notes

- Player registration requires full name, player category, and gender.
- Online registrations are added to the system roster as `Visitor` players.
- Existing queue/session data still uses browser local storage.
- The shared online part is the registration intake. A full multi-device live queue would need the rest of the system moved into the same database.
