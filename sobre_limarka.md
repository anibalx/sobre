Agora também é possível utilizar o limarka através de uma imagem docker, uma ferramenta de virtualização mais eficiente do que máquina virtual. A imagem possui o TexLive 2017 completo o limarka e todas as suas dependências.

Experimente o limarka:

1. Instale o docker
2. Baixe a imagem do limarka (demora um pouco):

        docker pull edusantana/limarka

3. Baixe o modelo de trabalho acadêmico:

    wget https://github.com/abntex/trabalho-academico-limarka/archive/master.zip -O master.zip; unzip master.zip; rm master.zip
    cd trabalho-academico-limarka-master

4. Gere o PDF

        docker run --mount src=`pwd`,target=/trabalho,type=bind edusantana/limarka exec
        No Windows, substitua `pwd` pelo diretório atual entre aspas.

- Conheça o limarka: https://github.com/abntex/limarka
- Tire suas dúvidas sobre o limarka no seu chat: https://gitter.im/abntex/limarka

# REFERÊNCIAS
[Experimente elaborar seu TCC em Markdown sem precisar instalar o Latex](https://groups.google.com/g/latex-br/c/KpmlEImrc_A)
