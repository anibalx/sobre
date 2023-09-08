# SSH GENERATE
```
  ssh-keygen -t ed25519 -C "your_email@example.com"
```

# SSH AGENTE
```
  eval "$(ssh-agent -s)"
```
```
  ssh-add ~/.ssh/id_ed25519
```

# SSH CAT AND ADD FROM GITHUB
```
  cat ~/.ssh/id_ed25519.pub
```
