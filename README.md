# My Money — Personal Finance Dashboard

A static INR financial dashboard for tracking family salary and expenses, individual EMIs, recurring commitments, chit groups, and peer-to-peer lending records.

## What's included

- Salary income entered person/source by person/source for each month.
- Individual EMI schedules with monthly amount, total tenure, installments paid, and installments remaining.
- Separate recurring fixed commitments, including chit payments, with remaining periods.
- Editable monthly expense budget headings and expense tracking.
- Chit business groups, members, collections, payouts, and expenses.
- Lending principal, variable monthly interest, interest receipts, and principal repayments.
- Local JSON export/import backup.
- Firebase Authentication and private per-user Cloud Firestore sync.

## Run locally

Use a local web server (recommended for Firebase Auth):

```bash
python -m http.server 8080
```

Open http://localhost:8080.

## Firebase setup

The supplied Firebase Web App config is already pre-filled in `index.html`. It is client-side configuration, not a service-account credential.

1. In Firebase Console, open project **myfinance-99e7a**.
2. Go to **Authentication → Sign-in method** and enable **Email/Password**.
3. Go to **Firestore Database** and create a database.
4. Publish the rules from `firestore.rules` in **Firestore Database → Rules**.
5. Open the dashboard and go to **Settings & backup → Firebase cloud sync**.
6. For the first use, enter an email/password and choose **Create account & sync**. For subsequent devices, use **Connect & sync** with the same account.
7. If using GitHub Pages, add the published Pages hostname (for example, `dineshdanny01.github.io`) in **Authentication → Settings → Authorized domains** if Firebase requires it.

The app stores the full dashboard state at:

`users/{Firebase Authentication UID}/dashboard/main`

The Firestore rules allow each signed-in user to read and write only their own document. Never use a Firebase service-account JSON or private key in this browser app or repository.

## Deploy with GitHub Pages

1. In this repository, open **Settings → Pages**.
2. Select **GitHub Actions** as the build and deployment source.
3. Pushes to `main` will run `.github/workflows/deploy.yml`.
4. Open the Pages URL shown under **Settings → Pages** after the workflow succeeds.

This repository is private. GitHub Pages for private repositories depends on the GitHub plan and repository settings. If Pages is unavailable for this private repository, make it public only if you are comfortable exposing the application source, or use another static host.

## Data and privacy notes

- The repository contains application source and rules only. Do not commit financial records, JSON backups, passwords, or service-account keys.
- Financial records are stored locally in the browser and are copied to Firestore only after a successful Firebase sign-in.
- The application password is used to sign in and is not saved by the dashboard.
- Download regular JSON backups. The current design stores one Firestore document per user; Firestore documents have a 1 MiB size limit.
- Firebase project configuration (including the Web API key) is expected to be visible in a client app. Access control must be enforced by Authentication and Firestore Security Rules.
