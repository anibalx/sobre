# PREFIXO
```sh
CTRL+b
```  

---

# MENU
```sh
tmux list-keys
tmux list-keys -N
CTRL+b ?
```  

---

# PROMPT PARA ENVIAR COMANDOS
```sh
CTRL+b :
```  

---

# SESSÃO
## LISTAR SESSÕES
```sh
tmux list-sessions
```  

> OU

```sh
tmux ls
```  

## CRIA (NOVA) SESSÂO:
```sh
tmux new-session
```  

> OU

```sh
tmux new
```  

## CRIA (NOVA) SESSÂO (COM NOME, NOMEADA):
```sh
tmux new-session -s <NOME DA SESSÂO>
```  

> OU

```sh
	tmux new -s <NOME DA SESSÂO>
```  

### EX 0:
```sh
tmux new -s sessao
```  

### EX 1:
```sh
tmux new -s "sessao"
```  

## CRIA (NOVA) SESSÂO (COM NOME, NOMEADA) (NÂO ENTRA NELA):
```sh
tmux new-session -d -s <NOME DA SESSÂO>
```  

> OU

```sh
tmux new -d -s <NOME DA SESSÂO>
```  

### EX 0
```sh
tmux new -d -s sessao
```  

### EX 1
```sh
tmux new -d -s "sessao"
```  


## CRIA (NOVA) SESSÂO e JANELA (AMBAS COM NOME, NOMEADAS):
```sh
tmux new-session -s <NOME DA SESSÂO> -n <NOME DA JANELA>
```  

### EX 0
```sh
tmux new -s sessao -n janela
```  

### EX 1
```sh
tmux new -s "sessao" -n janela
```  

### EX 2
```sh
tmux new -s sessao -n "janela"
```  

### EX 3
```sh
tmux new -s "sessao" -n "janela"
```  

## CRIA (NOVA) SESSÂO e JANELA (AMBAS COM NOME, NOMEADAS) (NÂO ENTRA NELA):
```sh
tmux new-session -d -s <NOME DA SESSÂO> -n <NOME DA JANELA>
```  

### EX 0
```sh
tmux new -d -s sessao -n janela
```  

### EX 1
```sh
tmux new -d -s "sessao" -n janela
```  

### EX 2
```sh
tmux new -d -s sessao -n "janela"
```  

### EX 3
```sh
tmux new -d -s "sessao" -n "janela"
```  

## CRIA (NOVA) SESSÂO DE DENTRO DE UMA SESSÃO JÁ UTILIZADA
```sh
tmux new-session -d -s nova_sessao
```

## CRIA (NOVA) SESSÂO e (NOVAS) JANELAS (TODAS COM NOME):
```sh
tmx () {
  # Use -d to allow the rest of the function to run
  tmux new-session -d -s SessionName
  tmux new-window -n Win1
  # -d to prevent current window from changing
  tmux new-window -d -n Win2
  tmux new-window -d -n Win3
  tmux new-window -d -n Win4
  # -d to detach any other client (which there shouldn't be,
  # since you just created the session).
  tmux attach-session -d -t SessionName
}
```  

### EX em .zshrc:
```sh
tmx () {
  # Use -d to allow the rest of the function to run
  tmux new-session -d -s "sheracu" -n "Música"
  # -d to prevent current window from changing
  tmux new-window -d -n "Rust"
  tmux new-window -d -n "Julia"
  tmux new-window -d -n "Python"
  tmux new-window -d -n "Golang"
  tmux send-keys -t "sheracu:Música" "lf" ENTER
  tmux source "${HOME}/.tmux.conf.local"
  # -d to detach any other client (which there shouldn't be,
  # since you just created the session).
  tmux attach-session -d -t "sheracu"
}
```  

## NAVEGAR ENTRE SESSÕES (LISTA DE SESSÕES):
```sh
CTRL+b s
```  

## NAVEGAR ENTRE SESSÕES:JANELAS (LISTA DE SESSÕES:JANELAS):
```sh
CTRL+b w
```  

## MUDAR NOME (RENOMEAR) DA SESSÃO ($ = SHIFT+4):
```sh
CTRL+b $
```  
        
## ENVIA TECLAS:
```sh
tmux send-keys -t <SESSÃO>:<JANELA>.<PAINEL> <TECLAS A ENVIAR>
```  
        
### EX 0:  
```sh
tmux send-keys -t sessao Olá, mundo!
```

### EX 1:  
```sh
tmux send-keys -t "sessao" Olá, mundo!
```

### EX 2:  
```sh
tmux send-keys -t sessao "Olá, mundo!"
```

### EX 3:  
```sh
tmux send-keys -t "sessao" "Olá, mundo!"
```

### EX 4:  
```sh
tmux send-keys -t sessao:0 Olá, mundo!
```

### EX 5:  
```sh
tmux send-keys -t "sessao:0" Olá, mundo!
```

### EX 6:  
```sh
tmux send-keys -t sessao:0 "Olá, mundo!"
```

### EX 7:  
```sh
tmux send-keys -t "sessao:0" "Olá, mundo!"
```

### EX 8:  
```sh
tmux send-keys -t minha_sessao:bash Olá, mundo!
```

### EX 9:  
```sh
tmux send-keys -t "minha_sessao:bash" "Olá, mundo!"
```

### EX 10: 
```sh
tmux send-keys -t "0:1" "olá, mundo"
```

## ENVIA COMANDOS:
```sh
tmux send-keys -t <SESSÃO>:<JANELA>.<PAINEL> <COMANDO> ENTER
```  

### EX 0:
```sh
tmux send-keys -t sessao ls ENTER
```  

### EX 1:
```sh
tmux send-keys -t sessao "ls" ENTER
```  

### EX 2:
```sh
tmux send-keys -t sessao ls "ENTER"
```  

### EX 3:
```sh
tmux send-keys -t "sessao" "ls" ENTER
```  

### EX 4:
```sh
tmux send-keys -t "sessao" "ls" "ENTER"
```  

### EX 5:
```sh
tmux send-keys -t sessao:janela ls ENTER
```  

### EX 6:
```sh
tmux send-keys -t "sessao:janela" ls ENTER
```  

### EX 7:
```sh
tmux send-keys -t sessao:janela "ls" ENTER
```  

### EX 8:
```sh
tmux send-keys -t sessao:janela ls "ENTER"
```  

### EX 9:
```sh
tmux send-keys -t "sessao:janela" "ls" "ENTER"
```  

### EX 10:
```sh
tmux send-keys -t sessao:janela.painel ls ENTER
```  

### EX 11:
```sh
tmux send-keys -t "sessao:janela.painel" ls ENTER
```  

### EX 12:
```sh
tmux send-keys -t sessao:janela.painel "ls" ENTER
```  

### EX 13:
```sh
tmux send-keys -t sessao:janela.painel ls "ENTER"
```  

### EX 14:
```sh
tmux send-keys -t "sessao:janela.painel" "ls" "ENTER"
```  

### EX 15:
```sh
tmux send-keys -t "0:0.0" "ls" "ENTER"
```  

## SAIR DE SESSÃO (MANTÉM SESSÃO VIVA):
```sh
CTRL+b d
```  
	
## ENTRAR (RETORNAR) PARA A SESSÃO:
```sh
tmux attach-session -t <NOME DA SESSÃO>
```  

### EX 0:
```sh
tmux attach-session -t sessao
```  

### EX 1:
```sh
tmux attach-session -t "sessao"
```  

### EX 2:
```sh
tmux attach-session -t "minha_sessao"
```  

### EX 3:
```sh
tmux attach -t sessao
```  

## MATA (MATAR, APAGAR, DELETAR) SESSÃO
```sh
tmux kill-session -t <SESSÃO>
```  

> OU

```sh
tmux kill-session -t <SESSÃO>:<JANELA>.<PAINEL>
```  

### EX 0:
```sh
tmux kill-session -t sessao
```  

### EX 1:
```sh
tmux kill-session -t sessao:janela.painel
```  

### EX 2:
```sh
tmux kill-session -t "sessao:janela.painel"
```  

### EX 3:
```sh
tmux kill-session -t 0:0.0
```  

### EX 4:
```sh
tmux kill-session -t "0:0.0"
```  

---

# JANELA
## LISTAR JANELAS:
```sh
tmux list-window
```  

## CRIA JANELA:
```sh
tmux neww
```  

> OU

```sh
CTRL+b c
```  

## CRIA JANELA (COM NOME):
```sh
CTRL+b , <NOME DA JANELA>
```  

> OU

```sh
tmux neww -n "<NOME DA JANELA>"
```  

## CRIA JANELA NO DIRETÓRIO ATUAL:
```sh
bind c new-window -c "#{pane_current_path}"
```  
        
## CRIA 5 JANELAS NO DIRETÓRIO ATUAL:
> -d = cria a sessão mas não abre imediatamente na tela
> -s = nome personalizado da sessão
```sh
tmux new-session -d -s <NOME A SESSÃO> \; <NOVA JANELA> \; <NOVA JANELA> \; <NOVA JANELA> \; <NOVA JANELA> \; attach
```  

## CRIE UMA NOVA JANELA -> ABRA UMA JANELA E EXECUTE UM COMANDO
```sh
tmux neww -n "<NOME DA JANELA>" "<COMANDO A SER EXECUTADO>"
```  

## VOLTAR PARA JANELA (SESSÃO):
```sh
tmux attach
```  

> OU

```sh
tmux attach -t <NOME DA JANELA> -> (-t = target)
```  

> OU

```sh
tmux a -t <NOME DA JANELA> -> (-t = target)
```  

## NAVEGAR ENTRE JANELAS:
```sh
CTRL+b n 
CTRL+b p
```  

> OU

```sh
bind-key -n S-right next-window || bind-key -n l next-window
bind-key -n S-left previous-window || bind-key -n h previous-window
```  

## MOVER (JOGAR, ENVIAR) JANELA PARA A MESMA SESSÃO (DEVE SER UM NÚMERO QUE NÂO ESTÁ EM USO NESTA SESSÂO)
```sh
CTRL+ . <NÚMERO NOVO DA JANELA>
```  

> OU

```sh
tmux move-window -s <NÙMERO DA JANELA A SER ENVIADA> -t <NÙMERO NOVO DA JANELA>
```  

> OU

```sh
tmux move-window -s <NOME DA JANELA A SER ENVIADA> -t <NÙMERO NOVO DA JANELA>
```  
        
### EX 0:
```sh
tmux move-window -s 0 -t 1
```  

### EX 1:
```sh
tmux move-window -s janela -t 1
```  

### EX 2:
```sh
tmux move-window -s git -t 1
```  

### EX 3:
```sh
tmux move-window -s "git" -t 1
```  

## MOVER (JOGAR, ENVIAR) JANELA DENTRO DA MESMA SESSÃO E SE MOVER EM CONJUNTO
```sh
CTRL+b : 
  swap-window -t -1; previous-window
  swap-window -t +1; next-window
```  

> OU

```sh
tmux swap-window -s <SESSÂO>:<NÙMERO DA JANELA A SER MOVIDA PARA ESQUERDA> -t <SESSÂO>:-1\; previous-window
tmux swap-window -s <SESSÂO>:<NÙMERO DA JANELA A SER MOVIDA PARA DIREITA> -t <SESSÂO>:+1\; next-window
```  

> OU

```sh
tmux swap-window -t -1\; previous-window
tmux swap-window -t +1\; next-window
```  

> OU

```sh
bind-key -n C-S-left swap-window -t -1\; previous-window
bind-key -n C-S-right swap-window -t +1\; next-window
```  

### EX 0 (ESQUERDA, ANTERIOR, PRÉVIA):
```sh
CTRL+b :
  swap-window -t -1; previous-window
```  

### EX 1 (DIREITA, POSTERIOR, PRÓXIMA):
```sh
CTRL+b :
  swap-window -t +1; next-window
```  

### EX 2: (ESQUERDA-DIREITA, PRIVIOUS-NEXT, VAI-E-VOLTA):
```sh
tmux swap-window -s sessao:2 -t sessao:-1\; previous-window
tmux swap-window -s sessao:1 -t sessao:+1\; next-window
```  

## MOVER (JOGAR, ENVIAR) JANELA (PARA OU OUTRA SESSÃO)
```sh
CTRL+ . <NOME DA SESSÃO QUE RECEBERÁ A JANELA>
```  

> OU

```sh
tmux move-window -s <SESSÂO>:<NÙMERO DA JANELA A SER ENVIADA> -t <SESSÂO>:<NÙMERO DA JANELA NA NOVA SESSÂO>
```  

> OU

```sh
tmux move-window -s <SESSÂO>:<NOME DA JANELA A SER ENVIADA> -t <SESSÂO>:<NÙMERO DA JANELA NA NOVA SESSÃO>
```  
        
### EX 0:
```sh
tmux move-window -s 0 -t 1
```  

### EX 1:
```sh
tmux move-window -s sessao:0 -t base:1
```  

### EX 2:
```sh
tmux move-window -s sessao:janela -t base:1
```  
        
## MUDAR NOME (RENOMEAR) DA JANELA ($ = SHIFT+4):
```sh
CTRL+b ,
```  
        
## PESQUISA (BUSCAR) NA JANELA
```sh
CTRL+b f
```  

## SALTAR PARA A JANELA
```sh
CTRL+b <NUMERO DA JANELA>
```  

## RENUMERA (MOVE) JANELA
```sh
CTRL+b . <NOVO NUMERO>
```  

> OU

```sh
CTRL+b :
  move-window -s <NUMERO ATUAL> -t <NOVO NUMERO>
```  

## RENUMERA TODAS AS JANELAS
```sh
CTRL+b :
  move-window -r
```  

## SINCRONIZA JANELAS
```sh
CTRL+b :
  run-shell 'tmux list-windows -t session | cut -d: -f1 | xargs -I{} tmux send-keys -t session:{} <COMANDO>'
```  

---

# PAINEL
## ABRIR PAINEL -> DIVISÃO VERTICAL (EXATA) (% = SHIFT+5):
```sh
tmux split-window -v
```  

> OU

```sh
CTRL+b %
```  

## ABRIR PAINEL -> DIVISÃO HORIZONTAL (" = SHIFT+'):
```sh
tmux split-window
```  

> OU

```sh
tmux split-window -h
```  

> OU

```sh
CTRL+b "
```  

## MOSTRA TODOS OS ÍNDICES DOS PAINÉIS CRIADOS (NÚMEROS):
```sh
CTRL+b q
```  

## NAVEGAR ENTRE PAINÉIS:
```sh
CTRL+b setas
```  

> OU  

```sh
CTRL+b o
```  

> OU  

```sh
CTRL+b ;
```  

## ZOOM NO PAINEL:
```sh
CTRL+b z
```  

## FECHAR PAINEL:
```sh
CTRL+b x
```  

## FECHAR TODOS OS PAINÉIS DE UMA JANELA DO TMUX:
```sh
CTRL+b &
```  
        
## ABRIR PAINEL E EXECUTAR COMANDO
```sh
tmux split-window -c "<DIRETÓRIO>" "<COMANDO A SER EXECUTADO>" 
```  
        
## HORA NO PAINEL (MX)
```sh
CTRL+b t
```  
        
## PESQUISA NO PAINEL (HIGHLIGHT)
```sh
CTRL+b [ 
        CTRL+s <- PESQUISA
        CTRL+r <- PESQUISA REVERSO
```  

## COPIA NO PAINEL
```sh
(vi copy mode set key)
   setw -g mode-keys vi
   bind -T copy-mode-vi y send-keys -X copy-pipe-and-cancel 'xclip -in -selection clipboard'
```  

> OU

```sh
(vi copy mode key)
   CTRL+b [
           SPACE
           CTRL+j OU  ENTER
```  

> OU

```sh
(emacs)
   CTRL+b [ 
           CTRL+SPACE
           ALT+w  OU  CTRL+w
```  
                 
## COLA NO PAINEL               
```sh
CTRL+b ]
```  

## MOVE (RODA, GIRA) O CONTEXTO ATUAL PARA O PRÓXIMA PRÓXIMO PAINEL
```sh
(segura o CTRL) (aperta b+o)
          CTRL + b-o
```  

## MOVE (ATIRA, JOGA, ENVIA) PAINEL (PARA OUTRA SESSÃO/JANELA)
```sh
CTRL+ : move-pane -s <NÚMERO DO PAINEL> -t <SESSÂO>:<JANELA>
```  

> OU

```sh
CTRL+ : move-pane -s <NÚMERO DO PAINEL> -t <SESSÂO>:<JANELA>.<NÚMERO DO PAINEL>
```  

> OU

### EX 0:
```sh
CTRL+ : move-pane -s 0 -t 0:0.0
```  

### EX 1:
```sh
CTRL+ : move-pane -s 0 -t sessao:janela.0
```  

### EX 2:
```sh
CTRL+ : move-pane -s 0 -t sessao:janela.1
```  

### EX 3:
```sh
CTRL+ : move-pane -s 1 -t sessao:janela.0
```  

### EX 4:
```sh
CTRL+ : move-pane -s 1 -t sessao:janela.1
```  

> OU

```sh
tmux move-pane -s <NÚMERO DO PAINEL> -t sessao:janela.<NÚMERO DO PAINEL>
```   

## TROCA (ATIRA, JOGA, ENVIA) PAINEL (PARA OUTRA SESSÃO/JANELA)
```sh
CTRL+ : swap-pane -s <NÚMERO DO PAINEL> -t <SESSÂO>:<JANELA>.<NÚMERO EXISTENTE DO PAINEL>
```  

> OU

### EX 0:
```sh
CTRL+ : swap-pane -s 0 -t 0:0.0
```  

### EX 1:
```sh
CTRL+ : swap-pane -s 0 -t sessao:janela.0
```  

### EX 2:
```sh
CTRL+ : swap-pane -s 0 -t sessao:janela.1
```  

### EX 3:
```sh
CTRL+ : swap-pane -s 1 -t sessao:janela.0
```  

### EX 4:
```sh
CTRL+ : swap-pane -s 1 -t sessao:janela.1
```  

> OU

```sh
tmux swap-pane -s <NÚMERO DO PAINEL> -t sessao:janela.<NÚMERO EXISTENTE DO PAINEL>
```   

## ALTERA O TAMANHO DOS PAINÉIS
```sh
(segura o CTRL) (aperta b+seta)
          CTRL + b-seta
```  

> OU

```sh
CTRL+b + CTRL(pressionado)+seta
```  

## MUDA O LAYOUT DO PAINEL
```sh
CTRL+b + CTRL+space
```  

## SINCRONIZA PAINÉIS
```sh
CTRL+b :
setw synchronize-panes on/off <on == liga e off == desliga>
```  

## MOVE PAINEL PARA OS LADOS COMO NO VI
```sh
bind L splitw -fh  \; swapp -t ! \; killp -t !
bind J splitw -fv  \; swapp -t ! \; killp -t !
bind K splitw -fvb \; swapp -t ! \; killp -t !
bind H splitw -fhb \; swapp -t ! \; killp -t!
#              │││    ├────────┘    ├───────┘
#              │││    │             └ kill the previous pane
#              │││    └ exchange the previous original pane with the current one
#              ││└ the new pane should be created to the left of or above target-pane
#              │└ full window height
#              └ creates a new pane spanning the full window height (with -h)
#                or full window width (with -v), instead of splitting the active pane
```  

## NAVEGAR ENTRE PAINÉIS COMO NO VI
```sh
bind h select-pane -L # -L == mover (navegar) para o painel à esquerda
bind j select-pane -D # -D == mover (navegar) para o painel abaixo
bind k select-pane -U # -U == mover (navegar) para o painel acima
bind l select-pane -R # -R == mover (navegar) para o painel à direita
```  


## ABRIR PAINEL NO DIRETÓRIO ATUAL
```sh
bind '"' split-window -c "#{pane_current_path}"
bind % split-window -h -c "#{pane_current_path}"
```  

---

# CONFIG
## LOCAL:
```sh
/home/${USER}/.tmux.conf       Default tmux configuration file.
/etc/tmux.conf     System-wide configuration file.
```  

## SETTINGS:
### DESATIVA PREFIXO: CTRL+b
```sh
unbind C-b
```  

### SETA NOVO PREFIXO (-g = global):
```sh
set -g prefix <NOVA(S) TECLA(S)>
set -g prefix C-a || set -g prefix M-a # C = CTRL ^ M - ALT
```  

### ATIVA MOUSE:
```sh
    setw -g mode-mouse on
```  

> OU

```sh
    set -g mouse on
```  

### SETA WINDOWS (SUPER KEY) COMO PREFIX:
```sh
set-option -g prefix <keycode>

unbind-key C-b

bind-key <keycode> send-prefix
```  

### ALTERA COR DA BARRA DE STATUS (STATUSBAR):
```sh
set -g status-bg default (default = cor do terminal)
set -g status-fg white
```  

### COMANDO QUE SINCRONIZA (PAINÉIS):
```sh
bind-key -n M-z set-window-option synchronize-panes
```  

## SETTINGS NUMA LINHA:
> SETA NOVO PREFIXO ^ NAVEGAR ENTRE JANELAS ^ ABRIR PAINEL NO DIRETÓRIO ATUAL ^ COMANDO QUE SINCRONIZA (PAINÉIS)
```sh
set -g prefix M-a ; bind-key -n S-right next-window ; bind-key -n S-left previous-window ; bind '"' split-window -c "#{pane_current_path}" ; bind '%' split-window -h -c "#{pane_current_path}" ; bind-key -n M-z set-window-option synchronize-panes ; bind-key -n C-S-left swap-window -t -1\; previous-window ; bind-key -n C-S-right swap-window -t +1\; next-window
```  

## PLUGINS
### LIST OF PLUGINS
```sh
set -g @plugin 'tmux-plugins/tpm' # C-a I
set -g @plugin 'tmux-plugins/tmux-sensible'

set -g @plugin 'tmux-plugins/tmux-resurrect' # prefix + Ctrl-s - save ^ prefix + Ctrl-r - restore
set -g @plugin 'tmux-plugins/tmux-continuum'
```  

### TMUX FZF URL
```sh
(NÂO USADO) set -g @plugin 'wfxr/tmux-fzf-url'
```  

### TMUX POWERLINE THEME
```sh
set -g @plugin 'wfxr/tmux-power'

set -g @tmux_power_theme 'snow'
(NÂO USADO) set -g @tmux_power_theme 'gold'
(NÂO USADO) set -g @tmux_power_theme 'redwine'
(NÂO USADO) set -g @tmux_power_theme 'moon'
(NÂO USADO) set -g @tmux_power_theme 'forest'
(NÂO USADO) set -g @tmux_power_theme 'violet'
(NÃO USADO) set -g @tmux_power_theme 'coral'
(NÃO USADO) set -g @tmux_power_theme 'sky'

(NÃO USADO) set -g @tmux_power_date_icon ' ' # set it to a blank will disable the icon
(NÃO USADO) set -g @tmux_power_date_icon '' # set it to a blank will disable the icon

set -g @tmux_power_time_icon '🕘' # emoji can be used if your terminal supports

(NÃO USADO) set -g @tmux_power_user_icon 'U'
(NÃO USADO) set -g @tmux_power_user_icon ' '
(NÃO USADO) set -g @tmux_power_user_icon ' '
(NÃO USADO) set -g @tmux_power_user_icon ' '

(NÃO USADO) set -g @tmux_power_session_icon 'S'
(NÃO USADO) set -g @tmux_power_session_icon ' '

(NÃO USADO) set -g @tmux_power_upload_speed_icon '↑'
(NÃO USADO) set -g @tmux_power_download_speed_icon '↓'
(NÃO USADO) set -g @tmux_power_left_arrow_icon '<'
(NÃO USADO) set -g @tmux_power_right_arrow_icon '>'
```  


### TMUX COLORIZED THEME
```sh
(NÃO USADO) set -g @plugin 'seebi/tmux-colors-solarized'
(NÃO USADO) set -g @colors-solarized '256' 
(NÃO USADO) set -g @colors-solarized 'dark'
(NÃO USADO) set -g @colors-solarized 'light'
(NÃO USADO) set -g @colors-solarized 'base16'
```  

### TMUX FOR VIM/NEOVIM
```sh
set -g @resurrect-strategy-vim 'session'
set -g @resurrect-strategy-nvim 'session'
```  

### TMUX FOR GIT
```sh
(NÃO USADO) set -g @plugin 'github_username/plugin_name'
(NÃO USADO) set -g @plugin 'github_username/plugin_name#branch'
(NÃO USADO) set -g @plugin 'git@github.com:user/plugin'
(NÃO USADO) set -g @plugin 'git@bitbucket.com:user/plugin'
```  

### TMUX BATTERY
```sh
(NÃO USADO) set -g @plugin 'tmux-plugins/tmux-battery'
# Formato: ícone + porcentagem + tempo restante
(NÃO USADO) set -g @tmux_power_right '🔋 #{battery_icon} #{battery_percentage} #{battery_remain} | #{date_icon} #{date} #{time_icon} #{time}'
```  

### TMUX SAVE AND RESTORE AUTOMATICALLY
```sh
set -g @continuum-restore 'on'
```  

### INITIALIZE TMUX PLUGIN MANAGER (KEEP THIS LINE AT THE VERY BOTTOM OF TMUX.CONF)
```sh
run '~/.tmux/plugins/tpm/tpm'
```  

---

# FUNÇÕES
```sh
tmx () {
    # Use -d to allow the rest of the function to run
    tmux new-session -d -s SessionName
    tmux new-window -n Win1
    # -d to prevent current window from changing
    tmux new-window -d -n Win2
    tmux new-window -d -n Win3
    tmux new-window -d -n Win4
    # -d to detach any other client (which there shouldn't be,
    # since you just created the session).
    tmux attach-session -d -t SessionName
}
```  

```sh
alias tmx='tmux source-file "${HOME}/.tmux/<NOME_DO_ARQUIVO>"'
```  

---

# REFERÊNCIAS
[TMUX FUNÇÕES](https://stackoverflow.com/questions/48997929/how-do-i-create-a-tmux-session-with-multiple-windows-already-opened)  
[Tmux Key Bind Like To Use The Windows Super For My Meta Key in Tmux Without x](https://unix.stackexchange.com/questions/112163/tmux-key-bind-like-to-use-the-windows-super-for-my-meta-key-in-tmux-without-x)  
[10 Killer Tmux Tips](https://www.sitepoint.com/10-killer-tmux-tips/)  
[Use Windows Key in Tmux](https://superuser.com/questions/717685/use-windows-key-in-tmux)  
[How Can i Search Within The Output Buffer of a Tmux Shell](https://superuser.com/questions/231002/how-can-i-search-within-the-output-buffer-of-a-tmux-shell)  
[Copy and Paste in Tmux](https://www.rockyourcode.com/copy-and-paste-in-tmux/)  

## TMUX CONF:
[A Tmux Crash Course](https://thoughtbot.com/blog/a-tmux-crash-course)  
[A Guide to Customizing Your Tmux Conf](https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/)  
[How Do I Reorder Tmux Windows](https://superuser.com/questions/343572/how-do-i-reorder-tmux-windows)  
[How To I Reload Tmux Configuration](https://superuser.com/questions/580992/how-do-i-reload-tmux-configuration)  
[Tmux How to Move Current Pane to far Left Right Up Down Like in Vim](https://superuser.com/questions/1601701/tmux-how-to-move-current-pane-to-far-left-right-up-down-like-in-vim)  
[How To Send A Command To All Panes in Tmux](https://qastack.com.br/programming/16325449/how-to-send-a-command-to-all-panes-in-tmux)  
[Run or Send a Command To a Tmux Pane in a Running Tmux Session](https://qastack.com.br/superuser/492266/run-or-send-a-command-to-a-tmux-pane-in-a-running-tmux-session)  
[Renumbering Windows in Tmux](https://qastack.com.br/unix/21742/renumbering-windows-in-tmux)  
[Use System Clipboard in VI Copy Mode in Tmux](https://unix.stackexchange.com/questions/131011/use-system-clipboard-in-vi-copy-mode-in-tmux)  
[Tmux Conf](https://thoughtbot.com/upcase/tmux)  
[Tmux Conf by spicycode](https://gist.github.com/spicycode/1229612)  
[Tmux Conf by paulodeleo](https://gist.github.com/paulodeleo/5594773)  
[Tmux Conf by henrik](https://gist.github.com/henrik/1967800)  
[Tmux Conf by MohamedAlaa](https://gist.github.com/MohamedAlaa/2961058)  
[Tmux Conf by Ape](https://gist.github.com/Ape/d0c48b3f7ec9c8efaecf48eaa1e75d0d)  
[Tmux Conf by william8th](https://gist.github.com/william8th/faf23d311fc842be698a1d80737d9631)  
[How do i Create a Tmux Session With Multiple Windows Already Opened](https://stackoverflow.com/questions/48997929/how-do-i-create-a-tmux-session-with-multiple-windows-already-opened)  
[Send Command to All Window in Tmux](https://stackoverflow.com/questions/9250884/send-command-to-all-window-in-tmux)  
[Tmux Using hjkl to Navigate Panes](https://stackoverflow.com/questions/30719042/tmux-using-hjkl-to-navigate-panes)  
[Tmux Create New Window on Current Directory](https://serverok.in/tmux-create-new-window-on-current-directory)  
[How To Create a New Window on The Current Directory in Tmux](https://unix.stackexchange.com/questions/12032/how-to-create-a-new-window-on-the-current-directory-in-tmux)  
[TMP - Tmux Plugins](https://github.com/tmux-plugins/tpm)  
