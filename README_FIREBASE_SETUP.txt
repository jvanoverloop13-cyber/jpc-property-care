JPC Property Care - Firebase test build

IMPORTANT: Keep the current live app and your downloaded JSON backup. This is a separate test build, not a live deployment.

Files: index.html, manifest.json, icon.svg, sw.js, firestore.rules.

Firebase setup required before using cloud login:
1. In Firebase Console > Authentication > Sign-in method, enable Email/Password.
2. In Firestore Database > Rules, publish the contents of firestore.rules. This rule grants each signed-in user access only to /businesses/{their own Firebase UID}/private/... documents. All other paths are denied.
3. Host this build over HTTPS (GitHub Pages is HTTPS). Do not open index.html as a local file; Firebase Auth needs a web origin.
4. Test with a new account and no customer data first. Then test a second account to confirm the data is isolated.
5. When an account has no cloud data but this browser has local data, the app asks before importing. Read the prompts carefully; choose Cancel if the current data belongs to another business.

Scope/limitations:
- This initial test build syncs the app's main business data keys to one Firestore document per authenticated user. Firestore has a 1 MiB document limit. Photos and large offline maps may exceed it. If sync fails, check the on-screen cloud status and keep local backup; a production build should move photos and large offline map data to Firebase Storage or a dedicated per-user data structure. Firebase Storage may require billing.
- Theme and address lookup cache remain local to the device.
- Never publish permissive Firestore rules. Keep your backup.
