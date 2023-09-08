# REPL
Um loop de leitura-avaliação-impressão,
também denominado de nível superior interativo ou 
shell de linguagem, 
é um ambiente de programação de computador
interativo 
simples 
que recebe entradas
de um único usuário, 
as executa e 
retorna o resultado ao usuário.  

Todo REPL é um shell.  


# Porque não executa
Não é um binário ELF e nem PE<32 || 64> executable (Portable executable)  
* hello.c (UTF-8/plain-text)  
* hello.py (ASCII text)  

Além disso, se tiver permissão de execução,
mas não shebang (#!/usr/bin/<INTERPRETER_FOR_MY_LANGUAGE>)
não executa.   

Isso seria como um shell que só lê português, ler também em chinês.  


# Como executa
## Hello.c

## Tipo do arquivo
* hello.c (UTF-8/plain-text)  
* hello (ELF/executable)  

## Formulação do arquivo
```
echo '
#include <stdio.h>

int main(void) {
    printf("Olá, mundo!");
}

return 0;
' > hello.c
```  

### Comando para execução
```
gcc -o hello hello.c && ./hello
```  

## Hello.py
* Se tiver permissão para executar && shebang (#!/usr/bin/env python) do interpretador (neste caso, python)  

## Tipo do arquivo
* Python script, ASCII text executable  

## Formulação do arquivo
```
echo '
#!/usr/bin/env python

print("Olá, mundo!")
' > hello.py
```  

### Comando para execução
```
python a.py
```  

---

# XXD
* mostra saída em hexadecimal  
* "0 = 4 bits; 00 = 8 bits = 1 byte"  
```
	xxd hello.c
```  

* -b mostra os 6 colunas de 8 bits (1 byte, que em ASCII == traduz para uma letra)  
```
	xxd -b hello.c
```   

* -l <NUM> mostra o octeto específicado pelo NUM (número)  
```
	xxd -l 8 hello.c
```   

* -c <NUM> mostra o número de colunas especificadas pelo NUM (número)  
```
	xxd -c 8 hello.c
```   


* -S || --source == código que será exibido em Assembly  
* --disassemble  == exiba os códigos mnemônicos dos assembler para as instruções de máquina do arquivo  
```
	objdump -S --disassemble hello
```  
```
	objdump -S --disassemble hello | head 
```  

* reconhece tipos de cabeçalhos de binários  
```
    file hello
```  
