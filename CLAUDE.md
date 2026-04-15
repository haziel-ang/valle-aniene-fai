# Valle dell'Aniene — FAI

## Workflow Git

- Sviluppa sempre su un branch dedicato (es. `claude/...`)
- Dopo aver pushato tutte le modifiche, esegui sempre il **merge in `main`** e push
- Sequenza standard:
  ```
  git checkout main
  git pull origin main --rebase
  git merge <branch> --no-ff
  git push -u origin main
  ```
