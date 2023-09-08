# Github
```
    https://github.com/ohmyzsh/ohmyzsh/
```  

Procure por **plugins**  
```
    https://github.com/ohmyzsh/ohmyzsh/*/plugins
```  
 
## Criação dos plugins
Criação de diretório para alocar os plugins:  
```
    mkdir -p ${HOME}/.config/zsh/plugins
```  
 
Abaixo, é realizado o redirecionamento do conteúdo de cada plugin,
para os arquivos que comportaram seu valor: 
```
 asdf.plugin.zsh    > ${HOME}/.config/zsh/plugins/asdf
                    > ${HOME}/.config/zsh/plugins/autosuggestions
 git.plugin.zsh     > ${HOME}/.config/zsh/plugins/git 
 poetry.plugin.zsh  > ${HOME}/.config/zsh/plugins/poetry 
 poetry.plugin.zsh  > ${HOME}/.config/zsh/plugins/poetry 
 themes.plugin.zsh  > ${HOME}/.config/zsh/plugins/themes 
```  

## Adição dos plugins
Dentro do:  
```
   ${HOME}/.zshrc
```  
 
Importe cada plugin:  
```
 source ${HOME}/.config/zsh/plugins/asdf
 source ${HOME}/.config/zsh/plugins/autosuggestions
 source ${HOME}/.config/zsh/plugins/git 
 source ${HOME}/.config/zsh/plugins/poetry 
 source ${HOME}/.config/zsh/plugins/vi-mode 
 source ${HOME}/.config/zsh/plugins/themes 
```  
