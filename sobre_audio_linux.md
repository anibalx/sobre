# Pesquisa
interact and connect my app with sound driver

---

# Directory
```
/proc/asound
```  

---

# Guia do Noob para Linux Audio: ALSA, OSS e Pulse Audio explicados

Há uma coisa
que os usuários de Linux novos e experientes podem concordar:
o áudio do Linux é confuso.
Não apenas várias tecnologias executam tarefas semelhantes,
mas a maioria delas pode ser completamente omitida
pelas distribuições Linux e seus usuários.
A situação é relativamente boa
quando se trata de distros mainstream como
Ubuntu, Debian ou Fedora
porque seus desenvolvedores fizeram um grande esforço
para fazer o áudio funcionar imediatamente,
mas o mesmo não pode ser dito sobre
Arch Linux, Gentoo, e outras distribuições minimalistas
que esperam que os usuários configurem tudo do zero.

Este artigo não fará de você um especialista em áudio do Linux,
mas, esperamos, explicará as tecnologias básicas
responsáveis por fazer o som sair dos alto-falantes
quando você abre um vídeo no YouTube ou joga um jogo no Steam.


## Arquitetura de som Linux avançada (ALSA)

Vamos começar
com a camada mais importante do áudio do Linux, ALSA.
Criada em 1998
pelo desenvolvedor de software tcheco Jaroslav Kysela, a ALSA
é responsável por dar voz a todas as distribuições Linux modernas.
Na verdade, é parte do próprio kernel do Linux,
fornecendo funcionalidade de áudio para o resto do sistema
por meio de uma interface de programação de aplicativos (API)
para drivers de dispositivo de placa de som.

O design original do ALSA
foi amplamente inspirado no driver de dispositivo Linux
para a placa de som Gravis Ultrasound,
que foi feita pela Advanced Gravis Computer Technology,
com sede no Canadá,
e se tornou muito popular na cena de demonstração
durante a década de 1990.

Suporte ALSA para todos os tipos de interfaces de áudio
graças a drivers de som totalmente modularizados,
pode gerenciar até oito dispositivos de áudio ao mesmo tempo,
acessar a funcionalidade MIDI de hardware,
realizar mixagem de hardware de vários canais e muito mais.

Os usuários normalmente interagem com o ALSA usando o alsamixer,
um programa de mixer gráfico
que pode ser usado para definir as configurações de som e
ajustar o volume de canais individuais.
O Alsamixer é executado no terminal e
você pode invocá-lo apenas digitando seu nome.
Um comando de teclado particularmente útil é
ativado pressionando a tecla M.
Este comando alterna o silenciamento do canal e
é uma correção bastante comum para muitas perguntas
postadas nos fóruns de discussão do Linux.


## Sistema de som aberto (OSS)

O site oficial da ALSA
menciona suporte para Open Sound System,
ou OSS para breve.
Até o Linux 2.5, o OSS era na verdade
o principal e único sistema de som para Linux.
O ALSA foi projetado para superar suas várias deficiências,
como o fato de não permitir
que mais de um aplicativo acessasse o hardware ao mesmo tempo.
No Linux 2.6 ALSA substituiu o OSS como o sistema de som padrão.

Quando os desenvolvedores do OSS
anunciaram que a versão do OSS teria uma licença proprietária,
os desenvolvedores do Linux
rapidamente decidiram substituí-la pelo ALSA.
Vale a pena notar que o OSS voltou a ser software livre
com o lançamento da versão 4 em 2007.
Hoje, o OSS é distribuído sob quatro licenças diferentes
(BSD, CDDL, GPL, Proprietary).

A maioria das distribuições Linux hoje em dia
nem se preocupam em ativar a camada de emulação OSS
presente no ALSA
porque quase ninguém mais precisa dela,
tornando o OSS uma relíquia do passado.


## PulseAudio

Se você não se lembra da última vez que interagiu com o ALSA
ao alterar suas configurações de áudio,
provavelmente é porque a camada voltada para o usuário
do sistema de áudio Linux
na maioria das distribuições modernas
é chamada de PulseAudio.

O PulseAudio foi lançado inicialmente em 2004 e
agora está incluído e habilitado por padrão no
Ubuntu, Linux Mint, openSUSE e outras grandes distribuições.
O trabalho do PulseAudio é passar dados de som
entre seus aplicativos e seu hardware,
direcionando sons vindos do ALSA
para vários destinos de saída,
como alto-falantes ou fones de ouvido do computador.
É por isso que é comumente referido como um servidor de som.

À primeira vista,
pode parecer que o PulseAudio
realmente não adiciona nada criticamente importante
ao áudio do Linux,
e muitos de seus críticos compartilham da mesma opinião.
Na realidade, existem muitas coisas que seriam impossíveis ou
difíceis de realizar sem ele,
incluindo misturar vários sons em um,
transferir áudio para uma máquina diferente ou
alterar o formato da amostra ou a contagem de canais.

O PulseAudio também traz compatibilidade entre plataformas
(FreeBSD, NetBSD, OpenBSD, Linux, Illumos, Solaris, macOS e, de forma limitada, Microsoft Windows).
Se você deseja controlar o PulseAudio diretamente,
em vez de interagir com ele
através de um widget de controle de volume ou
painel de algum tipo,
você pode instalar o PulseAudio Volume Control
(chamado pavucontrol na maioria dos repositórios de pacotes).

Se você achar que não tem uso
para os recursos fornecidos pelo PulseAudio,
você pode usar o ALSA puro ou
substituí-lo por um servidor de som diferente.


## PulseAudio vs. JACK

PulseAudio não é o único servidor de som para Linux.
Há também JACK,
que é um acrônimo recursivo para JACK Audio Connection Kit.
Enquanto o PulseAudio foi desenvolvido
tendo em mente as necessidades dos usuários gerais do Linux,
o JACK é destinado a DJs e profissionais de áudio,
fornecendo conexões em tempo real e
de baixa latência para dados de áudio e MIDI.

Como o JACK permite conectar as entradas e saídas de áudio
de cada um de seus aplicativos,
você pode fazer coisas muito legais com ele,
como monitorar sua própria voz,
adicionar efeitos em tempo real e muito mais.
Na verdade, o nome deste sistema de som
foi inspirado nos cabos usados em estúdios de gravação reais
para construir conexões intrincadas entre
instrumentos, sintetizadores, controladores MIDI e multitrackers.

Indiscutivelmente a maior desvantagem do JACK é
que ele geralmente funciona perfeitamente ou horrivelmente,
devido ao fato de que seu objetivo principal
é fornecer áudio de baixa latência.
Ele também requer consideravelmente mais poder de CPU
em comparação com o PulseAudio,
e é por isso que você o encontrará
principalmente em estações de trabalho profissionais
dedicadas à edição de áudio.


## Verificando Pulse Audio e ALSA

Você pode estar se perguntando,
como posso saber qual software de áudio meu computador está usando?
Para verificar se Pulse Audio e ALSA estão presentes em seu sistema,
use os dois comandos a seguir:

```
pactl || pamixer || pavucontrol
```

```
aplay -l || alsamixer
```

## Conclusão

Áudio no Linux parece complicado porque realmente é.
Desembaraçar a teia de tecnologias legadas e camadas de abstração
pode ser um verdadeiro desafio,
mesmo para usuários experientes de Linux
que conhecem os meandros do sistema operacional de cor.

Esperamos que nosso artigo tenha ajudado você
a entender melhor os componentes mais importantes
do sistema de áudio Linux, incluindo ALSA, OSS e PulseAudio.


# Referências
[Guid Linux Audio](https://linuxhint.com/guide_linux_audio/)
[Advanced Linux Sound Architecture](https://wiki.archlinux.org/title/Advanced_Linux_Sound_Architecture)
[Sound System](https://wiki.archlinux.org/title/sound_system)
