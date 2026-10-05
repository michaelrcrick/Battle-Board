# Sales Battle Board – Secure Config Version

Multi-user sales race board with Admin / Editor / Viewer roles.  
Firebase config is injected at build time via GitHub Secrets (not stored in the repository).

---

## How the secure config works

- The real Firebase keys live only in **GitHub Secrets**
- On every push, GitHub Actions replaces the placeholders in `index.html`
- The final live site has the real keys, but they never appear in your repository source code

> Note: The keys are still visible in the browser (this is unavoidable with client-side Firebase).  
> The benefit is that they are **not** in your GitHub repo history.

---

## Setup Instructions

### 1. Create the repository and upload files

1. Create a new **public** repository on GitHub
2. Upload these files:
   - `index.html`
   - `README.md`
   - `.github/workflows/deploy.yml`

### 2. Add GitHub Secrets

1. Go to your repository → **Settings** → **Secrets and variables** → **Actions**
2. Click **New repository secret** and add each of these one by one:

| Secret Name                      | Value                                              |
|----------------------------------|----------------------------------------------------|
| `FIREBASE_API_KEY`               | `AIzaSyBNMWBYrKK5VplJ_bzxu58Vm3LnoYFKGMI`         |
| `FIREBASE_AUTH_DOMAIN`           | `battle-board-38608.firebaseapp.com`               |
| `FIREBASE_PROJECT_ID`            | `battle-board-38608`                               |
| `FIREBASE_STORAGE_BUCKET`        | `battle-board-38608.firebasestorage.app`           |
| `FIREBASE_MESSAGING_SENDER_ID`   | `508059065368`                                     |
| `FIREBASE_APP_ID`                | `1:508059065368:web:6cb6236462650dfd73f76d`        |

### 3. Enable GitHub Pages (Actions method)

1. Go to **Settings → Pages**
2. Under **Build and deployment** → **Source**, choose **GitHub Actions**
3. Save

### 4. Trigger the first deploy

- Either push a small change, or
- Go to the **Actions** tab → select **Deploy to GitHub Pages** → **Run workflow**

After 1–2 minutes your site will be live at:  
`https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/`

---

## Firebase requirements (same as before)

- Authentication → Email/Password enabled
- Firestore created
- Security Rules published (see previous instructions)

---

## Local testing

Because the placeholders are still in the file, the board will **not** work if you just open `index.html` locally.  
It only works after GitHub Actions injects the real values during deployment.
