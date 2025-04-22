# Atalhos de edição úteis no Bash

## Movimentação do cursor:
- **CTRL+A**: Move o cursor para o início da linha.
- **CTRL+E**: Move o cursor para o fim da linha.
- **ALT+B**: Move o cursor uma palavra para trás.
- **ALT+F**: Move o cursor uma palavra para frente.
- **CTRL+L**: Limpa a tela do terminal.
- **ALT+<**: Move para o início do histórico de comandos.
- **ALT+>**: Move para o fim do histórico de comandos.
- **CTRL+B**: Move o cursor um caractere para trás.
- **CTRL+F**: Move o cursor um caractere para frente.

## Edição de texto:
- **CTRL+U**: Apaga o texto da posição do cursor até o início da linha.
- **CTRL+K**: Apaga o texto da posição do cursor até o fim da linha.
- **CTRL+W**: Apaga a palavra antes do cursor.
- **ALT+D**: Apaga a palavra após o cursor.
- **CTRL+T**: Troca os dois caracteres ao redor do cursor.
- **ALT+T**: Troca duas palavras adjacentes.
- **ALT+U**: Converte a palavra após o cursor para maiúsculas.
- **ALT+L**: Converte a palavra após o cursor para minúsculas.
- **ALT+C**: Capitaliza a palavra após o cursor (primeira letra maiúscula).
- **CTRL+X Backspace**: Apaga desde o início da linha até o cursor.
- **CTRL+D**: Exclui o caractere sob o cursor.
- **CTRL+H**: Apaga o caractere à esquerda do cursor (como um Backspace).
- **CTRL+V**: Insere o próximo caractere literalmente.

## Busca e histórico:
- **CTRL+R**: Inicia a busca reversa no histórico de comandos.
- **CTRL+S**: Inicia a busca para frente no histórico de comandos.
  - **Nota**: Use `stty -ixon` para habilitar a busca se **CTRL+S** pausar a saída do terminal.
- **CTRL+G**: Sai do modo de busca no histórico.
- **CTRL+P**: Exibe o comando anterior no histórico.
- **CTRL+N**: Exibe o próximo comando no histórico.

## Inserção e alteração:
- **ALT+.**: Insere o último argumento do comando anterior.
- **ALT+SHIFT+.`**: Insere o último comando executado.
- **ALT+?**: Exibe possíveis complementos para o comando.

## Desfazer e refazer:
- **CTRL+_** ou **CTRL+/**: Desfaz a última alteração.
- **CTRL+Y**: Cola o texto previamente apagado com **CTRL+U**, **CTRL+K** ou **CTRL+W**.

## Controle de processos e jobs:
- **CTRL+Z**: Suspende o processo em execução.
- **CTRL+D**: Fecha o terminal ou encerra a sessão (se estiver em uma linha vazia).
- **CTRL+C**: Interrompe o comando em execução.
- **CTRL+\**: Finaliza o processo em execução (gera um `core dump`).

## Outros comandos úteis:
- **CTRL+X CTRL+E**: Abre o editor padrão para editar o comando atual.
- **ALT+SHIFT+.**: Insere o último comando executado.
- **ALT+?**: Exibe possíveis complementos para o comando.
