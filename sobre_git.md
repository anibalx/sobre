# CRIAR REPOSITÓRIO NUMA LINHA
> OBS: origin = nome local do repositório
```sh 
		mkdir diretório &&\
    cd diretório &&\
    git init &&\
    echo "Meu commit" > README.md &&\
    git add README.md &&\
    git commit -m "Apenas um teste" &&\
    git push -u git@gitlab.com:usuário/diretório.git master
```

# CRIAR REPOSITÓRIO LOCAL POR: HTTPS
### Cria repositório (GitLab)
```sh
		git init
		git add "ARQUIVO"
		git commit -m "MENSAGEM REFERENTE AO QUE SERÁ COMITADO"
		git push --set-upstream https://gitlab.com/usuario/repositório.git master 
```
																	ou 
### Cria repositório (GitLab)
```sh
		git init
		git add "ARQUIVO"
		git commit -m "MENSAGEM REFERENTE AO QUE SERÁ COMITADO"
		git push -u origin https://gitlab.com/usuario/repositório.git HEAD:master 
```

### Ex de criação de repositório remoto localmente (GitLab e GitHub):	
```sh
		git push -u origingitlab https://gitlab.com/usuario/repositório.git master
		git push -u origingithub https://github.com/usuario/repositório.git master
```

##	ADICIONA REPOSITÓRIO REMOTO LOCALMENTE (GitLab)
```sh
		git remote add origin https://gitlab.com/usuario/repositório.git master 
```
### Ex de adição de repositório remoto localmente (GitLab e GitHub):	
```sh
	 git remote add origingitlab https://gitlab.com/usuario/repositório.git master
	 git remote add origingithub https://github.com/usuario/repositório.git master
```


# CRIAR REPOSITÓRIO LOCAL POR: SSH 
> uma vez que a chave pública tenha sido adicionada ao repositório online e 
a chave privada locamente na máquina do usuário
### Cria repositório (GitLab)
```sh
		git init
		echo "teste" > README.md
		git add README.md
		git commit -m "teste"
		git remote -v
		git push --set-upstream git@gitlab.com:usuario/repositório.git master
```
																	ou 
### Cria repositório (GitLab)
```sh
		git init
		echo "teste" > README.md
		git add README.md
		git commit -m "teste"
		git remote -v
		git push -u origin git@gitlab.com:usuario/repositório.git master 
```
### Ex de criação de repositório remoto localmente (GitLab e GitHub):	
```sh
	 git push -u origingitlab git@gitlab.com:usuario/repositório.git master 
	 git push -u origingithub git@github.com:usuario/repositório.git master 
```

##	ADICIONA REPOSITÓRIO REMOTO LOCALMENTE (GitLab)
```sh
		git remote add origin git@gitlab.com:usuario/repositorio.git master
```
### Ex de adição de repositório remoto localmente (GitLab e GitHub):	
```sh
	 git remote add origingitlab git@gitlab.com:usuario/repositorio.git
	 git remote add origingithub git@github.com:usuario/repositorio.git master
```


# MODIFICAR REPOSITÓRIO REMOTO LOCALMENTE:
## HTTPS:	
```sh
		git remote set-url origin https://gitlab.com/usuario/repositório.git
		git remote set-url origin https://github.com/usuario/repositório.git
```

## SSH:
```sh
		git remote set-url origin git@gitlab.com/usuario/repositório.git
		git remote set-url origin git@github.com/usuario/repositório.git
```


# ENVIAR PUSH DE UMA BRANCH LOCAL PARA A MASTER, NUM REPOSITÓRIO REMOTO
```sh
		git push -u git@gitlab.com:usuário/diretório.git nome_da_branch_local:master
		git push -u git@gitlab.com:usuário/diretório.git HEAD:master
		git push -u git@gitlab.com:usuário/diretório.git HEAD
```


# ACEITAR PULL REQUEST LOCALMENTE
```sh
		git fetch -pt
		git diff master..nome_da_branch_local
		git merge master nome_da_branch_local
		git push -u origin
```
	

# TAG - COLOQUE UMA TAG NO COMMIT
```sh
    git tag
    git tag <TAG> # tipo leve: apenas checksum de commit armazenando em um arquivo
    git tag -a <TAG> # tipo anotada
    git tag -a <TAG> -m "<MENSAGEM>"
    git tag -a <TAG> <CHECKSUM_FROM_COMMIT>
```


# CONFIG - CONFIGURE O GIT LOCALMENTE
```sh
    git config --global alias.co checkout # $ git co 
    git config --global alias.br branch   # $ git br
    git config --global alias.ci commit   # $ git ci
    git config --global alias.st status   # $ git st
```


# CONFIG - CONFIGURE O GIT USER LOCALMENTE
```sh
    git config --global user.name "<USER>"
    git config --global user.email "<EMAIL_USER"
```


# REMOTE - ADICIONA REPOSITÓRIO REMOTO LOCALMENTE (EXEMPLO GENÉRICO)
```sh
    git remote add <REPO_LOCAL> git@git<hub | lab>.com:<USER>/<REPO_EXTERNO>.git
    git remote rename <REPO_LOCAL_ANTIGO_NOME> <REPO_LOCAL_NOVO_NOME>
    git remote
```


# RESTORE - RESTAURE ARQUIVOS
```sh
    git restore <ARQUIVO> <ARQUIVO> ...
```


# DIFF - DIFERENCIE ARQUIVOS
```sh
    git diff <NÚMERO_DA_BRANCH> <NÚMERO_DA_BRANCH>
    git diff 9f89fcd 55f5924
    git diff HEAD~19 HEAD^^
    git diff <ARQUIVO> <ARQUIVO>
    git difftool
    git diff 
```


# RM - REMOVA ARQUIVOS
```sh
    git rm <ARQUIVO> <ARQUIVO> ...
```


# LOG - MOSTRE O LOG DO REPOSITÓRIO
```sh
    git log --oneline
    git log
```


# BRANCH - LIDA COM OS BRANCHES
```sh
    git branch <BRANCH_A_SER_CRIADA>       # crie uma branch
    git branch -d <BRANCH_A_SER_DELETADA>  # delete a branch
    git branch -m <NOVO_NOME_DA_BRANCH>    # renomeie a branch
    git branch
    git branch -l                          # liste as branchs
```


# CHECKOUT - CRIA NOVA BRANCH
```sh
    git checkout -b <NOVA_BRANCH>
    git checkout -B <NOVA_BRANCH>  # -B == cria, senão existir
```

# CHECKOUT - TROCA AS BRANCHES
```sh
    git checkout <BRANCH_A_SE_MOVER>
    git checkout-index
```


# STATUS - MOSTRAS AS INFORMAÇÔES SOBRE UM REPOSITÓRIO
```sh
    git status -h
    git status -s
    git status -b
    git status -sb
```


# CHECK - MOSTRA OS ATRIBUTOS DE UM REPOSITÓRIO
```sh
    git check-mailmap
    git check-attr
    git check-attr -a
```


# LS - MOSTRA A ÁRVORE DE ARQUIVO
```sh
    git ls-files

    git ls-remote

    git ls-tree -h
    git ls-tree -d <NOME_DA_BRANCH>
    git ls-tree -r <NOME_DA_BRANCH>
    git ls-tree -t <NOME_DA_BRANCH>
    git ls-tree -l <NOME_DA_BRANCH>
```


# BLAME - MOSTRA A ÚLTIMA MODIFICAÇÂO
```sh
    git blame
    git blame --show-name <ARQUIVO>
    git blame --show-name --color-by-age <ARQUIVO>
```


# NOTES - MOSTRA AS NOTES REFERENTES AO REPOSITÓRIO
```sh
    git notes
    git notes list
    git notes show
```


# COMMIT - ADICIONA INFORMAÇÔES DO REPOSITÓRIO
```sh
    git commit -m "<MENSAGEM>"
    git commit-tree
    git commit-graph
```


# SHOW - MOSTRA VÁRIAS INFORMAÇÔES SOBRE REPOSITÓRIO
```sh
    git show-branch
    git show-index
    git show-ref
```


# RANGE-DIFF - MOSTRA AS DIFERÊNÇAS ENTRE OS INTERVALOS DE COMMITS
```sh
    git range-diff 9f89fcd 7da234c
    git range-diff 9f89fcd
```


# PUSH - ATUALIZA REPOSITÓRIO REMOTO
```sh
    git push
    git push originlab
    git push
    git push --set-upstream originlab origin
    git push --set-upstream originlab
    git push origin <TAG> # envia tag para server online
```


# INIT - INICIALIZAÇÃO DE REPOSITÓRIO
```sh
git init --bare
git init
```


# FETCH - DOWNLOAD DE OUTROS REPOSITÓRIOS
```sh
git fetch 
```


# REBASE - RETORNE NO COMMITS
```sh
git rebase
```

		
# REFERÊNCIAS:
[Atlassian Tutorials](https://www.atlassian.com/br/git/tutorials)
[Help Github - Adddins an Existing Project to Github Using The Command Line](https://help.github.com/pt/github/importing-your-projects-to-github/adding-an-existing-project-to-github-using-the-command-line)
[Coderwall - Create New Github Repo from command Line](https://coderwall.com/p/mnwcog/create-new-github-repo-from-command-line)
[Hub Create](https://hub.github.com/hub-create.1.html)
[Git Docs - Push](https://git-scm.com/docs/git-push)
[Stackoverflow - Remote Already Exists on Git Push to a New Repository](https://stackoverflow.com/questions/1221840/remote-origin-already-exists-on-git-push-to-a-new-repository)
[Snippets from Gitlab](https://gitlab.com/snippets/1975567)
[Blog da 2k - Manter Repositorio Github Forkado Sincronizado com o Original](https://blog.da2k.com.br/2014/01/19/manter-repositorio-github-forkado-sincronizado-com-o-original/)
[Blog da 2k - Git e Github do Clone ao Pull Request](https://blog.da2k.com.br/2015/02/04/git-e-github-do-clone-ao-pull-request/)
[Stackoverflow - Tem como aceitar um Pull Request Localmente via terminal ou Github desktop](https://pt.stackoverflow.com/questions/426095/tem-como-aceitar-um-pull-request-localmente-via-terminal-ou-github-desktop)
[lut/EvolutionApp.git](https://github.com/lut/EvolutionApp.git)
[Stackoverflow - Warning Permanently Addded The RSA Host Key For IP Address](https://translate.googleusercontent.com/translate_c?depth=1&hl=pt-BR&prev=search&pto=aue&rurl=translate.google.com&sl=en&sp=nmt4&u=https://stackoverflow.com/questions/18711794/warning-permanently-added-the-rsa-host-key-for-ip-address&usg=ALkJrhjmBnIFUtvgGN5Mkw6zgZ4uDglHzw)
