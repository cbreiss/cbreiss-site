# cbreiss.com — Personal Academic Site

Static HTML/CSS site for [cbreiss.com](https://cbreiss.com).

## Workflow

Edit files → `git commit` → `git push` → GitHub Actions deploys to DreamHost automatically.

```bash
# Make a change, then:
git add -A
git commit -m "update research section"
git push
# Done — site is live in ~30 seconds.
```

## Add your photo

Drop your photo into `assets/photo.jpg`. Then push.

## One-time setup checklist

Before the first push you need to complete the DreamHost setup:

1. **Re-add hosting for cbreiss.com** in DreamHost panel
   panel.dreamhost.com → Websites → Manage Websites → Add Hosting
   Set domain = `cbreiss.com`, webroot = `~/cbreiss.com`

2. **Enable SSH** for your DreamHost user
   panel.dreamhost.com → Users → Manage Users → edit user → set Shell = bash

3. **Generate a deploy key** (on your local machine):
   ```bash
   ssh-keygen -t ed25519 -C "github-actions-deploy" -f ~/.ssh/dreamhost_deploy
   ```

4. **Add the public key to DreamHost**
   panel.dreamhost.com → Users → Manage Users → edit user → SSH Keys
   Paste the contents of `~/.ssh/dreamhost_deploy.pub`

5. **Find your DreamHost server hostname**
   panel.dreamhost.com → Websites → Manage Websites → cbreiss.com → shows something like `hostN.dreamhost.com`

6. **Add GitHub Secrets** to this repo
   github.com → cbreiss/cbreiss-site → Settings → Secrets and variables → Actions → New secret:

   | Name | Value |
   |------|-------|
   | `DREAMHOST_SSH_KEY` | Full contents of `~/.ssh/dreamhost_deploy` (private key) |
   | `DREAMHOST_USER` | Your DreamHost username |
   | `DREAMHOST_HOST` | Your DreamHost server hostname (step 5) |

7. **Push to main** — GitHub Actions will deploy the site.

## File structure

```
index.html          main page
style.css           styling
assets/
  photo.jpg         your profile photo (you add this)
.github/
  workflows/
    deploy.yml      auto-deployment
```
