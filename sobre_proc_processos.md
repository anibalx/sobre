# Entre em /proc
```
cd /proc
```  

---

# Entre em algum processo
> Acesse o processo, dentro de /proc, por seu PID (Process ID)
```
cd <PID>
```  

---

# Exiba nome do processo
> Ás vezes, o processo não tem nome
```
cat cmdline 
```  

---

# Páginas de memória
```
cat maps
```  

## Exemplo de saída de maps
```
    ÁREA (intervalo) DE MEM VIRTUAL (COMPOSTA DE VÁRIAS PÁGINAS) -> END INÌCIO e END FINAL
    PERMISSÔES -> r (READ) w (WRITE) x (EXECUTE) p (PRIVATE) s(SHARED)
        p (PRIVATE) -> copy on write
        s (SHARED)  -> memória compartilhada
    OFFSET -> existe como a memória referencia um arquivo

    END INÌCIO  | END FINAL  | PERMISSÔES | OFFSET | NÙMERO DO DISCO | INODE DA LIB | NOME DA LIB
    7f91d309b000-7f91d30a6000 r--p 0002c000 00:22 652489                     /usr/lib64/ld-linux-x86-64.so.2
    7f91c845a000-7f91c8e6a000 rw-s 00000000 00:2f 301                        /home/rui/.cache/icon-cache.kcache
    563e0a95c000-563e0a97f000 r--p 00000000 00:22 501147                     /usr/bin/bash

    MEMÒRIA HEAP
        558831524000-55883170c000 rw-p 00000000 00:00 0                          [heap]

    MEMÒRIA STACK
        7ffe268ca000-7ffe268eb000 rw-p 00000000 00:00 0                          [stack]

    ESPAÇOS MEMÒRIAS PARA ACELERAR SYSCALL DO LINUX
        7ffe269b3000-7ffe269b7000 r--p 00000000 00:00 0                          [vvar]
        7ffe269b7000-7ffe269b9000 r-xp 00000000 00:00 0                          [vdso]
        ffffffffff600000-ffffffffff601000 --xp 00000000 00:00 0                  [vsyscall]

    MAPEAMENTO DE MEMÒRIA ANÔNINA (não referência disco)
        OBS: sem OFFSET, DISCO e INODE
        7f91d306d000-7f91d306f000 rw-p 00000000 00:00 0
```  

---

# Referência de memória
```
cat mem
```  

## Exemplo de saída de mem
> mem é um inode/x-empty, não abre com cat
```
    CABEÇALHO ELF (A PARTIR DO MEM)
        xxd -s 0x563e0a95c000 -l 100 mem
        OSB: 0x563e0a95c000 -> END INÌCIO -> bash

    xxd /usr/bin/bash | less
    readelf /usr/bin/bash

    INVESTIGAÇÂO
        proc/maps
        vê as áreas de memória
        busque o ELF

        HEAP            -> 563e0ca03000-563e0ca45000 rw-p 00000000 00:00 0                          [heap]
        MEMÒRIA ANÔNINA -> 563e0aa6f000-563e0aa7d000 rw-p 00000000 00:00 0
        BSS             -> 563e0aa6b000-563e0aa6f000 rw-p 0010e000 00:22 501147                     /usr/bin/bash
        DATA READ WRITE -> 563e0aa68000-563e0aa6b000 r--p 0010b000 00:22 501147                     /usr/bin/bash
        DATA READ ONLY  -> 563e0aa45000-563e0aa68000 r--p 000e9000 00:22 501147                     /usr/bin/bash
        TEXT            -> 563e0a97f000-563e0aa45000 r-xp 00023000 00:22 501147                     /usr/bin/bash
        ELF             -> 563e0a95c000-563e0a97f000 r--p 00000000 00:22 501147                     /usr/bin/bash
```  

---

# Área de memória
```
less smaps
```  

## Exemplo de saída de uma área de smaps
```
    563e0aa6b000-563e0aa6f000 rw-p 0010e000 00:22 501147                     /usr/bin/bash
    Size:                 16 kB ➜ tamanho desta área de memória
    KernelPageSize:        4 kB ➜ tamanho da página (Criada pos o mapeamento de 1 a 1, não cabe na memória)
    MMUPageSize:           4 kB ➜ tamanho do MMU (Memory Management Unit)
    Rss:                  16 kB ➜ memória do processo que está na RAM, para esta aŕea de memória: no exemplo, é o bash (Redident Set Size)
    Pss:                  16 kB ➜ tamanho Resident divido por quantos processos usam a memória: RSS/total de processos usam esta memória (Proportional Set Size)
    Shared_Clean:          0 kB ➜ memória compartilhada, memória limpa (memória ainda não escrita, não está Dirty e nem wrute back pro disco)
    Shared_Dirty:          0 kB ➜ memória compartilhada, memória suja (memória escrita, está Dirty)
    Private_Clean:         0 kB ➜ memória não compartilhada (faz copy on write), memória limpa (memória ainda não escrita, não está Dirty e nem wrute back pro disco)
    Private_Dirty:        16 kB ➜ memória não compartilhada (faz copy on write), memória suja (memória escrita, está Dirty)
    Referenced:           16 kB ➜ memória lida recentemente (quais páginas foram recentemente lidas) e serão retoradas ao disco
    Anonymous:            16 kB ➜ memória área de rascunho, que não possui referência no disco
    LazyFree:              0 kB ➜ memória dita ao kernel: não vou usar, se quiser: desaloca
    AnonHugePages:         0 kB ➜ mecanismo para aumentar a página de memória
    ShmemPmdMapped:        0 kB ➜ 
    FilePmdMapped:         0 kB ➜ 
    Shared_Hugetlb:        0 kB ➜ 
    Private_Hugetlb:       0 kB ➜ 
    Swap:                  0 kB ➜ memória área de troca (memória que vem para a swap -> memória anônina: memória escrita, já alterada)
    SwapPss:               0 kB ➜ tamanho Swap divido por quantos processos usam a memória: Swap/total de processos usam esta memória (Swap Proportional Set Size)
    Locked:                0 kB ➜ quantas páginas não devem ir ao disco (segurança, leitura mais rápida)
    THPeligible:    0 ➜ 
    VmFlags: rd wr mr mw me ac sd ➜ Flags
```  

---

CRIE

    giordano.py
```
    #!/usr/bin/python3

    import time
    import mmap

    # mmap -> -1, memória anônima (sem file descriptor -> sem chamada ao kernel, para não chamar a função open)
    with mmap.mmap(-1, 64) as mm:
        beer = input("Digite a cerva favorita: ")
        mm.write(str.encode(beer)) # grava no endereço de memória (memória anônima)

        print("Vou printar a cerva favorita")
        while True:
            mm.seek(0) # volta ao começo do memória map (mapa de memória)
            print(mm.readline().decode("utf-8").strip()) # lê a a linha, decodifica, corta o último caracter (\$) e printa na tela
            time.sleep(1) # com intervalo de 1 segundo
```

    badtux.py
```
    #!/usr/bin/python3

    import sys

    pid = input("digite o PID (ID do processo): ")
    mem_file = open(f"/proc/{pid}/mem", "rb+")

    address = int(input("Digite o endereço de memória da cerva: "), 16)
    mem_file.seek(address) # leva o ponteiro para onde "address" aponta

    beer = input("Digite a cerva favorita: ") + "\n"
    mem_file.write(str.encode(beer))
    mem_file.flush()

    print("Veja a cerva favorita de antes!")
```

EXECUTE
    python3 giordano.py

    # Pega PID
    ps -ef | grep gio

    # Acesse o mapeamento de memória de "gio"
    cd /proc/<PID>/maps

    # Python gera um /dev/zero
    563e0aa6b000-563e0aa6f000 rw-p 0010e000 00:22 501147                     /dev/zero (deleted)

    # Exiba a saída: <CERVA>
    xxd -s 0x563e0aa6b000 -l 10 /proc/<PID>/maps

    python3 badtux.py


CACHE
    apt install vmtouch time
    free -wh
    sysctl -w vm.drop_chaches=3
    free -wh
    head -c 16 </dev/urandom > escrita
    free -wh
    vmtouch -v escrita # Exiba as áreas de memória Resident (RSS)
    grep Dirty /proc/mem/info
    sync
    grep Dirty /proc/mem/info
    /usr/bin/time wc -l escrita



  /*
   * stack_e_heap.c
   *
   * Verificar número do processo
   *
   * Compile o programa (vamos usar o gcc): 
   *    gcc -o memoria_stack_e_heap memoria_stack_e_heap.c
   *
   * Execute o programa: 
   *    ./memoria_stack_e_heap
   *
   * Abra outro terminal e execute: 
   *    ps auxw
   *
   * Procure o nome do programa e pegue o número do processo
   * Entre na pasta proc/<NUMERO_DO_PROCESSO>: 
   *    cd /proc/<NUMERO_DO_PROCESSO>
   *
   * Exiba as informações do arquivos maps: 
   *    cat maps
   *
   * Procure por [heap] e [stack]
   * Calcule o tamanho alocado: pegue o endereço final (segundo) e subtraia o endereço de início (primeiro)
   *    final - inicial
   *
   * ambos estão no lado mais à esquerda da exibição do arquivo
   */
