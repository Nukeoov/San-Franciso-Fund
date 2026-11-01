# Our Little Getaway — San Francisco travel fund ✈

A responsive two-page website: Overview + Contributions. All amounts are USD.

## What's included
- Animated routes: Houston → San Francisco and Daytona Beach → San Francisco.
- Savings progress bar, current balance / target, and six editable expense estimates.
- Add a deposit or withdrawal with person, date, amount, and note.
- Delete incorrect entries with confirmation; totals recalculate automatically.
- Real-time synchronization **when Firebase is configured**.
- Demo mode using browser localStorage if Firebase is not configured (**NOT shared across devices**).

## Quick demo
Open the project with a local server, e.g. VS Code Live Server, or run `python -m http.server 8000` in this folder and visit http://localhost:8000. The demo saves only in that browser.

## Set up real-time sharing (Firebase, free tier available)

1. Go to https://console.firebase.google.com/ → Create a project.
2. From Project settings → Your apps → Add Web app (`</>`). Copy the **firebaseConfig** object values into `firebase-config.js`.
3. In **Build → Authentication → Sign-in method**, enable **Email/Password** (not anonymous sign-in).
4. In **Authentication → Users**, manually add **two users**: your email and your girlfriend's email. Set strong, separate passwords. You can use your real emails; password reset is supported by Firebase if enabled and configured, although this template has no reset form.
5. In **Build → Firestore Database**, create a database in production mode. Choose a region close to users.
6. Open `firestore.rules`, replace `YOUR_EMAIL@gmail.com` and `PARTNER_EMAIL@gmail.com` with the **exact two account email addresses**, then copy the rules to Firestore Database → Rules and **Publish**. Do not leave the placeholder emails or allow public writes.
7. Deploy the files as a static website, for example to GitHub Pages. In Firebase Console → Authentication → Settings → Authorized domains, add your exact GitHub Pages domain if needed (e.g. `nukeoov.github.io`). Do not include `https://` or a repository path.
8. Both of you open the same website and sign in with your **own accounts**. You can now add/remove transactions from either phone, and both screens update immediately while online.

### GitHub Pages deployment
Upload `index.html`, `style.css`, `app.js`, `firebase-config.js` to your own repository (root folder). In **Settings → Pages**, choose **Deploy from a branch**, select `main` and `/ (root)`; the site URL will typically be `https://YOUR_USERNAME.github.io/REPOSITORY_NAME/`.

### Important security notes
- Firebase web config (`apiKey`, etc.) is **public client configuration** and can be committed; it is **not an admin/service account secret**. Security depends on Authentication + correctly published Firestore rules.
- Do **not** put GitHub personal access tokens, service account keys, private API keys, or your passwords in the repo.
- `firestore.rules` is included as a template; GitHub Pages does not automatically deploy the rules. You must publish them inside Firebase.
- Use **private/unique passwords** and keep Firebase account access secure. The two allowed email identities are configured in rules.
- This is a voluntary savings tracker, **not a bank account** and does not move real funds.
- If amounts are sensitive, avoid publishing transaction data anywhere except the access-controlled Firestore database.
- If you change Firebase configuration and the site still looks like a demo, refresh the page (and check browser console for errors).

### Data structure
- `trips/san-francisco` stores an array `budget`.
- `trips/san-francisco/entries/{auto-id}` stores `type`, `amount`, `date`, `person`, `note`, `createdAt`.
- Total deposits − withdrawals = current savings. Target = sum of six budget lines. Deleting an entry reverses its effect.

### Editing names
The `Who?` drop-down currently offers `Me` and `My girlfriend`. To personalize these labels, change the `<option>` text and values in `transactionModal()` in `app.js`. Existing transactions retain the names saved at the time.
