############################# PREFIXO ############################
PREFIXO: 
        CTRL+b

############################# MENU ############################
tmux list-keys
tmux list-keys -N
CTRL+b ?

############################# PROMPT PARA ENVIAR COMANDOS ############################
CTRL+b :

############################ SESSÃO ############################
LISTAR SESSÕES:
	tmux list-sessions
	OU
	tmux ls


CRIA (NOVA) SESSÂO:
	tmux new-session
	OU
	tmux new


CRIA (NOVA) SESSÂO (COM NOME, NOMEADA):
	tmux new-session -s <NOME DA SESSÂO>
	OU
	tmux new -s <NOME DA SESSÂO>
  EX 0: tmux new -s sessao
  EX 1: tmux new -s "sessao"


CRIA (NOVA) SESSÂO (COM NOME, NOMEADA) (NÂO ENTRA NELA):
	tmux new-session -d -s <NOME DA SESSÂO>
	OU
	tmux new -d -s <NOME DA SESSÂO>
  EX 0: tmux new -d -s sessao
  EX 1: tmux new -d -s "sessao"


CRIA (NOVA) SESSÂO e JANELA (AMBAS COM NOME, NOMEADAS):
        tmux new-session -s <NOME DA SESSÂO> -n <NOME DA JANELA>
        OU
  EX 0: tmux new -s sessao -n janela
  EX 1: tmux new -s "sessao" -n janela
  EX 2: tmux new -s sessao -n "janela"
  EX 3: tmux new -s "sessao" -n "janela"


CRIA (NOVA) SESSÂO e JANELA (AMBAS COM NOME, NOMEADAS) (NÂO ENTRA NELA):
        tmux new-session -d -s <NOME DA SESSÂO> -n <NOME DA JANELA>
        OU
  EX 0: tmux new -d -s sessao -n janela
  EX 1: tmux new -d -s "sessao" -n janela
  EX 2: tmux new -d -s sessao -n "janela"
  EX 3: tmux new -d -s "sessao" -n "janela"


CRIA (NOVA) SESSÂO e (NOVAS) JANELAS (TODAS COM NOME):
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

        EX em .zshrc:
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


NAVEGAR ENTRE SESSÕES (LISTA DE SESSÕES):
        CTRL+b s


NAVEGAR ENTRE SESSÕES:JANELAS (LISTA DE SESSÕES:JANELAS):
        CTRL+b w
        

MUDAR NOME (RENOMEAR) DA SESSÃO ($ = SHIFT+4):
        CTRL+b $
        

ENVIA TECLAS:
        tmux send-keys -t <SESSÃO>:<JANELA>.<PAINEL> <TECLAS A ENVIAR>
        
  EX 0:  tmux send-keys -t sessao Olá, mundo!
  EX 1:  tmux send-keys -t "sessao" Olá, mundo!
  EX 2:  tmux send-keys -t sessao "Olá, mundo!"
  EX 3:  tmux send-keys -t "sessao" "Olá, mundo!"
  EX 4:  tmux send-keys -t sessao:0 Olá, mundo!
  EX 5:  tmux send-keys -t "sessao:0" Olá, mundo!
  EX 6:  tmux send-keys -t sessao:0 "Olá, mundo!"
  EX 7:  tmux send-keys -t "sessao:0" "Olá, mundo!"
  EX 8:  tmux send-keys -t minha_sessao:bash Olá, mundo!
  EX 9:  tmux send-keys -t "minha_sessao:bash" "Olá, mundo!"
  EX 10: tmux send-keys -t "0:1" "olá, mundo"


ENVIA COMANDOS:
        tmux send-keys -t <SESSÃO>:<JANELA>.<PAINEL> <COMANDO> ENTER

  EX 0:  tmux send-keys -t sessao ls ENTER
  EX 1:  tmux send-keys -t sessao "ls" ENTER
  EX 2:  tmux send-keys -t sessao ls "ENTER"
  EX 3:  tmux send-keys -t "sessao" "ls" ENTER
  EX 4:  tmux send-keys -t "sessao" "ls" "ENTER"
  EX 5:  tmux send-keys -t sessao:janela ls ENTER
  EX 6:  tmux send-keys -t "sessao:janela" ls ENTER
  EX 7:  tmux send-keys -t sessao:janela "ls" ENTER
  EX 8:  tmux send-keys -t sessao:janela ls "ENTER"
  EX 9:  tmux send-keys -t "sessao:janela" "ls" "ENTER"
  EX 10: tmux send-keys -t sessao:janela.painel ls ENTER
  EX 11: tmux send-keys -t "sessao:janela.painel" ls ENTER
  EX 12: tmux send-keys -t sessao:janela.painel "ls" ENTER
  EX 13: tmux send-keys -t sessao:janela.painel ls "ENTER"
  EX 14: tmux send-keys -t "sessao:janela.painel" "ls" "ENTER"
  EX 15: tmux send-keys -t "0:0.0" "ls" "ENTER"


SAIR DE SESSÃO (MANTÉM SESSÃO VIVA):
	CTRL+b d
	

ENTRAR (RETORNAR) PARA A SESSÃO:
	tmux attach-session -t <NOME DA SESSÃO>

  EX 0: tmux attach-session -t sessao
  EX 1: tmux attach-session -t "sessao"
  EX 2: tmux attach-session -t "minha_sessao"


MATA SESSÃO
        tmux kill-session -t <SESSÃO>
	OU
        tmux kill-session -t <SESSÃO>:<JANELA>.<PAINEL>

  EX 0: tmux kill-session -t sessao
  EX 1: tmux kill-session -t sessao:janela.painel
  EX 2: tmux kill-session -t "sessao:janela.painel"
  EX 3: tmux kill-session -t 0:0.0
  EX 4: tmux kill-session -t "0:0.0"


############################# JANELA ############################
LISTAR JANELAS:
	tmux list-window


CRIA JANELA:
        tmux neww
        OU
        CTRL+b c


CRIA JANELA (COM NOME):
        CTRL+b , <NOME DA JANELA>
                OU
        tmux neww -n "<NOME DA JANELA>"
        

CRIA JANELA NO DIRETÓRIO ATUAL:
        bind c new-window -c "#{pane_current_path}"
        

CRIA 5 JANELAS NO DIRETÓRIO ATUAL:
	-d = cria a sessão mas não abre imediatamente na tela
	-s = nome personalizado da sessão
	tmux new-session -d -s <NOME A SESSÃO> \; <NOVA JANELA> \; <NOVA JANELA> \; <NOVA JANELA> \; <NOVA JANELA> \; attach


CRIE UMA NOVA JANELA -> ABRA UMA JANELA E EXECUTE UM COMANDO
        tmux neww -n "<NOME DA JANELA>" "<COMANDO A SER EXECUTADO>"


VOLTAR PARA JANELA:
        tmux attach
                OU
        tmux attach -t <NOME DA JANELA> -> (-t = target)
                OU
        tmux a -t <NOME DA JANELA> -> (-t = target)


NAVEGAR ENTRE JANELAS:
        CTRL+b n 
        CTRL+b p
          OU
        bind-key -n S-right next-window || bind-key -n l next-window
        bind-key -n S-left previous-window || bind-key -n h previous-window


MOVER (JOGAR, ENVIAR) JANELA PARA A MESMA SESSÃO (DEVE SER UM NÚMERO QUE NÂO ESTÁ EM USO NESTA SESSÂO)
        CTRL+ . <NÚMERO NOVO DA JANELA>
          OU
        tmux move-window -s <NÙMERO DA JANELA A SER ENVIADA> -t <NÙMERO NOVO DA JANELA>
	  OU
        tmux move-window -s <NOME DA JANELA A SER ENVIADA> -t <NÙMERO NOVO DA JANELA>
        
   EX 0: tmux move-window -s 0 -t 1
   EX 1: tmux move-window -s janela -t 1
   EX 2: tmux move-window -s git -t 1
   EX 3: tmux move-window -s "git" -t 1
    
        
MOVER (JOGAR, ENVIAR) JANELA (PARA OU OUTRA SESSÃO)
        CTRL+ . <NOME DA SESSÃO QUE RECEBERÁ A JANELA>
          OU
        tmux move-window -s <SESSÂO>:<NÙMERO DA JANELA A SER ENVIADA> -t <SESSÂO>:<NÙMERO DA JANELA NA NOVA SESSÂO>
          OU
        tmux move-window -s <SESSÂO>:<NOME DA JANELA A SER ENVIADA> -t <SESSÂO>:<NÙMERO DA JANELA NA NOVA SESSÃO>
        
    EX 0: tmux move-window -s 0 -t 1
    EX 1: tmux move-window -s sessao:0 -t base:1
    EX 1: tmux move-window -s sessao:janela -t base:1

        
MUDAR NOME (RENOMEAR) DA JANELA ($ = SHIFT+4):
        CTRL+b ,
        
PESQUISA (BUSCAR) NA JANELA
        CTRL+b f

SALTAR PARA A JANELA
        CTRL+b <NUMERO DA JANELA>

RENUMERA (MOVE) JANELA
        CTRL+b . <NOVO NUMERO>
          OU
        CTRL+b :
          move-window -s <NUMERO ATUAL> -t <NOVO NUMERO>

RENUMERA TODAS AS JANELAS
        CTRL+b :
          move-window -r

SINCRONIZA JANELAS
        CTRL+b :
          run-shell 'tmux list-windows -t session | cut -d: -f1 | xargs -I{} tmux send-keys -t session:{} <COMANDO>'


############################# PAINEL ############################
ABRIR PAINEL -> DIVISÃO VERTICAL (EXATA) (% = SHIFT+5):
        tmux split-window -v
        CTRL+b %

ABRIR PAINEL -> DIVISÃO HORIZONTAL (" = SHIFT+'):
        tmux split-window
              OU
        tmux split-window -h
              OU
        CTRL+b "

MOSTRA TODOS OS ÍNDICES DOS PAINÉIS CRIADOS (NÚMEROS):
        CTRL+b q

NAVEGAR ENTRE PAINÉIS:
        CTRL+b setas 
        CTRL+b o
        CTRL+b ;

ZOOM NO PAINEL:
        CTRL+b z

FECHAR PAINEL:
        CTRL+b x

FECHAR TODOS OS PAINÉIS DE UMA JANELA DO TMUX:
        CTRL+b &
        
ABRIR PAINEL E EXECUTAR COMANDO
        tmux split-window -c "<DIRETÓRIO>" "<COMANDO A SER EXECUTADO>" 
        
HORA NO PAINEL (MX)
        CTRL+b t
        
PESQUISA NO PAINEL (HIGHLIGHT)
        CTRL+b [ 
                CTRL+s <- PESQUISA
                CTRL+r <- PESQUISA REVERSO

COPIA NO PAINEL
     (vi copy mode set key)
        setw -g mode-keys vi
        bind -T copy-mode-vi y send-keys -X copy-pipe-and-cancel 'xclip -in -selection clipboard'
          OU
     (vi copy mode key)
        CTRL+b [
                SPACE
                CTRL+j OU  ENTER
          OU
     (emacs)
        CTRL+b [ 
                CTRL+SPACE
                ALT+w  OU  CTRL+w
                 
COLA NO PAINEL               
                CTRL+b ]

MOVE (RODA, GIRA) O CONTEXTO ATUAL PARA O PRÓXIMA PRÓXIMO PAINEL
       (segura o CTRL) (aperta b+o)
                 CTRL + b-o

ALTERA O TAMANHO DOS PAINÉIS
       (segura o CTRL) (aperta b+seta)
                 CTRL + b-seta
                      ou
                 CTRL+b + CTRL(pressionado)+seta

MUDA O LAYOUT DO PAINEL
       CTRL+b + CTRL+space

SINCRONIZA PAINÉIS
        CTRL+b :
        setw synchronize-panes on/off <on == liga e off == desliga>

MOVE PAINEL PARA OS LADOS COMO NO VI
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

NAVEGAR ENTRE PAINÉIS COMO NO VI
        bind h select-pane -L # -L == mover (navegar) para o painel à esquerda
        bind j select-pane -D # -D == mover (navegar) para o painel abaixo
        bind k select-pane -U # -U == mover (navegar) para o painel acima
        bind l select-pane -R # -R == mover (navegar) para o painel à direita


ABRIR PAINEL NO DIRETÓRIO ATUAL
        bind '"' split-window -c "#{pane_current_path}"
        bind % split-window -h -c "#{pane_current_path}"


############################# CONFIG ############################
LOCAL:
     ~/.tmux.conf       Default tmux configuration file.
     /etc/tmux.conf     System-wide configuration file.

SETTINGS:
    DESATIVA PREFIXO: CTRL+b
        unbind C-b

    SETA NOVO PREFIXO (-g = global):
        set -g prefix <NOVA(S) TECLA(S)>
        set -g prefix C-a || set -g prefix M-a # C = CTRL ^ M - ALT

    ATIVA MOUSE:
        setw -g mode-mouse on
            # ou
        set -g mouse on

    SETA WINDOWS (SUPER KEY) COMO PREFIX:
        set-option -g prefix <keycode>

        unbind-key C-b

        bind-key <keycode> send-prefix

    ALTERA COR DA BARRA DE STATUS (STATUSBAR):
        set -g status-bg default (default = cor do terminal)
        set -g status-fg white

    COMANDO QUE SINCRONIZA (PAINÉIS):
        bind-key -n M-z set-window-option synchronize-panes


SETTINGS NUMA LINHA:
    SETA NOVO PREFIXO ^ NAVEGAR ENTRE JANELAS ^ COMANDO QUE SINCRONIZA (PAINÉIS) ^ ABRIR PAINEL NO DIRETÓRIO ATUAL
	set -g prefix M-a ; bind-key -n S-right next-window ; bind-key -n S-left previous-window ; bind '"' split-window -c "#{pane_current_path}" ; bind '%' split-window -h -c "#{pane_current_path}" ; bind-key -n M-z set-window-option synchronize-panes


############################### FUNÇÕES ##############################
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

alias tmx='tmux source-file "${HOME}/.tmux/<NOME_DO_ARQUIVO>"'

TMUX FUNÇÕES:
#   -> https://stackoverflow.com/questions/48997929/how-do-i-create-a-tmux-session-with-multiple-windows-already-opened

############################# REFERÊNCIAS ############################
#   -> https://unix.stackexchange.com/questions/112163/tmux-key-bind-like-to-use-the-windows-super-for-my-meta-key-in-tmux-without-x
#   -> https://www.sitepoint.com/10-killer-tmux-tips/
#   -> https://superuser.com/questions/717685/use-windows-key-in-tmux
#   -> https://superuser.com/questions/231002/how-can-i-search-within-the-output-buffer-of-a-tmux-shell 
#   -> https://www.rockyourcode.com/copy-and-paste-in-tmux/

TMUX CONF:
#   -> https://gist.github.com/spicycode/1229612
#   -> https://gist.github.com/paulodeleo/5594773
#   -> https://thoughtbot.com/blog/a-tmux-crash-course
#   -> https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/
#   -> https://superuser.com/questions/580992/how-do-i-reload-tmux-configuration
#   -> https://gist.github.com/henrik/1967800
#   -> https://gist.github.com/MohamedAlaa/2961058
#   -> https://gist.github.com/Ape/d0c48b3f7ec9c8efaecf48eaa1e75d0d
#   -> https://qastack.com.br/programming/16325449/how-to-send-a-command-to-all-panes-in-tmux
#   -> https://qastack.com.br/superuser/492266/run-or-send-a-command-to-a-tmux-pane-in-a-running-tmux-session
#   -> https://unix.stackexchange.com/questions/131011/use-system-clipboard-in-vi-copy-mode-in-tmux#:~:text=Then hit Ctrl%2Bb %5B to,default bindings with vi keys.
#   -> https://thoughtbot.com/upcase/tmux
#   -> https://stackoverflow.com/questions/48997929/how-do-i-create-a-tmux-session-with-multiple-windows-already-opened
#   -> https://qastack.com.br/unix/21742/renumbering-windows-in-tmux
#   -> https://stackoverflow.com/questions/9250884/send-command-to-all-window-in-tmux
#   -> https://superuser.com/questions/343572/how-do-i-reorder-tmux-windows#:~:text=Pressing%20Ctrl%2BShift%2BLeft%20(,use%20the%20modifier%20(C-b).

#   -> https://superuser.com/questions/1601701/tmux-how-to-move-current-pane-to-far-left-right-up-down-like-in-vim
#   -> https://stackoverflow.com/questions/30719042/tmux-using-hjkl-to-navigate-panes
#   -> https://serverok.in/tmux-create-new-window-on-current-directory
#   -> https://gist.github.com/william8th/faf23d311fc842be698a1d80737d9631
#   -> https://unix.stackexchange.com/questions/12032/how-to-create-a-new-window-on-the-current-directory-in-tmux
