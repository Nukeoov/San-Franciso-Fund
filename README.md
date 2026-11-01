# San Francisco Travel Fund — GitHub Pages version

This website reads expenses and transaction history from `data.json` in your GitHub repository. Only the GitHub repository owner can unlock the editing UI with a personal access token that has write access. Every addition, deletion, or budget edit commits the updated `data.json` directly to your repo. No Firebase or server is required.

## Installation
1. Extract the ZIP. Upload **all files** to your repo's root directory (including `data.json`). Do not upload the containing folder.
2. In repository Settings > Pages, select **Deploy from a branch**, `main`, `/(root)`; save.
3. Visit `https://YOUR_USERNAME.github.io/YOUR_REPO/`. The site auto-detects the username and repo from the URL.
4. For a custom domain or local preview, set `owner` and `repo` in `github-config.js`.
5. The repository MUST be public for visitors to see the shared fund without a token. **Do not put private personal or financial information in transaction notes**; all saved information is public and appears in repository history.

## Owner-only edit setup
1. GitHub > Settings > Developer settings > Personal access tokens > **Fine-grained tokens** > Generate new token.
2. Under Resource owner select **your own GitHub account**, grant **only the trip-fund repository** access.
3. Repository permissions: **Contents: Read and write**. All other permissions: no additional access.
4. Create token, copy it securely. Never paste it into any file or commit, chat, screenshot, or public page. A short expiry is preferable; create another token when it expires.
5. Open your website, click **Owner login**, paste the token. Click unlock. You can now edit the budget and transactions; edits commit to `data.json` on the `main` branch.
6. Click **Lock editing** when finished, or close the tab. The token is held only in this tab's sessionStorage (not in the Git repository). Avoid logging in on public/shared computers.

GitHub checks token write permissions, not just the visible login button. For enhanced security, you can use a dedicated private backend and GitHub App OAuth instead; browser-issued personal access tokens can be exposed by malicious browser extensions or an XSS vulnerability, so use only a restricted token.

## Important limitations
- If GitHub Pages uses `gh-pages` or another branch, update `branch` in `github-config.js` to match the data branch and grant write permission accordingly.
- GitHub API caching and Pages deployment can introduce a brief delay. Reload after changes on another device.
- Changes create public commits; deleted transactions remain in Git history.
- If the repo's main branch is protected or requires approvals, direct commits will fail.
- To change the two names shown in the form, edit the two `<option>` elements in `app.js` once.
- Browser file:// preview cannot auto-detect repo; configure `github-config.js` and preview via a local server.
