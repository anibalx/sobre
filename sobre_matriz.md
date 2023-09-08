## Example 1
> Matriz de 2ª ordem: 2 linhas e 2 colunas
```
     ┌        ┐
     │ -5  -3 │
A => │        │
     │ +3  +2 │
     └        ┘
```

---

## Transposta (A^+)
> linhas viram colunas
```
     ┌        ┐             ┌        ┐
     │ -5  -3 │             │ -5  +3 │
A => │        │  ->  A^+ => │        │
     │ +3  +2 │             │ -3  +2 │
     └        ┘             └        ┘
```

---

## Indetidade (In)
> Os elementos da diagonal principal, são sempre 1. Os outros elementos, são sempre 0.
```
     ┌        ┐            ┌        ┐
     │ -5  -3 │            │ +1  +0 │
A => │        │  ->  I2 => │        │
     │ +3  +2 │            │ +0  +1 │
     └        ┘            └        ┘
```
> I2 == inversa de segunda ordem

---

## Inversa (A^-1)
> A * A^-1 = In

### Inversa: método sistema
```
     ┌        ┐            ┌      ┐           ┌        ┐
     │ -5  -3 │            │ a  b │           │ +1  +0 │
A => │        │  * A^-1 => │      │  =  I2 => │        │ ->
     │ +3  +2 │            │ c  d │           │ +0  +1 │
     └        ┘            └      ┘           └        ┘

     ┌                      ┐   ┌        ┐
     │ -5a  -3c    -5b -3d  │   │ +1  +0 │
  => │                      │ = │        │ ->
     │ +3a  +2c    +3b +2d  │   │ +0  +1 │
     └                      ┘   └        ┘
```

> SISTEMA 1:
```
    ┌                           ┌
    │ -5a  -3c = 1  * (+2)      │ -10a  -6c = 2 
 => │                       ->  │                ->
    │ +3a  +2c = 0  * (+3)      │ +09a  +6c = 0 
    └                           └
 
    ┌
    │ -10a = 2
 => │           -> -10a + 9a = 2 -> -a = 2 -> -a (*-1) = 2 (-1) -> a = -2
    │ +09a = 0
    └
 
  -> +3a  +2c = 0 -> +3(-2) + 2c = 0 -> +3(-2) = -2c -> 2c = -3(-2) -> c = 6/2 -> c = 3
```

> SISTEMA 2:
```
    ┌                          ┌
    │ -5b -3d = 0  * (+2)      │ -10b -6d = 0
 => │                      ->  │
    │ +3b +2d = 1  * (+3)      │ +09b +6d = 3
    └                          └

    ┌
    │ -10b = 0
 => │           -> -10b + 9b = 2 -> -b = 3 -> -b (*-1) = 3 (-1) -> b = -3
    │ +09b = 3
    └

 -> -5b  -3d = 0 -> -5(-3) - 3d = 0 -> 15 -3d = 0 -> 15 = 3d -> d = 15/3 -> d = 5
```


> INVERSA:
```
     ┌        ┐
     │ -5  -3 │
A => │        │
     │ +3  +2 │
     └        ┘

        ┌      ┐             ┌        ┐
        │ a  b │             │ -2  -3 │
A^-1 => │      │  =  A^-1 => │        │
        │ c  d │             │ +3  +5 │
        └      ┘             └        ┘
```

### Inversa: método determinante
> 1º Dividir os termos pelo determinante (d)
```
        ┌        ┐
        │ -5  -3 │
A^-1 => │        │ d = (-5 * 2) - (-3 + 3) -> d = -10 - (-9) -> d = -10 + 9 -> d = -1
        │ +3  +2 │
        └        ┘

        ┌              ┐    ┌        ┐
        │ -5/-1  -3/-1 │    │ +5  +3 │
A^-1 => │              │ => │        │
        │ +3/-1  +2/-1 │    │ -3  -2 │
        └              ┘    └        ┘
```

> 2º Permutar (inverter a posição) os (dos) termos da diagonal principal e 
```
        ┌        ┐    ┌        ┐
        │ +5  +3 │    │ -2  +3 │
A^-1 => │        │ => │        │
        │ -3  -2 │    │ -3  +5 │
        └        ┘    └        ┘
```

> 3º inverter o sinal dos termos da diagonal secundária
```
        ┌        ┐    ┌        ┐
        │ +5  +3 │    │ -2  -3 │
A^-1 => │        │ => │        │
        │ -3  -2 │    │ +3  +5 │
        └        ┘    └        ┘
```

---

## Soma e Subtração de Matrizes
> A^-1 + A^+ - In
```
        ┌        ┐           ┌        ┐           ┌        ┐
        │ -2  -3 │           │ -5  +3 │           │ +1  +0 │
A^-1 => │        │  + A^+ => │        │  -  I2 => │        │ ->
        │ +3  +5 │           │ -3  +2 │           │ +0  +1 │
        └        ┘           └        ┘           └        ┘

     ┌                         ┐    ┌        ┐
     │ -2 -5 -(+1)  -3 +3 -(+0)│    │ -8  +0 │
A => │                         │ => │        │
     │ +3 -3 -(+0)  +5 +2 -(+1)│    │ +0  +6 │
     └                         ┘    └        ┘
```

---

## Example 2
> Matriz de 3ª ordem: 3 linhas e 3 colunas
```
     ┌         ┐
     │ 1  2  3 │
A => │         │
     │ 0  1  4 │
     │         │
     │ 5  6  0 │
     └         ┘
```

### Matriz 3x3: determinante
> 1º repita as duas primeiras colunas, após a terceira coluna
```
     ┌         ┐         ┌               ┐
     │ 1  2  3 │         │ 1  2  3  1  2 │
     │         │         │               │
A => │ 0  1  4 │    A => │ 0  1  4  0  1 │
     │         │         │               │
     │ 5  6  0 │         │ 5  6  0  5  6 │
     └         ┘         └               ┘
```

> 2º multiple os elementos das diagonais
```
     ┌               ┐
     │ 1  2  3  1  2 │
     │               │
A => │ 0  1  4  0  1 │
     │               │
     │ 5  6  0  5  6 │
     └               ┘

d = -( (5 * 1 * 3) + (6 * 4 * 1) + (0 * 0 * 2) ) + (1 * 1 * 0) + (2 * 4 * 5) + (3 * 0 * 6)
```

> 3º calcule o determinante
```
d = -( 15 + 24 + 0 ) + 0 + 40 + 0

d = -( 15 + 24 + 0 ) + 40

d = -( 39 ) + 40

d = -39 + 40 -> d = 1
```

### Matriz 3x3: adjunta
> 1º repita as duas primeiras colunas, após a terceira coluna
```
     ┌               ┐
     │ 1  2  3  1  2 │
     │               │
A => │ 0  1  4  0  1 │
     │               │
     │ 5  6  0  5  6 │
     └               ┘
```

> 2º repita as duas primeiras linhas, abaixo da terceira linha
```
     ┌               ┐
     │ 1  2  3  1  2 │
     │               │
     │ 0  1  4  0  1 │
     │               │
A => │ 5  6  0  5  6 │
     │               │
     │ 1  2  3  1  2 │
     │               │
     │ 0  1  4  0  1 │
     └               ┘
```

> 3º ignore a primeira linha e a primeira coluna
```
     ┌               ┐
     │ x  x  x  x  x │
     │               │
     │ x  1  4  0  1 │
     │               │
A => │ x  6  0  5  6 │
     │               │
     │ x  2  3  1  2 │
     │               │
     │ x  1  4  0  1 │
     └               ┘
```

> 4º calcule o determinante de cada coluna (2x2) da matriz
```
     ┌               ┐
     │ x  x  x  x  x │
     │               │
     │ x  1  4  0  1 │
     │               │
A => │ x  6  0  5  6 │
     │               │
     │ x  2  3  1  2 │
     │               │
     │ x  1  4  0  1 │
     └               ┘

       ┌      ┐
       │ 1  4 │
L1,C1  │      │ (1*0) - (4*6) => 0 - 24 => -24
       │ 6  0 │
       └      ┘
       ┌      ┐
       │ 6  0 │
L1,C2  │      │ (6*3) - (0*2) => 18 - 0 => +18
       │ 2  3 │
       └      ┘
       ┌      ┐
       │ 2  3 │
L1,C3  │      │ (2*4) - (3*1) => 8 - 3 => +05
       │ 1  4 │
       └      ┘


       ┌      ┐
       │ 4  0 │
L2,C1  │      │ (4*5) - (0*0) => 20 - 0 => +20
       │ 0  5 │
       └      ┘
       ┌      ┐
       │ 0  5 │
L2,C2  │      │ (0*1) - (5*3) => 0 - 15 => -15
       │ 3  1 │
       └      ┘
       ┌      ┐
       │ 3  1 │
L2,C3  │      │ (3*0) - (1*4) => 0 - 4 => -04
       │ 4  0 │
       └      ┘


       ┌      ┐
       │ 0  1 │
L3,C1  │      │ (0*6) - (1*5) => 0 - 5 => -05
       │ 5  6 │
       └      ┘
       ┌      ┐
       │ 5  6 │
L3,C2  │      │ (5*2) - (6*1) => 10 - 6 => +04
       │ 1  2 │
       └      ┘
       ┌      ┐
       │ 1  2 │
L3,C3  │      │ (1*1) - (2*0) => 1 - 0 => +1
       │ 0  1 │
       └      ┘
```

> 5º Monte a matriz adjunta com: Lx,Cx
```
     ┌             ┐
     │ -24  18   5 │
     │             │
A => │ 20  -15  -4 │
     │             │
     │ -5    4   1 │
     └             ┘
```

> 6º Divida cada elemento da matriz adjunta, pelo determinante
```
d = 1

     ┌                   ┐    ┌             ┐
     │ -24/1  18/1   5/1 │    │ -24  18   5 │
     │                   │    │             │
A => │ 20/1  -15/1  -4/1 │ => │ 20  -15  -4 │
     │                   │    │             │
     │ -5/1    4/1   1/1 │    │ -5    4   1 │
     └                   ┘    └             ┘
```

---

# REFERÊNCIAS
[matriz - Rápido e Fácil ｜ Matriz Inversa](https://youtube.com/watch?v=2rtwh5-eHEk)
[matriz - 🔴MATRIZ INVERSA (FÁCIL)](https://youtube.com/watch?v=F10TdwBH8qc)
[matriz - MATRIZ INVERSA 3X3 FÁCIL!](https://youtube.com/watch?v=CNWvpQu1PKg)
