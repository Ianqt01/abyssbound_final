ABYSSBOUND — Firebase Email Verification

This package keeps the existing ABYSSBOUND home screen and gameplay design. The account backend is changed to Firebase Authentication + Cloud Firestore, and email verification is required before entering the realm.

FILES
- index.html — game with Firebase auth/save and email verification flow
- config.js — paste your Firebase Web App configuration here
- firestore.rules — Firestore security rules

FIREBASE CONSOLE SETUP
1. Create/open your Firebase project.
2. Authentication > Sign-in method > enable Email/Password.
3. Authentication > Settings > Authorized domains: add the domain where you host ABYSSBOUND. For local testing, use a local web server rather than file:// when possible.
4. Authentication > Templates > Email address verification: customize the sender/name/subject/body if desired.
5. Firestore Database: create the database.
6. Publish firestore.rules.
7. Project settings > Your apps > Web app: copy the Firebase config into config.js.

EMAIL VERIFICATION FLOW
Registration:
Create Account -> Firebase account -> Firestore player document -> verification email -> verification screen.

Verification screen:
- RESEND EMAIL sends Firebase's verification email again.
- I'VE VERIFIED MY EMAIL reloads the Firebase user and checks emailVerified.
- The player cannot enter the game until emailVerified is true.
- BACK TO LOGIN signs out and returns to the login screen.

LOGIN FLOW
If an existing account has not verified its email, login opens the same verification screen instead of entering the game.

PASSWORD RESET
Forgot Password uses Firebase Authentication's password reset email.

FIRESTORE DATA
Collection: players
Document ID: Firebase Authentication UID
Fields include username, email, selectedHero, data, createdAt, updatedAt.

IMPORTANT
Do not put a service-account private key in config.js. The Firebase Web App config is intended for client-side use; security comes from Authentication and Firestore Security Rules.

CUSTOM 6-DIGIT CODE
This version uses Firebase's standard verification link. Firebase's normal email/password verification flow does not provide a built-in 6-digit verification code. A custom code would require a trusted backend to generate, store, expire, and email the code.
