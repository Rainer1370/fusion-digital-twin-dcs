# Publishing Guide

## Recommended: separate public repository

Create a new empty GitHub repository named `fusion-digital-twin-dcs`, then run:

```bash
cd ~/git
unzip ~/Downloads/fusion-digital-twin-public.zip
mv fusion-digital-twin-public fusion-digital-twin-dcs
cd fusion-digital-twin-dcs

git init
git branch -M main
git add -A
git commit -m "Publish fusion digital twin DCS technical preview"
git remote add origin git@github.com:Rainer1370/fusion-digital-twin-dcs.git
git push -u origin main
```

If your GitHub remote uses HTTPS, replace the `git@github.com:...` address with the HTTPS address shown by GitHub.

## Do not publish the uploaded source repository in place

Changing an existing private repository to public, or deleting files in a new commit, can leave earlier sensitive content in Git history. The curated package was designed to begin with clean public history.

## Before publishing

1. Review `README.md`, `ARTICLE.md`, and the architecture diagram.
2. Confirm the email address and intended GitHub repository name.
3. Decide whether any patent filing should occur before public disclosure.
4. Keep the original full engineering repository private.
