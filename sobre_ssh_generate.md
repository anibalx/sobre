# SSH GENERATE
```sh
  ssh-keygen -t ed25519 -C "your_email@example.com"
```  

# SSH AGENTE
```sh
  eval "$(ssh-agent -s)"
```  

```sh
  ssh-add ~/.ssh/id_ed25519
```  

# SSH CAT AND ADD FROM GITHUB
```sh
  cat ~/.ssh/id_ed25519.pub
```  
