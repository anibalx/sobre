# PDFTK
> A1 == página 1
```sh
  pdftk A=<pdf_de_entrada>.pdf cat A1 output <pdf_de_saida>.pdf
```

> A1-5 == página 1 até 5
```sh
  pdftk A=<pdf_de_entrada>.pdf cat A1-5 output <pdf_de_saida>.pdf
```

> Separa página por página
```sh
  for n in {1..10} ; do pdftk A=<pdf_de_entrada>.pdf cat A$n output <pdf_de_saida>$n.pdf ; done
```
