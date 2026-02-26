# Características de uma linguagem OPP

## Toda linguagem POO deve: 

- permitir que você crie objetos que possuam parâmetros que podem ser ajustados a qualquer momento, para que suas características e/ou qualidades reflitam os valores do mundo real. A estes parâmetros chamamos PROPRIEDADES ou ATRIBUTOS; 

- permitir que sejam codificadas ações (como um controle remoto) para que você possa interagir com o objeto. A estas ações chamamos MÉTODOS;  

- permitir que fique à disposição do programador/designer somente a parte funcional do objeto, sendo que tudo o que não seja interessante para ele, mas somente para o objeto, fique visível. A isto chamamos ENCAPSULAMENTO;  

- permitir que novos objetos sejam criados a partir de objetos ou modelos de objetos pré-criados. A isto chamamos HERANÇA.   

---

## Exemplos

Como exemplo de **ATRIBUTOS**, posso citar:  
* peso, 
* altura, 
* cor, 
* quantidade, 
* nome.  
Repare que estas informações podem ser utilizadas para representar uma infinidade de objetos (inclusive seres humanos). 

Como exemplo de **MÉTODO**, posso citar ações como:  
* Andar, 
* Correr, 
* Mergulhar, 
* Nadar,  
Repare somente o seguinte: quando se diz para uma pessoa nadar, pode-se pedir que o faça em determinado estilo (Borboleta ou Costas). Repare que a ação é a mesma (Nadar), mas a ação final é diferente.  

A isto (métodos que possuem o mesmo nome, mas com ações diferentes) chamamos **POLIMORFISMO** e pode ser de dois tipos: **SOBRECARGA** ou **SOBREPOSIÇÃO**.  

A sobrecarga só executa um método específico dependendo da lista de argumentos informada. A sobreposição **REESCREVE** um método existente.  

O conceito de **ENCAPSULAMENTO** pode parecer estranho, mas imagine o seguinte: uma ligação elétrica para uma lâmpada.  
Repare que você tem basicamente o seguinte:  
* um botão (o interruptor); 
* uma lâmpada; 
* fios; 
* eletricidade. 
O que lhe interessa aqui são o botão e a lâmpada, certo? E é justamente isto que está à sua disposição.  

Toda a fiação, a voltagem, conduites, etc, não lhe são diretamente revelados, pois estão escondidos (encapsulados) para sua segurança, mas garantem que a coisa toda funcione.  

Mas, se você for um eletricista (o programador do objeto acima) você pode mexer nesta parte oculta para adaptar alguma coisa ou resolver algum problema.  

Simples assim...  

Com relação à **HERANÇA**, creio que o termo seja auto-explicativo. Mas, como exemplo: a partir de uma caneta esferográfica azul, posso criar uma vermelha aproveitando tudo que já existe e alterando somente a cor, certo? Pois isto é, grosso modo, herança... 

---

## Outras informações úteis: 

* ABSTRAÇÃO é o termo utilizado para identificar a modelagem/transformação de um objeto real em um objeto computacional;  
* CLASSE é o nome dado a um modelo de objeto;  
* INSTÂNCIA é o nome dado a um objeto carregado na memória e em execução;  
* MÉTODOS são o mesmo que Procedures e Functions em outras linguagens;  
* CONSTRUTORES são métodos especiais que servem para inicializar um objeto;  
* EVENTOS são monitoramentos programáveis que ficam "ouvindo" determinadas ações para executar alguma coisa. Para você acender nossa lâmpada acima, é necessário apertar o botão, certo? Pois um evento ficaria "ouvindo" e, caso você apertasse o botão, ele se encarregaria de disparar o método "Ligar" ou "Desligar" da nossa lâmpada;  
* ASSINATURA é todo o cabeçalho de definição de um método, sem o código que o compõe.  
