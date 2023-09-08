# BASE
Algumas demonstrações, de alguns utilitários,
usados para Data Science através da linha de comando.  

## HEAD
Mostre as 25 primeiras linhas.
```
    head -n 25 youtube.csv
```  

## GREP
Exiba os que tiverem "vasco".
```
    grep -i "vasco" youtube.csv
```  

## WC
Pegue o total
```
    cat youtube.csv | wc -l     # 828
```  

### Calcule o número total de "vasco"
```
    grep -i "vasco" youtube.csv | wc -l     # 9
```  

### Percentagem
```
    (9-2)/828 * 100% =  6 / 828 * 100 = 0.845%
```  

## CUT
Pegue o primeiro e o terceiro campo, delimitados pela vírgula.
```
    cut -f1,3 -d, youtube.csv
```  

## SORT
Pegue o primeiro e o terceiro campo, delimitados pela vírgula
Ordene a partir de uma chave numérica (nomes dos canais), delimitados pela vírgula.
```
    cut -f1,3 -d, youtube.csv | sort -k 2 -t","
```  

## UNIQ
Pegue o primeiro e o terceiro campo, delimitados pela vírgula
Ordene e prefixe a linha pelo número de ocorrência.
```
    cut -f1,3 -d, youtube.csv | sort | uniq -c
```  

## AWK
Some o segundo e o terceiro elementos, delimitados pela vírgula
e exiba o primeiro elemento com o resultado da soma.
| FILE  | SHOW |
| F,1,4 | F,5  |
| G,9,1 | G,10 |
```
    awk -F "," '{ total = $2 + $3; print $1"," total; total=0 }' extra.csv | head
```  

## SED
Delete as primeiras 5 linhas
```
    sed -i '1,5d' FILE.csv
```  

---

# Combinação

## AWK
    Some o segundo elemento e o terceiro elemento, delimitados pela vírgula
## SORT
    Ordene a patir de uma chave numérica,
    compare de acordo coma a stirng,
    mostre o resultado revertido, delimitados pela vírgula
## HEAD
    Pegue só a cabeça
```
    awk -F "," '{ total = $2 + $3; print $1"," total; total=0 }' extra.csv | sort -n -r -t"," -k 2 | head -n 1
```  

---

# Convert
```
    libreoffice --headless -convert-to csv *.xls
```  

---

# FERRRAMENTAS
* csvstat
* csvlook
* csvcut
* cut
* cat
* grep
* sort
* head
* tail
* awk
* libreoffice
* mv

---

# REFERÊNCIAS
[shell scientific_programming_school - Learn Practical Data Sciences with Bash Shell： Full Video Course!](https://youtube.com/watch?v=g3d7r7hHwmI)
