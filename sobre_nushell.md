# Nushell Commands
> enter ≈ pushd = não é igual ao pushd, mas pode ser usado da mesma forma. Na realidade, enter "cria" um novo shell que poderá ser acesado. Para navegar entre os shells, n e p.

> Comando nushell.  
```
ls 
```  

> Comando sistema.  
```
^ls 
```  

```
sys | get host.sessions == sys | host.sessions 
```  

> Lista todos arquivos do diretório atual, ordene por nome, exiba apenas os 5 primeiros resultados e retre os 2 primeiros da exibição final.  
```
ls | sort-by size | first 5 | skip 2 
```  

> Lista todos arquivos do diretório atual, ordene por nome e tamanho, exiba as linhas 2 e 5.  
```
ls | sort-by name size | nth 2 5 
```  

> Exibe a passagem do comando acima para um comando externo.  
```
echo "ls | sort-by name size | nth 2 5" | xclip -selection clipboard 
```  

> **exit** eleimina um shell, com --now todos serão eliminados.
```
exit --now 
```  

---

# REFERÊNCIAS
[Contributor Book - Nushell](https://www.nushell.sh/contributor-book/es/indice.html)  
[Book - Nushell](https://www.nushell.sh/book/pt-BR/indice.html)  
