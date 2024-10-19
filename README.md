# dotfiles

My personal collection of dotfiles, managed by chezmoi

## Apply dotfiles

Run this command to download dotfiles from this repo using chezmoi:

```
sh -c "$(curl -fsLS get.chezmoi.io)" -- init --apply Andistar12
```

## Updating dotfiles

```
chezmoi cd
git add .
git commit -m "Commit message"
git push -u origin main
```
