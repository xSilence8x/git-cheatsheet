# git-cheatsheet

Vytažení konkrétního souboru z main větve
```
# Nejprve fetchni aktuální stav z remote
git fetch origin

# Pak vytáhni konkrétní soubor z origin/main
git checkout origin/main -- cesta/k/souboru.txt
```
Nebo moderněji
```
git fetch origin
git restore --source=origin/main -- cesta/k/souboru.txt
```
Případně více souborů lze vytáhnout jako příkaz
```
git restore --source=origin/main -- cesta/ke/slozce/
```
Tím se soubor překopíruje do aktuální např. dev větve jako unstaged změna.

## Git flow
Stav dev větve
```
git status
git diff
```

```
git checkout dev
git pull origin dev          # synchronizuj s remote
```

Uložení práce na dev větvi a nová feature větev
```
# Ulož rozdělanou práci stranou
git stash

# Vytvoř feature větev z dev
git checkout -b feature/split-settings

# Obnov změny
git stash pop
```

Commity
```
git add settings/
git commit -m "feat: split settings into base, dev, prod"
# Před mergem pushni feature větev na remote
git push origin feature/split-settings
```

Hotová feature jde zpět do dev větve
```
git checkout dev
git merge --no-ff feature/split-settings   # --no-ff zachová historii feature
git push origin dev
# smaž větev lokálně i na remote
git branch -d feature/split-settings
git push origin --delete feature/split-settings     
```

Release do produkce
```
git checkout main
git merge --no-ff dev
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin main --tags
```

Merge do main větve na locale
```
git checkout dev
git merge --no-ff feature/split-settings
git push origin dev
```
Nebo na Githubu přes Pull Request

Lokálně pak sync
```
git checkout main
git pull origin main
```

## Graf a historie větví
URL:
```
github.com/<username>/<repo>/network
```
