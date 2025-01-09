# Caracter�sticas de uma linguagem OPP

## Toda linguagem POO deve: 

- permitir que voc� crie objetos que possuam par�metros que podem ser ajustados a qualquer momento, para que suas caracter�sticas e/ou qualidades reflitam os valores do mundo real. A estes par�metros chamamos PROPRIEDADES ou ATRIBUTOS; 

- permitir que sejam codificadas a��es (como um controle remoto) para que voc� possa interagir com o objeto. A estas a��es chamamos M�TODOS;  

- permitir que fique � disposi��o do programador/designer somente a parte funcional do objeto, sendo que tudo o que n�o seja interessante para ele, mas somente para o objeto, fique vis�vel. A isto chamamos ENCAPSULAMENTO;  

- permitir que novos objetos sejam criados a partir de objetos ou modelos de objetos pr�-criados. A isto chamamos HERAN�A.   

---

## Exemplos

Como exemplo de **ATRIBUTOS**, posso citar:  
* peso, 
* altura, 
* cor, 
* quantidade, 
* nome.  
Repare que estas informa��es podem ser utilizadas para representar uma infinidade de objetos (inclusive seres humanos). 

Como exemplo de **M�TODO**, posso citar a��es como:  
* Andar, 
* Correr, 
* Mergulhar, 
* Nadar,  
Repare somente o seguinte: quando se diz para uma pessoa nadar, pode-se pedir que o fa�a em determinado estilo (Borboleta ou Costas). Repare que a a��o � a mesma (Nadar), mas a a��o final � diferente.  

A isto (m�todos que possuem o mesmo nome, mas com a��es diferentes) chamamos **POLIMORFISMO** e pode ser de dois tipos: **SOBRECARGA** ou **SOBREPOSI��O**.  

A sobrecarga s� executa um m�todo espec�fico dependendo da lista de argumentos informada. A sobreposi��o **REESCREVE** um m�todo existente.  

O conceito de **ENCAPSULAMENTO** pode parecer estranho, mas imagine o seguinte: uma liga��o el�trica para uma l�mpada.  
Repare que voc� tem basicamente o seguinte:  
* um bot�o (o interruptor); 
* uma l�mpada; 
* fios; 
* eletricidade. 
O que lhe interessa aqui s�o o bot�o e a l�mpada, certo? E � justamente isto que est� � sua disposi��o.  

Toda a fia��o, a voltagem, conduites, etc, n�o lhe s�o diretamente revelados, pois est�o escondidos (encapsulados) para sua seguran�a, mas garantem que a coisa toda funcione.  

Mas, se voc� for um eletricista (o programador do objeto acima) voc� pode mexer nesta parte oculta para adaptar alguma coisa ou resolver algum problema.  

Simples assim...  

Com rela��o � **HERAN�A**, creio que o termo seja auto-explicativo. Mas, como exemplo: a partir de uma caneta esferogr�fica azul, posso criar uma vermelha aproveitando tudo que j� existe e alterando somente a cor, certo? Pois isto �, grosso modo, heran�a... 

---

## Outras informa��es �teis: 

* ABSTRA��O � o termo utilizado para identificar a modelagem/transforma��o de um objeto real em um objeto computacional;  
* CLASSE � o nome dado a um modelo de objeto;  
* INST�NCIA � o nome dado a um objeto carregado na mem�ria e em execu��o;  
* M�TODOS s�o o mesmo que Procedures e Functions em outras linguagens;  
* CONSTRUTORES s�o m�todos especiais que servem para inicializar um objeto;  
* EVENTOS s�o monitoramentos program�veis que ficam "ouvindo" determinadas a��es para executar alguma coisa. Para voc� acender nossa l�mpada acima, � necess�rio apertar o bot�o, certo? Pois um evento ficaria "ouvindo" e, caso voc� apertasse o bot�o, ele se encarregaria de disparar o m�todo "Ligar" ou "Desligar" da nossa l�mpada;  
* ASSINATURA � todo o cabe�alho de defini��o de um m�todo, sem o c�digo que o comp�e.  
