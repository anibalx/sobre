# Systemd
```
  systemd-analyze syscall-filter <ARG>     # filtra as syscall
```

# STRACE
Ferramenta usada para ler syscall (chamada de sistema) realizada pelo processo

* -f || --follow-forks == Rastrear processos filhos como eles são criados por processos atualmente rastreados como resultado das chamadas do sistema fork(2), vfork(2) e clone(2).
```
  strace -f <COMMAND>
```

* -p || --attach == Anexar ao strace o process ID ( pid ) e começar a traçar.
```
  strace -p <PID>
```

* -o || --output
```
  strace -o <FILE_NAME> -f <COMMAND>
```

* -c || --summary-only == Contar tempo, chamadas e erros para cada chamada do sistema e relatar um resumo na saída do programa, suprimindo a saída regular.
```
  strace -c -o <FILE_NAME> -f <COMMAND>
```

* -e || --expr == Uma expressão qualificada que modifica quais eventos rastreá-los ou como rastreá-los.
* trace=write  == pega só as chamadas (syscall) write
```
  strace -e trace=write -o <FILE_NAME> -f <COMMAND>
  strace -e trace=read -o <FILE_NAME> -f <COMMAND>
  strace -e trace=write,read -o <FILE_NAME> -f <COMMAND>
```

## EX: 
Dado um caso específico, onde está rodando um script numa máquina, mas não sei o que faz,
você consegue saber:
  onde está escrevendo um arquivo?
  qual máquina ele conecta?
  qual ferramenta você usa?
  qual outra ferramenta você usa? sysdig

* network && connect == syscalls usadas para indentificar conexão da máquina com outra máquina
```
  strace -e trace=write,read,network,connect -fp 1795
```
