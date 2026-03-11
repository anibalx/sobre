# Comandos
```
ctrl + d 					= sai do termenial
ctrl + e 					= salta para o final
ctrl + j 					= similar ao TAB
ctrl + k 					= apaga tudo para frente
ctrl + r 					= busca para trás
ctrl + s 					= trava terminal
ctrl + u 					= cola o que há no buffer
ctrl + w 					= apaga para trás de onde o cursor está (na verdade, corta e não exclui)
ctrl + y 					= desfazer o que eu havia apagado (puxa tudo)
ctrl + shift + - 	        = desfazer o que eu havia apagado
ctrl + / 					= desfazer caracter a caracter 
```  

---

## 1. Usar o `which` ou `whereis`

Se você já conhece o nome do binário (ou parte dele):
```bash
# Procura pelo comando
which nautilus
which gnome-text-editor

# Procura em vários locais
whereis nautilus
```

## 2. Usar o `grep` para buscar nos binários

```bash
# Lista todos os binários disponíveis e filtra por "gnome" ou "text"
ls /usr/bin/ | grep -i "gnome"  # -i ignora maiúsculas/minúsculas
ls /usr/bin/ | grep -i "editor"
```

## 3. Através dos arquivos .desktop

Os arquivos `.desktop` contêm informações completas dos aplicativos:
```bash
# Lista todos os aplicativos Gnome
ls /usr/share/applications/ | grep -i gnome

# Para ver detalhes de um aplicativo específico
cat /usr/share/applications/org.gnome.TextEditor.desktop | grep -i "Exec"
```

## 4. Usar o comando `apropos` ou `whatis`

```bash
# Busca por descrições de comandos relacionados
apropos editor
apropos gnome

# Mostra descrição curta de um comando
whatis gnome-text-editor
```

## 5. Descobrindo o nome do editor de texto

Especificamente para o editor de texto atual do Gnome:
```bash
# O editor de texto moderno do Gnome
gnome-text-editor  # Nome do comando atual

# Editor legado (versões antigas)
gedit              # Editor anterior

# Para descobrir qual está instalado
which gnome-text-editor gedit 2>/dev/null
```

## 6. Usar o `dpkg` (Debian/Ubuntu) ou `rpm` (Fedora)

```bash
# No Debian/Ubuntu, lista todos os pacotes gnome
dpkg -l | grep gnome | grep editor

# No Fedora
rpm -qa | grep gnome | grep editor
```

## 7. Comando prático para listar todos os aplicativos Gnome

Aqui está um comando útil que lista os principais aplicativos Gnome instalados:

```bash
# Lista binários Gnome no /usr/bin
ls /usr/bin/ | grep -E '^gnome-|^nautilus|^evince|^eog|^gedit|^gnome-text-editor' | sort

# Ou melhor, lista pelos arquivos .desktop
grep -l "^Exec=" /usr/share/applications/org.gnome.*.desktop | xargs grep "Name="
```

## Para o seu caso específico:

O editor de texto atual do Gnome (Gnome Text Editor) tem como comando:
```bash
gnome-text-editor
```

Outros aplicativos comuns do Gnome:
```bash
nautilus           # Gerenciador de arquivos (Arquivos)
gnome-terminal     # Terminal
gnome-calculator   # Calculadora
gnome-calendar     # Calendário
gnome-software     # Loja de aplicativos
gnome-system-monitor # Monitor do sistema
evince            # Visualizador de PDF (Documentos)
eog               # Visualizador de imagens (Eye of Gnome)
gnome-disk-utility # Discos (Gerenciador de discos)
gnome-screenshot   # Captura de tela
gnome-logs        # Visualizador de logs
gnome-characters  # Mapa de caracteres
```

Para descobrir rapidamente, você pode usar:
```bash
# Lista todos os binários relacionados ao Gnome
ls /usr/bin/ | grep -E '^gnome-|^nautilus' | sort
```

Isso mostrará todos os comandos disponíveis começando com "gnome-" e também o nautilus, facilitando encontrar o nome correto de cada aplicativo.

---

## 📝 Método 1: Editor de Menus (Mais Simples)

Esta é a forma mais direta para qualquer aplicativo:

1.  **Clique com botão direito** no menu K (Kickoff Application Launcher) no painel
2.  Selecione **"Editar Menu"** ou **"Menu Editor"** 
3.  **Navegue até o aplicativo** desejado (ex: Sistema → Dolphin)
4.  Na aba **"Geral"**, veja o campo **"Comando"** - este é o nome do executável 
5.  Confirme no terminal: `which nome_do_comando` (ex: `which dolphin`)

## 🔍 Método 2: Listar Todos os Comandos KDE

Para ver todos os comandos KDE disponíveis no sistema:

```bash
# Lista todos os binários relacionados ao KDE
ls /usr/bin/ | grep -E '^kde|^kwin|^dolphin|^konsole|^kate|^okular' | sort

# Ou especificamente para aplicações KDE
ls /usr/bin/ | grep -i "^k" | grep -E 'kate|konsole|dolphin|okular|kwrite'
```

## 🎯 Método 3: Descobrir pelo Nome do Processo (xprop)

Se o aplicativo já estiver aberto:

```bash
# No terminal, digite:
xprop WM_CLASS
# O cursor vira uma cruz - clique na janela do aplicativo
# O terminal mostrará algo como: WM_CLASS(STRING) = "dolphin", "Dolphin"
# O primeiro valor entre aspas é o nome do comando 
```

## 📦 Método 4: Buscar nos Arquivos .desktop

Os arquivos .desktop contêm os nomes reais dos comandos:

```bash
# Lista todos os arquivos .desktop do KDE
ls /usr/share/applications/ | grep -i kde | grep -i desktop

# Ver detalhes de um específico
cat /usr/share/applications/org.kde.dolphin.desktop | grep -i "Exec"
```

## 🚀 Principais Comandos de Aplicativos KDE

Aqui estão os comandos dos aplicativos mais comuns do KDE:

| Aplicativo (nome visual) | Comando no Terminal |
|--------------------------|---------------------|
| **Dolphin** (Gerenciador de Arquivos) | `dolphin`  |
| **Kate** (Editor Avançado) | `kate` |
| **KWrite** (Editor Simples) | `kwrite` |
| **Konsole** (Terminal) | `konsole` |
| **Okular** (Visualizador de PDF/Documentos) | `okular` |
| **Spectacle** (Captura de Tela) | `spectacle` |
| **Gwenview** (Visualizador de Imagens) | `gwenview` |
| **KSystemLog** (Visualizador de Logs) | `ksystemlog` |
| **Ark** (Compactador de Arquivos) | `ark` |
| **KCalc** (Calculadora) | `kcalc` |

## 🔧 Método Avançado: Usar DCOP (KDE 3/4)

Em versões mais antigas do KDE, existe o sistema DCOP:

```bash
# Lista todas as aplicações rodando com interface DCOP
dcop
```

## 💡 Dica Extra: Parâmetros Comuns

Todos os aplicativos KDE aceitam parâmetros padrão úteis :
```bash
nome_app --help        # Mostra ajuda
nome_app --version     # Mostra versão
nome_app --author      # Mostra autores
nome_app --license     # Mostra licença
```

Agora você pode facilmente descobrir que o editor de texto principal do KDE (Kate) é chamado pelo terminal simplesmente como `kate`! 😊

---

Em gerenciadores de janela como i3wm ou Sway, o método para descobrir o nome dos comandos é um pouco diferente, pois eles não vêm com um conjunto fixo de aplicativos pré-instalados. A filosofia é você escolher e instalar as ferramentas que deseja. Portanto, a maneira de "descobrir" depende de como você as iniciou ou configurou.

Aqui estão as principais estratégias, divididas entre os dois tipos de aplicação:

### 1. Para Aplicativos que Você Já Está Usando

Esta é a forma mais direta se o programa já está aberto na tela. Você vai usar ferramentas para "inspecionar" a janela e descobrir seu nome de processo.

#### No i3 (X11)
O comando principal aqui é o `xprop`. Ele é uma ferramenta padrão do X11 para exibir propriedades das janelas.
1.  Abra um terminal.
2.  Digite `xprop` e pressione Enter.
3.  Seu cursor se transformará em uma cruz ou um alvo.
4.  **Clique na janela do aplicativo** que você quer investigar (por exemplo, o editor de texto).
5.  O terminal será preenchido com várias informações sobre aquela janela. Procure especificamente pela linha `WM_CLASS`. O resultado será algo como:
    ```
    WM_CLASS(STRING) = "geany", "Geany"
    ```
    **Interpretação**: No i3, o primeiro valor (`geany`) é geralmente a **instância** (que pode variar), e o segundo (`Geany`) é a **classe**. Para a maioria dos casos, e especialmente para descobrir o nome do comando, o segundo valor costuma ser o nome do executável, mas em minúsculas. No exemplo acima, o comando é muito provavelmente `geany` .
6.  Para sair do modo `xprop`, pressione `Ctrl + C` no terminal.

> **Dica extra:** Você pode usar `xprop | grep WM_CLASS` para filtrar a saída e ver apenas a linha que interessa .

#### No Sway (Wayland)
No Wayland, o `xprop` não funciona. O equivalente é o comando `swaymsg`, que é a ferramenta de controle do próprio Sway.
1.  Com o aplicativo aberto e em foco, execute no terminal:
    ```bash
    swaymsg -t get_tree | grep -i "app_id"
    ```
    Ou, para uma busca mais específica pelo nome da janela:
    ```bash
    swaymsg -t get_tree | grep -i "nome_do_app_na_janela"
    ```
2.  O `swaymsg` retornará uma grande estrutura JSON com a árvore de todas as janelas. O `grep` vai te ajudar a encontrar a linha que contém o `"app_id"`, que é o identificador que o Sway usa e que geralmente corresponde ao nome do binário do aplicativo.

### 2. Para Aplicativos que Você Lança com um Launcher

Em i3 e Sway, é muito comum usar lançadores de aplicativos como `dmenu`, `rofi`, ou `bemenu`.

#### Se você usa o lançador padrão (`dmenu_run` ou `i3-dmenu-desktop`)

*   **`dmenu_run`**: Este comando simplesmente lista todos os binários disponíveis no seu `PATH` (as pastas onde o sistema procura por executáveis, como `/usr/bin`). **O nome que aparece no `dmenu` é o próprio nome do comando**. Se você digitar "editor" e aparecer "kate", "gedit" ou "gnome-text-editor", esse é o comando a ser usado no terminal .
*   **`i3-dmenu-desktop`**: Este é um script mais inteligente que lê os arquivos `.desktop` dos aplicativos. Ele mostra o **nome amigável** do aplicativo (ex: "Arquivos", "Editor de Texto") no lugar do nome do binário . Para descobrir o comando real por trás desse nome bonito, você precisará investigar o arquivo `.desktop` correspondente, como explicado na seção 3 abaixo.

#### Se você usa o Rofi

O Rofi tem dois modos principais:
*   `rofi -show run`: Funciona como o `dmenu_run`, listando binários do `PATH`. O nome é o comando.
*   `rofi -show drun`: Funciona como o `i3-dmenu-desktop`, lendo os arquivos `.desktop` e mostrando nomes amigáveis .

### 3. O Método Universal: Consultar os Arquivos `.desktop`

Esta é a maneira mais confiável e funciona em qualquer ambiente Linux (GNOME, KDE, i3, Sway). Os arquivos `.desktop` guardam a ligação entre o nome que você vê no menu e o comando real a ser executado.

1.  **Encontre o arquivo `.desktop`:** Os arquivos ficam em `/usr/share/applications/` (para o sistema todo) ou `~/.local/share/applications/` (para o seu usuário). Você pode procurar por palavras-chave:
    ```bash
    # Procura por arquivos relacionados a "editor" ou "text"
    ls /usr/share/applications/ | grep -i editor
    ls /usr/share/applications/ | grep -i text
    ```
2.  **Inspecione o arquivo:** Com o nome do arquivo (ex: `org.gnome.TextEditor.desktop`), use o `cat` ou `grep` para ver seu conteúdo:
    ```bash
    cat /usr/share/applications/org.gnome.TextEditor.desktop | grep -E "^Name=|^Exec="
    ```
    A saída será algo como:
    ```
    Name=Editor de Texto
    Exec=gnome-text-editor %U
    ```
    Pronto! A linha `Exec` mostra o comando real, que você pode usar no terminal (`gnome-text-editor`) .

### Tabela Rápida de Comandos Úteis

| Para descobrir... | No i3 (X11) | No Sway (Wayland) | Em qualquer WM |
| :--- | :--- | :--- | :--- |
| **Nome de app já aberto** | `xprop \| grep WM_CLASS`  | `swaymsg -t get_tree \| grep app_id`  | `ps aux \| grep nome_do_app` |
| **Comando por nome amigável** | `cat /usr/share/applications/ | ...` | `cat /usr/share/applications/ | ...` | **`grep "Name=SeuApp" /usr/share/applications/*.desktop -l`**  |
| **Comando real do app** | `cat /caminho/do/app.desktop \| grep Exec` | `cat /caminho/do/app.desktop \| grep Exec` | **`grep Exec /usr/share/applications/*.desktop`** |

Com essas ferramentas, você pode descobrir que o editor de texto simples instalado no seu i3 pode ser o `geany`, `mousepad`, `leafpad`, `kate` ou até mesmo o `gnome-text-editor` — basta investigar!
